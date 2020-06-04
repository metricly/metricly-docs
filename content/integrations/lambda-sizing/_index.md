---
title: "Lambda Sizing"
#date: 2018-12-12
draft: false
tags: [ "#aws", "#integrations", "#lambda" ]
author: Lawrence Lane

hidden: true
---

The Lambda Function Sizing tool parses Lambda function CloudWatch logs to pull billable duration and memory metrics. It’s primarily used to calculate a **memory utilization metric**, calculated off the max used and billable memory values. These values are then sent to CloudWisdom. The [CloudFormation template](https://console.aws.amazon.com/cloudformation/home?#/stacks/create/review?stackName=Lambda-Utilization&templateURL=https://s3-us-west-2.amazonaws.com/com-netuitive-app-usw2-lambda-assets-us-west-2/lambda-utilization/lambda-utilization.template&param_BucketLocation=app-usw2) is the easiest way to start using the project.

## Basic Workflow

1. A cron defaulted to run every 5 minutes kicks off execution of the Lambda function
2. The Lambda function collects REPORT logs from 2-1 durations ago (e.g. 10 min to 5 min ago for the default)
  - REPORT logs are the last line of each execution’s logs reporting the usage
  - Logs are paged, so high throughput functions may cause high Lambda Utilization run times
3. Each log from CloudWatch is parsed and produces CloudWisdom samples
4. Samples from all logs are collapsed into a single CloudWisdom ingest payload and sent to CloudWisdom.

## Installation

### Quickstart via CloudFormation Script

1. Open this link to be redirected to your AWS console: Launch CloudFormation Script.
2. Provide your CloudWisdom Custom API key to obtain your **APIKey** parameter. This can be found here.
3. Add any Lambda function names you want monitored to the **FunctionNames** parameter in a comma delimited list. (This function monitors itself by default.)
4. Check **I acknowledge…** checkbox at the bottom.
5. Click **Create**. In about 5 minutes, you’ll start seeing the additional metrics in CloudWisdom!

`aws.lambda.memory.utilization` and `aws.lambda.billed` are the metrics created upon installation. You can find these throughout the product in [dashboards][3], the [Metric Explorer][1] page, and the [Resource Utilization][2] report.


## Rightsizing Lambda Functions

Use the following steps to evaluate if the function can have its memory reduced. We recommend only re-sizing functions utilizing <50% of their memory.

### 1. **Check How Much RAM the function is using.**
Lambda Functions using more than 128mb of RAM should be vetted for optimization. 128mb is the minimum amount required to run a function.

### 2. **Determine if the function’s memory is highly volatile.**
You can do this by looking at its min-max memory utilization. If it varies greatly (spiking up to 70-90%), it is dangerous to reduce the memory any further without risking the occasional invocation to error out. This usually means your function is not a good candidate for resizing–but if your application can gracefully handle failures, then continue on this checklist.

### 3. Gauge how CPU intensive your function is.
If your function is CPU intensive, you may not save much money reducing the memory utilization. Less memory means less CPU. Lowering the memory increases invocation duration, thus increasing cost. For small memory allocations (less than 1.5GB) and medium invocation duration (~5-60 sec) a 50% decrease in memory usage can lead to a 100% increase in run time, resulting in the same cost. Refer to experimentation and this Medium article for more information.

### 4. Check if invocation durations are close to the 300 second limit.
Reducing the memory can increase the invocation duration which could cause more functions to time out.

### 5. Determine if function primarily makes network calls.
If so, your function is a perfect candidate to optimize memory. Network intensive Lambda functions don’t usually see much of an increase in invocation duration, which means a 50% reduction in memory is a 50% reduction in cost.


[1]: /capacity-monitoring/metrics/metric-page/
[2]: /right-sizing/reports-resource-utilization/
[3]: /dashboards/
