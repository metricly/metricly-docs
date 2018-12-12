---
title: "IAM"
date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["aws", "iam role"]
author: Lawrence Lane
pre: "<i class='fa fa-download'></i> &nbsp; "
weight: 2
---
## IAM Role Method

Setting up an AWS integration via IAM Role is a two step process:

Create a new AWS integration in Metricly using an IAM read-only role.
Optionally, filter your AWS elements for inclusion in Metricly by creating or choosing an existing tag (key-value pair), then assigning that tag to the desired elements in AWS.

### Step 1: Create a new AWS integration
1. From the top navigation menu, select Integrations.
2. Click the Amazon Web Services card.
3. Type a name for the new AWS integration. Ensure that Data Collection is selected.
4. For AWS Authentication, select IAM Role.
5. In a separate, new tab, open your AWS console.

### Step 2a: Create Read Only Role (with standard permissions)
1. Log in to your AWS Identity & Access Management (IAM) Console.
2. Once in the IAM dashboard, navigate to the Roles section.
3. Click Create New Role.
4. For Role Name, type Metricly and click Next Step.
5. For Role Type, select Role for Cross-Account Access.
6. Click Select next to the “Provide access between your AWS account and a 3rd party AWS account” option.
7. On the tab that has the AWS Integration Setup page open, copy the Account ID and the External ID provided to you.
8. On the tab that has the AWS console open, paste your Account ID and External ID into the appropriate fields. Leave Require MFA unchecked. Click Next Step.
9. For Attach Policy, add all of the following:
 - CostExplorerAPIAccess
 - AmazonMQReadOnlyAccess
 - ReadOnlyAccess
10. Click Next Step to review the role and access the Role ARN.
11. Copy the Role ARN.
12. After copying the Role ARN, click Create Role.

If you are not able to create a new read only role through the AWS Identity & Access Management (IAM) dashboard, see Access Key authentication.

Please make sure you save the role in the AWS console before you attempt the next step.

### Step 2b: Creating a Read Only Role (with minimal permissions)
If you want to use a limited read only access policy, you’ll need to create a custom policy first.

1. Log in to your AWS Identity & Access Management (IAM) Console.
2. Once in the IAM dashboard, navigate to the Policies section.
3. Click Create Policy in the top left-hand corner.
4. Click Select next to Create Your Own Policy.
5. Type a Policy Name into the field.
6. Type a description of the policy.
7. Copy and paste the following code into the Policy Document section.

```json
{
"Version": "2012-10-17",
"Statement": [
  {
    "Action": [
      "autoscaling:Describe*",        
      "ce:*",
      "cloudwatch:Describe*",
      "cloudwatch:Get*",
      "cloudwatch:List*",
      "dynamodb:Describe*",
      "dynamodb:Get*",
      "dynamodb:List*",
      "ec2:Describe*",
      "ec2:GetConsoleOutput",
      "ecs:Describe*",
      "ecs:List*",
      "elasticache:Describe*",
      "elasticache:List*",
      "elasticloadbalancing:Describe*",
      "elasticmapreduce:Describe*",
      "elasticmapreduce:List*",
      "iam:Get*",
      "kinesis:DescribeStream",
      "kinesis:Get*",
      "kinesis:List*",
      "lambda:List*",
      "rds:Describe*",
      "rds:ListTagsForResource",
      "redshift:Describe*",
      "mq:List*",
      "mq:Describe*",
      "s3:Describe*",
      "s3:Get*",
      "s3:List*",
      "sqs:Get*",
      "sqs:List*",
      "tag:Get*"
    ],
    "Effect": "Allow",
    "Resource": "*"
  }
]
}
```
