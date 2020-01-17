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

Setting up an AWS integration via IAM Role is a five step process:

1. Create a new AWS integration in CloudWisdom.
 - Optionally, define data filters for AWS elements to be included/excluded in CloudWisdom using tags (key-value pair).
2. Create a custom in-line policy for Cost Explorer API access.
3. Create a custom in-line policy for Cost and Usage Reports read access.
4. Create an IAM role in your AWS Console.
5. Add your IAM Role's ARN to your AWS integration in CloudWisdom.


{{% notice tip %}}
If you already have an existing IAM role for CloudWisdom but it does not include a in-line policies for Cost Explorer or Cost and Usage Reports, start with sections 2 and 3.
{{% /notice %}}

### 1: Create a new AWS integration in CloudWisdom
1. Login to CloudWisdom and select the **Integrations** icon.
![integrations-icon](/images/AWS-IAM-Installation/integrations-icon.png)
2. Select the **Amazon Web Services** card.
3. Select **Add Integration** to create a new integration. (If updating an existing integration, select **View Current Integrations**).
![add-integration](/images/AWS-IAM-Installation/add-integration.png)
4. Provide a name for the new AWS integration.
5. Enable **Detailed Billing** and **Explorer API**.
   - Once you have finished all setup on this page, see the [Detailed Billing steps](/integrations/aws-integration/aws-detailed-billing).
6. For Authentication, select **IAM Role**.
7. In a separate, new tab, open your AWS console.

### 2: Create a Custom In-line Policy for Cost Explorer API Access

1. Log in to your **AWS Console**.
2. In **Find Services**, search for `IAM` and select the result.
![select-IAM](/images/AWS-IAM-Installation/select-iam.png)
3. Select **Policies**.
4. Select **Create Policy**.
5. Switch to the **JSON** tab.
6. Copy and paste the following code into the Policy Document section:
```
{
"Version": "2012-10-17",
"Statement": [
{
"Action": "ce:*",
"Resource": "*",
"Effect": "Allow"
}
]
}
```
7. Select **Review Policy**.
8. Provide a **Name**, such as `CostExplorerAPIReadOnly`. You must add this customer managed policy to your IAM role in **Part 4**.
9. Review the permissions summary and select **Create Policy**.

### 3: Create a Custom In-line Policy for Cost and Usage Report Read Access

1. Return to **IAM** > **Policies**.
2. Select **Create Policy**.
3. Switch to the **JSON** tab.
4. Copy and paste the following code into the Policy Document section:
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": "cur:DescribeReportDefinitions",
            "Resource": "*"
        }
    ]
}
```
5. Select **Review Policy**.
6. Provide a **Name**, such as `ReadCostAndUsageReportDefinitions`. You must add this customer managed policy to your IAM role in **Part 4**.
7. Review the permissions summary and select **Create Policy**.


### 4: Create Read Only Role (with standard permissions)

1. Log in to your **AWS Console**.
2. In **Find Services**, search for `IAM` and select the result.
![select-IAM](/images/AWS-IAM-Installation/select-iam.png)
3. Select **Roles**.
4. Select **Create role**.
5. Select **Another AWS Account**
![another-aws-accnt](/images/AWS-IAM-Installation/another-aws-accnt.png)
6. Provide the **Account ID** from your CloudWisdom AWS integration. _Leave Require MFA unchecked_.
7. Select **Next: Permissions**.
8. For Attach permission policies, add all of the following:
 - CostExplorerAPIReadOnly (**Filter policies** > **Customer Managed**)
 - ReadCostAndUsageReportDefinitions (**Filter policies** > **Customer Managed**)
 - AmazonMQReadOnlyAccess
 - ReadOnlyAccess
 ![customer-managed](/images/AWS-IAM-Installation/customer-managed.png)
9. Select **Next Step: Tags** and add any needed tags; **this is an optional step and you may skip it.**
10. Select **Next: Review**.
11. Add **Role Name**: `CloudWisdom`.
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
10. Follow **Part 3** of this guide, replacing **step 8** with your custom minimal permissions policy.

### 5: Update AWS Integration in CloudWisdom with the Role ARN

1. Return to the open CloudWisdom tab from **Step 1**.
2. Add the Role ARN from the IAM role found in your AWS Console.
![arn-role](/images/AWS-IAM-Installation/arn-role.png)
3. **Save**.
