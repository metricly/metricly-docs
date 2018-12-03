---
title: "AWS Integration"
date: 2018-11-30T16:08:13-05:00
draft: true
categories: ["integration", "admin guide", "getting started"]
tags: ["aws", "detailed billing", "iam role"]
author: Lawrence Lane
---
The Amazon Web Services (AWS) Integration allows performance data to be collected at regular intervals from AWS for analysis in Metricly.

**Metrics**

For a list of collected and computed metrics, visit our Metrics List.

**Dependencies**

Must have access to an AWS account and CloudWatch metrics.

| ASG                       | EC2                      | EBS       |
|---------------------------|--------------------------|-----------|
| ELB                       | RDS                      | SQS       |
| DynamoDB                  | Kinesis Stream           | Redshift  |
| ElastiCache               | EMR                      | ECS       |
| Lambda                    | Custom CloudWatch Metric | S3 Bucket |
| Application Load Balancer | Target Group             | MQ Broker |

## Prerequisite: Enable Cost Explorer
Regardless of the installation method used below, Cost Explorer must be enabled from the master billing account–even if set up on a sub-account. IAM Roles set up with the master billing account allow Metricly to present reports spanning all of your accounts; IAM Roles set up with a sub-account only reports cost for that one account.

1. Log in to your AWS master billing account.
2. Navigate to Cost Explorer.
3. Click Enable Cost Explorer.
![Enable Cost Explorer](/images/aws-integration/enable-cost-explorer.png)
4. The API is now available for use but has no data; you can request up to a year of cost billing data from AWS.

## Installation Methods
The Access Key Method is no longer recommended; AWS recommends always using IAM Roles. Check out AWS’s Security Best Practices for more information.

{{% children  %}}

| AWS Toggle   | Description |
|--------------|---------------------------------------------------------------|
| CostExplorer | Captures billing data. This should only be enabled on 1 AWS account, the master billing data account. |
| CloudWatch   | Enable the CloudWatch toggle to monitor performance data. This can be done on multiple accounts. |
