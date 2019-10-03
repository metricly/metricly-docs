---
title: "IAM"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#aws", "#iam role"]
author: Lawrence Lane
#pre: "<i class='fa fa-download'></i> &nbsp; "
weight: 2
---
## IAM Role Method

Setting up an AWS integration via IAM Role is a three step process:

1. Create a new AWS integration in Metricly.
 - Optionally, define data filters for AWS elements to be included/excluded in Metricly using tags (key-value pair).
2. Create an IAM role in your AWS Console.
3. Add your IAM Role's ARN to your AWS integration in Metricly.


{{% notice tip %}}
If you already have an existing IAM role for Metricly but it does not include a policy for Cost Explorer, skip to the last section.
{{% /notice %}}

### Step 1: Create a new AWS integration in Metricly
1. Login to Metricly and select the **Integrations** icon.
![integrations-icon](/images/AWS-IAM-Installation/integrations-icon.png)
2. Select the **Amazon Web Services** card.
3. Provide a name for the new AWS integration.
4. Enable **Detailed Billing** and **Explorer API**.
   - Once you have finished all setup on this page, see the [Detailed Billing steps](/integrations/aws-integration/aws-detailed-billing).
4. For Authentication, select **IAM Role**.
5. In a separate, new tab, open your AWS console.

### Step 2: Create Read Only Role (with standard permissions)

1. Log in to your **AWS Console**.
2. In **Find Services**, search for `IAM` and select the result.
![select-IAM](/images/AWS-IAM-Installation/select-iam.png)
3. Select **Roles**.
4. Select **Create role**.
5. Select **Another AWS Account**
![another-aws-accnt](/images/AWS-IAM-Installation/another-aws-accnt.png)
6. Provide the **Account ID** from your Metricly AWS integration. _Leave Require MFA unchecked_.
7. Select **Next: Permissions**.
8. For Attach permission policies, add all of the following:
 - CostExplorerAPIAccess
 - AmazonMQReadOnlyAccess
 - ReadOnlyAccess
9. Select **Next Step: Tags** and add any needed tags.
10. Select **Next: Review**.
11. Add **Role Name**: `Metricly`.
12. Select **Create Role**.  You are returned to IAM Roles in your AWS console.
13. Select the new role you have created.
14. Copy the **Role ARN**.
![role-arn](/images/AWS-IAM-Installation/role-arn.png)


#### Alternative: Create a Custom Policy with Minimal Permissions (Read Only Role)

If you want to use a limited read only access policy, you’ll need to create a custom policy _before_  creating an IAM role.

1. Log in to your **AWS Console**.
2. In **Find Services**, search for `IAM` and select the result.
![select-IAM](/images/AWS-IAM-Installation/select-iam.png)
3. Select **Policies**.
4. Select **Create Policy**.
5. Switch to the **JSON** tab.
6. Copy and paste the following code into the Policy Document section.

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
7. Select **Review Policy**.
8. Provide a **Name**.
9. Review the permissions summary and select **Create Policy**.
10. Follow **Section 2** of this guide, replacing **step 8** with your custom minimal permissions policy.

### Step 3: Update AWS Integration in Metrily with the Role ARN

1. Return to the open Metricly tab from **Step 1**.
2. Add the Role ARN from the IAM role found in your AWS Console.
![arn-role](/images/AWS-IAM-Installation/arn-role.png)
3. **Save**.

---

## Add Inline Policy to Existing IAM Role

This section is for customers who created Metricly accounts before 12/01/2018 or any customer who has an existing IAM role that is missing a policy for Cost Explorer. Adding this policy enables Metricly to report on and analyze your AWS Cost Explorer data.

### Step 1: Update IAM Role

1. In the AWS Console, Navigate to **IAM** > **Roles**.
2. Select your **Metricly** Iam role (or _Netuitive_, if you created this policy before the rebrand).

![iam-role-img](/images/AWS-IAM-Installation/iam-role-img.png)
The last policy in this list is created by our current cloud formation script.  But if this policy does not exist in your current IAM role, you can create and add it from your AWS console.


3. Select **Add inline policy** and choose the **JSON** tab to paste the following in the editor:
```
"Version": "2012-10-17",
"Statement": [
{
"Action": "ce:*",
"Resource": "*",
"Effect": "Allow"
}
]
```
4. Select **Review Policy**.
![create-policy](/images/AWS-IAM-Installation/create-policy.png)

5. Name the policy and select **Create Policy**.
![name-policy](/images/AWS-IAM-Installation/name-policy.png)

### Step 2: Enable Detailed Billing
1. Login to your Metricly account.
2. Navigate to **Integrations** > **AWS** > your datasource.
3. Enable **Detailed Billing** in Metricly.
![enable-detailed-billing](/images/AWS-IAM-Installation/enable-detailed-billing.png)
