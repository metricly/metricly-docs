---
title: "Onboarding Wizard"
draft: false
categories:
tags:
author: Lawrence Lane
pre:
weight: 5
---

The Onboarding Wizard is a guided setup tool that helps new users integrate their first datasource with CloudWisdom. Before using the Onboarding Wizard, CloudWisdom recommends completing some configuration steps in the AWS console. These steps ensure you have all of the required settings in place to integrate to CloudWisdom.

## 1. Configure AWS

### 1. Enable Cost Explorer
Cost Explorer must be enabled from the master billing account---even if already set up on a sub-account. IAM Roles set up with the master billing account allow CloudWisdom to present reports spanning all of your accounts; IAM Roles set up with a sub-account only reports cost for that one account.

1. Log in to your AWS master billing account.
2. Navigate to Cost Explorer.
3. Select **Enable Cost Explorer**.
![Enable Cost Explorer](/images/aws-integration/enable-cost-explorer.png)
4. The API is now available for use but has no data; you can request up to a year of cost billing data from AWS.

### 2. Enable Cost & Usage Reports in AWS

Cost and Usage Reports (CUR) have replaced Detailed Billing in AWS. CloudWisdom recommends switching to (or starting with) a CUR setup instead of using AWS Detailed Billing.

{{% notice tip %}}

Already have an existing Cost and Usage Report with GZIP or ZIP compression set up? Great! You can skip this section. You'll need to provide your CUR's Report Path Prefix at a later stage in this setup.

{{% /notice %}}

1. Log in to your AWS Console.
2. Navigate to **Billing** > **Cost & Usage Reports**.
3. Select **Create report**.
![create-report](/images/aws-cur/create-report.png)
4. Name the report `HourlyCSVWithResourceIDs`.
5. Enable the **Include resource IDs** checkbox.
![enable-resource-ids](/images/aws-cur/enable-resource-ids.png)
6. Select **Next**.
7. Select **Configure** to choose (or create) a S3 bucket that will store your files.
![save-s3-bucket](/images/aws-cur/save-s3-bucket.png)
8. Provide a **Report path prefix**, such as `CostAndUsageReports`. Do not include any leaning or trailing forward slashes; doing so may distort the file hierarchy output by AWS.
9. Select **Hourly** under Time granularity.
10. Select your preferred Report versioning method. Overwriting the existing report may save on your storage costs in the future.
11. Leave all data integration options unchecked.
12. Select **GZIP** for Compression type.
13. Select **Next**.
14. Review your configurations.
16. Select **Review and Complete** to create the Cost and Usage Report (CUR).

It can take up to a few hours for data to populate in the S3 bucket.


## 2. Complete Onboarding Wizard in CloudWisdom

### 1. Create an IAM Role

1. Log in to CloudWisdom. You are automatically directed to the Onboarding Wizard.
3. Select **Run Cloudformation Script**. This opens a new tab and is the fastest way to set up your IAM role; you will be prompted to log in to AWS.
4. Enable the **I acknowledge that AWS CloudFormation might create IAM resources** checkbox.
5. Select **Create Stack**. This process may take a few minutes. Wait for the stack to say **CREATE_COMPLETE** before proceeding to the next step.
6. Select the stack you have created. It will start with `CloudWisdom`.
7. Navigate to the **Outputs** tab.
8. Copy the **Role ARN Value**.
![role-arn-value](/images/onboarding-wizard/role-arn-value.png)
9. Return to the CloudWisdom Onboarding Wizard and paste the Role ARN into the field.
10. Select **Next: Cloudwatch**.

### 2. Configure CloudWatch Data Collection

CloudWisdom collects performance data to power analyses. The elements enabled by default are recommended and can be changed at any time.

1. Approve the list of enabled default collections; uncheck any you wish to disable.
2. Select **Next: Cost and Billing**.

### 3. Configure Cost & Billing Settings

1. Leave **Enable Cost Explorer** enabled.
2. Select a **Report Path Prefix**. The values listed are a combination of the S3 bucket name where the billing files reside followed by the full Report path prefix of the Cost & Usage report you configured.
![select-report-path](/images/onboarding-wizard/select-report-path.png)
3. Select **Next: Summary**.


{{% notice tip %}}
If the **Report Path Prefix** lookup is not available (and is instead a freeform text input), make sure you are using the most recent IAM role available. You can create the latest IAM role using the our [CloudFormation script](/integrations/aws-integration/aws-cloudformation-installation/).
You also have the option to manually enter the **S3 Bucket Name** (chosen in section 1, step 7) and **Report Path Prefix** (created in section 1, step 8).
{{% /notice %}}

### 4. Name & Finalize New Datasource

1. Provide a name for your AWS datasource.
2. Select **Confirm & Finish**.

You can create more datasources using the guides in our [Integrations][3] section.

[1]:/integrations/aws-integration/aws-cur/
[2]:/integrations/aws-integration/#prerequisite-enable-cost-explorer
[3]:/integrations/
