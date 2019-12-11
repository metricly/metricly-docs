---
title: "Cost & Usage Reports"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#aws", "#detailed billing", "#s3 bucket",]
author: Lawrence Lane
weight: 4
---

Cost and Usage Reports (CUR) have replaced Detailed Billing in AWS. CloudWisdom recommends switching to (or starting with) a CUR setup instead of using AWS Detailed Billing.

## 1. Enable Cost & Usage Reports in AWS

1. Log in to your AWS Console.
2. Navigate to **Billing** > **Cost & Usage Reports**.
3. Select **Create report**.
![create-report](/images/aws-cur/create-report.png)
4. Name the report `HourlyCSVWithResourceIDs`.
5. Enable the **Include Resource IDs** checkbox.
![enable-resource-ids](/images/aws-cur/enable-resource-ids.png)
6. Select **Next**.
7. Select **Configure** to choose (or create) a S3 bucket that will store your files.
![save-s3-bucket](/images/aws-cur/save-s3-bucket.png)
8. Provide a **Report path prefix**, such as `CostAndUsageReports`. Do not include any leaning or trailing forward slashes.
9. Select **Hourly** under Time granularity. 
10. Select your preferred Report versioning method. Overwriting the existing report may save on your storage costs in the future.
11. Leave all data integration options unchecked.
12. Select **GZIP** for Compression type.
13. Select **Next**.
![final-steps](/images/aws-cur/final-steps.png)
14. Review your configurations.
15. Select **Review and Complete** to create the Cost and Usage Report (CUR).

It can take up to a few hours for data to populate in the S3 bucket.

## 2. Update your AWS Integration in CloudWisdom

If you have just created your IAM role, **wait 2-5 minutes** for AWS to finalize its creation before proceeding to these steps. This ensures the new role has the correct s3 access permissions when added to CloudWisdom.

1. From the side navigation menu, select **Integrations**.
2. Select the **Amazon Web Services** card.
3. Select **Cost and Usage Report (recommended)** from the Detailed Billing Source dropdown.
![detailed-billing-source](/images/aws-cur/detailed-billing-source.png)
4. Scroll to the **Detailed Billing Settings** section and complete the following fields:
   - **S3 Bucket Name**: the case sensitive name of bucket chosen in section 1, step 7.
   - **Report Path Prefix**: the path designated in section 1, step 8. `/CostAndUsageReports`.
5. Select **Save**.  

---

## Cost & Usage Report Best Practices

The following best practices ensure optimal Cost & Usage report setup.

### 1. Use Dedicated S3 Buckets

Keep your files in a dedicated S3 bucket. Having a large number of other files in the same S3 bucket requires more API calls to locate your files.

Don't write billing files from more than one AWS account into the same S3 bucket, as the filenames can be confused.


### 2. Request CUR Setup for Resold Resources

You may not have access to your billing preferences if you have purchased AWS services through a reseller. You must contact your reseller and request to be set up with an S3 bucket to store your CUR data.

{{% notice tip %}}
Extracts or summaries of your billing data must have the exact same file name format and file structure of AWS CUR files to be ingested by CloudWisdom.
{{% /notice %}}

**Reseller concerned about sharing an S3 bucket?**

Virtana only reads the costs for accounts that we monitor; we discard all data for any unrelated accounts. You can also have them reach out to our support team with any questions they may have.
