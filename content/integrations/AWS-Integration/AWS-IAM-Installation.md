---
title: "IAM"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["aws", "iam role", "management account"]
author: Lawrence Lane
#pre: "<i class='fa fa-download'></i> &nbsp; "
weight: 2
---

Setting up an AWS integration via IAM Role is a five step process:

1. Create a new AWS integration in CloudWisdom.
 - Optionally, define data filters for AWS elements to be included/excluded in CloudWisdom using tags (key-value pair).
2. Create a custom in-line policy for Cost Explorer API access.
3. Create a custom in-line policy for Cost and Usage Reports read access.
4. Create an IAM role in your AWS Console.
5. Add your IAM Role's ARN to your AWS integration in CloudWisdom.


{{% notice tip %}}
If you already have an existing IAM role for CloudWisdom but it does not include in-line policies for Cost Explorer or Cost and Usage Reports, start with sections 2 and 3.
{{% /notice %}}

## 1: Create a new AWS integration in CloudWisdom
1. Log in to CloudWisdom and select the **Integrations** icon.
![integrations-icon](/images/AWS-IAM-Installation/integrations-icon.png)
2. Select the **Amazon Web Services** card.
3. Select **Add Integration** to create a new integration. (If updating an existing integration, select **View Current Integrations**).
![add-integration](/images/AWS-IAM-Installation/add-integration.png)
4. Provide a name for the new AWS integration.
5. Enable **Cost Explorer API** and **Cost And Usage Reports** if applicable to this integration.
   - Once you have finished all setup on this page, see the [Cost and Usage Report steps](/integrations/aws-integration/aws-cur).
6. For Authentication, select **IAM Role**.
7. In a separate, new tab, open your AWS console.

## 2: Create a Custom In-line Policy for Cost Explorer API Access

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
"Action": "ce:Get*",
"Resource": "*",
"Effect": "Allow"
}
]
}
```
7. Select **Review Policy**.
8. Provide a **Name**, such as `CostExplorerAPIReadOnly`. You must add this customer managed policy to your IAM role in **Part 4**.
9. Review the permissions summary and select **Create Policy**.

## 3: Create a Custom In-line Policy for Cost and Usage Report Read Access

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


## 4: Create Read-Only Role

This guide includes instructions for setting up both standard and minimal read permissions.

1. Log in to your **AWS Console**.
2. In **Find Services**, search for `IAM` and select the result.
![select-IAM](/images/AWS-IAM-Installation/select-iam.png)
3. Select **Roles**.
4. Select **Create role**.
5. Select **Another AWS Account**
![another-aws-accnt](/images/AWS-IAM-Installation/another-aws-accnt.png)
6. Provide the **Account ID** from your CloudWisdom AWS integration. _Leave Require MFA unchecked_.
7. Select **Next: Permissions**.

## 5. Define Role Permissions  

There are four options available for this role: standard permissions, minimal monitoring permissions, minimal cost permissions, and management account permissions. A Minimal permission policy must be created _before_ being assigned to an IAM Role.

{{% notice tip %}}
We recommend opening a second browser tab to follow this section when creating minimal read-only policies. Once the policy is created, use the original tab to resume setup of the IAM role.

{{% /notice %}}

### Standard Permissions

Grants blanket read-only access to collect CloudWatch **performance metrics** and **billing files** from S3.

{{% expand "View Steps." %}}

Continuing from **Section 4**:

1. For Attach permission policies, add all of the following:
 - CostExplorerAPIReadOnly (**Filter policies** > **Customer Managed**)
 - ReadCostAndUsageReportDefinitions (**Filter policies** > **Customer Managed**)
 - AmazonMQReadOnlyAccess
 - ReadOnlyAccess
 ![customer-managed](/images/AWS-IAM-Installation/customer-managed.png)
2. Select **Next Step: Tags** and add any needed tags; **this is an optional step and you may skip it.**
3. Select **Next: Review**.
4. Add **Role Name**: `CloudWisdom`.
5. Select **Create Role**.  You are returned to IAM Roles in your AWS console.
6. Select the new role you have created.
7. Copy the **Role ARN** and move on to **Section 6**.
![role-arn](/images/AWS-IAM-Installation/role-arn.png)

{{% /expand %}}

### Minimal Monitoring Permissions

Grants read-only access to collect CloudWatch **performance metrics** for the AWS services CloudWisdom provides an integration.

{{% expand "View Steps." %}}

In a Separate Browser Tab:

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
        "cloudwatch:Get*",
        "cloudwatch:List*",
        "cloudwatch:Describe*",
        "dynamodb:Get*",
        "dynamodb:List*",
        "dynamodb:Describe*",
        "ec2:Get*",
        "ec2:Describe*",
        "ecs:Describe*",
        "ecs:List*",
        "elasticache:List*",
        "elasticache:Describe*",
        "elasticfilesystem:List*",
        "elasticfilesystem:Describe*",
        "elasticloadbalancing:Describe*",
        "elasticmapreduce:Get*",
        "elasticmapreduce:List*",
        "elasticmapreduce:Describe*",
        "iam:Get*",
        "kinesis:Get*",
        "kinesis:List*",
        "kinesis:Describe*",
        "lambda:Get*",
        "lambda:List*",
        "mq:List*",
        "mq:Describe*",
        "redshift:Get*",
        "redshift:List*",
        "redshift:Describe*",
        "route53:Get*",
        "route53:List*",
        "rds:List*",
        "rds:Describe*",
        "s3:Get*",
        "s3:List*",
        "s3:Describe*",
        "sqs:Get*",
        "sqs:List*",
        "tag:Get*",
        "tag:Describe*"
      ],
      "Effect": "Allow",
      "Resource": "*"
    }
  ]
}
```

