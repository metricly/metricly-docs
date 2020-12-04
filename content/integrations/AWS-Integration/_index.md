---
title: "AWS"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["aws", "iam role", "cost explorer", "getting started"]
author: Lawrence Lane
type: docs
---
The Amazon Web Services (AWS) Integration allows performance data to be collected at regular intervals from AWS for analysis in CloudWisdom.

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
Regardless of the installation method used below, Cost Explorer must be enabled from the management account–even if set up on a sub-account. IAM Roles set up with the management account allow CloudWisdom to present reports spanning all of your accounts; IAM Roles set up with a sub-account only reports cost for that one account.

1. Log in to your AWS management account.
2. Navigate to Cost Explorer.
3. Click **Enable Cost Explorer**.
![Enable Cost Explorer](/images/aws-integration/enable-cost-explorer.png)
4. The API is now available for use but has no data; you can request up to a year of cost billing data from AWS.

## Installation Methods
The Access Key Method is no longer recommended; AWS recommends always using IAM Roles. Check out AWS’s Security Best Practices for more information.  

1. [CloudFormation Script][1]  
2. [IAM Method][2]  
3. [Access Keys][3]  

## Plan to Create Multiple AWS Integrations?
You can create multiple AWS integrations if you wish. If you haven’t created an AWS integration yet, continue with the installation instructions.  

### Create Additional AWS Integrations
If you’ve already created an AWS integration but want to create another one, navigate to the Integrations page (top navigation menu) and click the **Amazon Web Services** card. Your most recently created integration’s information will be available in the fields. Click **Add Integration**; a blank AWS integration setup page will appear.

### Edit Most Recently Added AWS Integration
If you’ve already created an AWS integration and want to edit the configuration information, navigate to the Integrations page (top navigation menu) and click the **Amazon Web Services** card. Your most recently created integration’s information will be available in the fields; edit as necessary.

### Edit Any AWS Integration
If you want to edit a different AWS integration, click **View Current Integrations** on the AWS integration setup page, then select the desired AWS integration.

[1]:/integrations/aws-integration/aws-cloudformation-installation
[2]:/integrations/aws-integration/aws-iam-installation
[3]:/integrations/aws-integration/aws-access-key-installation
