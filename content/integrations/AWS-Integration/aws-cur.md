---
title: "Cost & Usage Reports"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#aws", "#detailed billing", "#s3 bucket", "#master billing"]
author: Lawrence Lane
weight: 4
---

Cost and Usage Reports (CUR) have replaced Detailed Billing in AWS. CloudWisdom recommends switching to (or starting with) a CUR setup instead of using AWS Detailed Billing.

{{% notice tip %}}

Already have an existing Cost and Usage Report with GZIP or ZIP compression set up? Great! Skip to part 2 of this guide.

{{% /notice %}}

## 1. Enable Cost & Usage Reports in AWS

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
![final-steps](/images/aws-cur/final-steps.png)
14. Review your configurations.
16. Select **Review and Complete** to create the Cost and Usage Report (CUR).

It can take up to a few hours for data to populate in the S3 bucket.

## 2. Update your AWS Integration in CloudWisdom

If you have just created your [IAM role][1], **wait 2-5 minutes** for AWS to finalize its creation before proceeding to these steps. This ensures the new role has the correct s3 access permissions when added to CloudWisdom.

1. From the side navigation menu, select **Integrations**.
2. Select the **Amazon Web Services** card.
3. Ensure **Cost & Usage Reports** is enabled.
4. Scroll to the **Cost & Usage Reports settings** section.
5. Select a **Report Path Prefix** from the dropdown.
![cur-lookup](/images/aws-cur/cur-lookup.png)
5. Select **Save**.  

{{% notice tip %}}

If the **Report Path Prefix** lookup is not available (and is instead a freeform text input), make sure you are using the most recent IAM role available. You can create the latest IAM role using the our [CloudFormation script](/integrations/aws-integration/aws-cloudformation-installation/).
You also have the option to manually enter the **S3 Bucket Name** (chosen in section 1, step 7) and **Report Path Prefix** (created in section 1, step 8).
{{% /notice %}}

---

## Cost & Usage Report Best Practices

The following best practices ensure optimal Cost & Usage report setup.

### Shared Master Billing Account: How to Grant Limited Access

Some customers store their billing files in a shared master billing account and need to grant CloudWisdom restricted access to one specific S3 bucket. You can use the [master billing account permissions](/integrations/aws-integration/aws-iam-installation/#master-billing-account-permissions) to create a limited read-only IAM role when configuring your AWS integration with CloudWisdom.

For customers using a shared S3 bucket: CloudWisdom only reads the costs for accounts that we monitor; data for unrelated accounts is discarded.


[1]: /integrations/aws-integration/aws-cloudformation-installation/
