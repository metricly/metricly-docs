---
title: "Cost & Usage Reports"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#aws", "#detailed billing", "#s3 bucket", "#management account"]
author: Lawrence Lane
weight: 4
---

Cost & Usage Reports (CUR) have replaced Detailed Billing in AWS. These reports publish your AWS billing reports once a day in CSV format to an S3 bucket that you own. CloudWisdom uses these reports to analyze your resource costs and right sizing needs.

{{% notice warning %}}
CloudWisdom no longer supports Detailed Billing files.
{{% /notice %}}

## 1. Enable Cost & Usage Reports in AWS

Already have an existing hourly Cost & Usage Report with GZIP or ZIP compression set up? Great! Skip to Part 2 of this guide.

1. Log in to your AWS Console for your **management account**.
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
![final-steps](/images/aws-cur/final-steps.png)
14. Review your configurations.
16. Select **Review and Complete** to create the Cost and Usage Report (CUR).

It can take up to a few hours for data to populate in the S3 bucket.

## 2. Set up your AWS Integration in CloudWisdom

If you have just created your [IAM role][1], **wait 2-5 minutes** for AWS to finalize its creation before proceeding to these steps. This ensures the new role has the correct s3 access permissions when added to CloudWisdom.

1. From the side navigation menu, select **Integrations**.
2. Select the **Amazon Web Services** card and do one of the following:
   - To create your first AWS integration, continue to step 3.
   - To create another AWS integration, select **Add Integration**, and then continue to step 3.
   - To update an existing AWS integration, select **View Current Integrations**, choose an integration, and continue to step 3.
3. Provide a **Name** for the integration.
4. Enable **Cost & Usage Reports**.
5. Scroll to the **Authentication** section.
6. Add the **IAM Role ARN** created in Part 1 of this guide.
5. Scroll to the **Cost & Usage Reports settings** section.
6. Select a **Report Path Prefix** from the dropdown.
![cur-lookup](/images/aws-cur/cur-lookup.png)
7. Select **Save**.  

{{% notice tip %}}

If the **Report Path Prefix** lookup is not available (and is instead a freeform text input), make sure you are using the most recent IAM role available. You can create the latest IAM role using the our [CloudFormation script](/integrations/aws-integration/aws-cloudformation-installation/).
You also have the option to manually enter the **S3 Bucket Name** (chosen in section 1, step 7) and **Report Path Prefix** (created in section 1, step 8).
{{% /notice %}}

## 3. Link AWS Accounts (Optional)

You can link multiple AWS accounts to one AWS integration. These accounts can be either management accounts or member accounts; authentication information (IAM Role or Access Key) must be included for each linked account. Linking multiple accounts simplifies your setup process and grants access to the latest cost and right-sizing reports.

{{% notice note %}}
Only the first account assigned to an AWS Integration (from the Data Collection tab) has the ability to send performance metrics to CloudWisdom. Additional accounts added to your integration collect only cost and right sizing data. To send performance data, create a separate AWS integration.
{{% /notice %}}

1. Scroll to the top of your AWS integration's details and select the **Linked Accounts** tab.
2. Provide a **Name** for the linked account.
3. Provide an IAM Role. If none has been created for the linked account, follow [these instructions][1] to create an IAM role.
4. Select **Add**.
![add-iam-role-member-accounts](/images/aws-cur/add-iam-role-member-accounts.png)
5. Repeat for all relevant accounts.


### How to Remove a Linked Account  

You can remove linked accounts from your AWS integration using the following steps:

1. Log in to CloudWisdom.
2. Navigate to **Integrations**.
3. Select **Amazon Web Services**.
4. Select **View Current Integrations**.
5. Choose the AWS integration associated with the linked account.
6. Navigate to the **Linked Accounts** Tab.
7. Select the **Trashcan Icon** to delete.
![delete linked aws account](/images/aws-cur/delete-linked-aws-account.png)


---

## Cost & Usage Report Best Practices

The following best practices ensure optimal Cost & Usage report setup.

### Shared Management Account: How to Grant Limited Access

Some customers store their billing files in a shared management account and need to grant CloudWisdom restricted access to one specific S3 bucket. You can use the [management account permissions](/integrations/aws-integration/aws-iam-installation/#management-account-billing-permissions) to create a limited read-only IAM role when configuring your AWS integration with CloudWisdom.

For customers using a shared S3 bucket: CloudWisdom only reads the costs for accounts that we monitor; data for unrelated accounts is discarded.


[1]: /integrations/aws-integration/aws-cloudformation-installation/