7\. Select **Review Policy**. <br>
8\. Provide a **Name**. <br>
9\. Review the permissions summary and select **Create Policy**. <br>

Continuing From **Section 4**:

1. Add the minimal read-only monitoring policy to _Attach permission policies_. This policy can be found by filtering for **customer managed** policies.
 ![customer-managed](/images/AWS-IAM-Installation/customer-managed.png)
2. Select **Next Step: Tags** and add any needed tags; **this is an optional step and you may skip it.**
3. Select **Next: Review**.
4. Add **Role Name**: `CloudWisdom Monitoring`.
5. Select **Create Role**.  You are returned to IAM Roles in your AWS console.
6. Select the new role you have created.
7. Copy the **Role ARN** and move on to **Section 6**.
![role-arn](/images/AWS-IAM-Installation/role-arn.png)

{{% /expand %}}

### Minimal Cost Permissions

Grants read-only access to collect CloudWatch **performance metrics** and **billing files** limited to only the AWS services that CloudWisdom provides cost reports for.

{{% expand "View Steps." %}}

In a Separate Browser Tab:

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
        "cloudwatch:Get*",
        "cloudwatch:List*",
        "cloudwatch:Describe*",
        "ec2:Get*",
        "ec2:Describe*",
        "elasticloadbalancing:Describe*",
        "iam:Get*",
        "rds:Describe*",
        "rds:List*",
        "s3:Get*",
        "s3:List*",
        "s3:Describe*",
        "tag:Get*",
        "tag:Describe*"
      ],
      "Effect": "Allow",
      "Resource": "*"
    }
  ]
}


```
7\. Select **Review Policy**. <br>
8\. Provide a **Name**. <br>
9\. Review the permissions summary and select **Create Policy**.<br>

Continuing From **Section 4**:

1. Add the minimal read-only cost policy to _Attach permission policies_. This policy can be found by filtering for **customer managed** policies.
 ![customer-managed](/images/AWS-IAM-Installation/customer-managed.png)
2. Select **Next Step: Tags** and add any needed tags; **this is an optional step and you may skip it.**
3. Select **Next: Review**.
4. Add **Role Name**: `CloudWisdom Billing`.
5. Select **Create Role**.  You are returned to IAM Roles in your AWS console.
6. Select the new role you have created.
7. Copy the **Role ARN** and move on to **Section 6**.
![role-arn](/images/AWS-IAM-Installation/role-arn.png)

{{% /expand %}}

#### Management Account Billing Permissions

Grants read-only access to collect billing files from a **single s3 bucket** that can be located in a management account.

{{% expand "View Steps." %}}

In a Separate Browser Tab:

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
      "Effect": "Allow",
      "Action": [
        "s3:ListBucket"
      ],
      "Resource": [
        "arn:aws:s3:::your-bucket-name"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject"
      ],
      "Resource": [
        "arn:aws:s3:::your-bucket-name/*"
      ]
    }
  ]
}
```

7\. Replace `your-bucket-name` with the name of the bucket associated with your CUR files. <br>
8\. Select **Review Policy**. <br>
9\. Provide a **Name**. <br>
10\. Review the permissions summary and select **Create Policy**.<br>

Continuing From **Section 4**:

1. Add the minimal read-only cost policy to _Attach permission policies_. This policy can be found by filtering for **customer managed** policies.
 ![customer-managed](/images/AWS-IAM-Installation/customer-managed.png)
2. Select **Next Step: Tags** and add any needed tags; **this is an optional step and you may skip it.**
3. Select **Next: Review**.
4. Add **Role Name**: `CloudWisdom Billing`.
5. Select **Create Role**.  You are returned to IAM Roles in your AWS console.
6. Select the new role you have created.
7. Copy the **Role ARN** and move on to **Section 6**.
![role-arn](/images/AWS-IAM-Installation/role-arn.png)

{{% /expand %}}

## 6: Update AWS Integration in CloudWisdom with the Role ARN

1. Return to the open CloudWisdom tab from **Section 1**.
2. Add the Role ARN from the IAM role found in your AWS Console.
![arn-role](/images/AWS-IAM-Installation/arn-role.png)
3. **Save**.


[1]: /integrations/aws-integration/aws-cur
