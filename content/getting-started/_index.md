---
title: "Getting Started"
#date: 2018-12-03
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#getting started", "#directory page",]
author: Lawrence Lane
alwaysopen: false
weight: 1
pre:
type: docs
---

![getting-started-header-1](/images/_index/getting-started-header-1.png)

## 1. Watch Our Product Demo
There’s no faster way to get acquainted with the UI than by watching the [demo video][1]. This tour covers both the Cost and Monitoring products, including topics like: the EC2 recommendation report, the Utilization Boxplot report, and the Cost report.

## 2. Register an Account
You’re excited to right-size your environments and lower their costs. You’ve done all your research, and you’re ready to try CloudWisdom’s **21-day free trial**. Select Sign Up at the top-right of the page and, after filling out a quick form, you’ll begin to set up CloudWisdom.

### Whitelist CloudWisdom Emails
Make sure you’re able to receive all of your emailed reports and notifications by whitelisting ``@virtana.com``.  This prevents your reports from getting caught in spam filters.

## 3. Set Up The AWS Integration
![getting-started-setup-aws](/images/_index/getting-started-setup-aws.png)

Chances are, you’re going to want to start with AWS.  

We recommend linking your AWS account using the [CloudFormation Method][2] found in our help documentation. It’s fast and gets you ready to pump in billing data. Just run the script, enable AWS Cost Explorer, and you’re ready to start monitoring.

### Trial Datasource Limit
While using the trial version of CloudWisdom you are limited to integrating with **two cloud datasources**.

### This Integration Supports
  -  Cost Reports for EC2, RDS, and S3    
  -  Resource Utilization   
  -  EC2 Recommendation   
  -  EC2 Reservation Recommendation   
  -  AWS Services Cost   
  -  ASG Recommendation   
  -  Idle Resource Discovery (ELB, EBS)

{{% notice tip %}}
Remember to enable **Cost Explorer** and **Cost & Usage Reports** before moving beyond this stage.
{{% /notice %}}

### 4. Install Agents (Linux, Windows)
Check out our most popular agents! Select on the links to read their in-depth setup documentation. These agents pull in additional cost metrics and help you take action on report insights. **Using these agents ensures the most accurate cost recommendations**.

- [Linux Agent][3]  
  Quickly deploy and collect metrics with a richer set of metadata, right out of the box. This agent also supports CloudWatch integration.

- [Windows Agent][4]  
  Monitor windows performance counters and attributes with the Windows Agent. Pre-configured to send the most important performance metrics, windows events, and system attributes, it’s powerful from the start. You can also customize it to send additional data as needed.

[1]:https://www.metricly.com/demo/
[2]:/integrations/aws-integration/aws-cloudformation-installation/
[3]:/integrations/agents/linux-agent
[4]:/integrations/agents/windows-agent
