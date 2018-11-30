---
title: "CloudFormation"
date: 2018-11-30T16:08:13-05:00
draft: true
categories: ["integration", "admin guide", "getting started"]
tags: ["aws", "detailed billing", "iam role", "cloudFormation script"]
author: Lawrence Lane
---
This installation method leverages a CloudFormation script found in step 1.4. After you make a new AWS integration in Metricly, the script populates a read-only IAM role in your AWS account and links it using the integration’s Account ID and External ID. Once created, it may take a few minutes for the status to be updated.

Create an AWS Integration in Metricly
1. Open Metricly and navigate to Integrations > AWS.
2. Create a new AWS integration. Ensure that the below tabled properties are set according to your needs.
![Enable CloudWatch](/images/CloudFormation-Installation/enable-cloudwatch.png)
3. For AWS Authentication, select **IAM Role**.
![IAM Role](/images/CloudFormation-Installation/iam-role.png)
4. Click the **CloudFormation script** link under Configure AWS Permissions. This opens a new tab in AWS.
5. Check **I acknowledge that AWS CloudFormation might create IAM resources** (squared in green).
6. Click **Create Role**.
![I acknowledge](/images/CloudFormation-Installation/i-acknowledge.png)
7. It may take a few minutes to create the role. When ready, the status turns green.
