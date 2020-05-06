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
3. Ensure both **Cost Explorer API** and **Detailed Billing** are enabled.
4. Scroll to the **Detailed Billing Settings** section.
5. Select a **Report Path Prefix** from the dropdown.
![cur-lookup](/images/aws-cur/cur-lookup.png)
5. Select **Save**.  

{{% notice tip %}}

If the **Report Path Prefix** lookup is not available (and is instead a freeform text input), make sure you are using the most recent IAM role available. You can create the latest IAM role using the our [CloudFormation script](/integrations/aws-integration/aws-cloudformation-installation/).

{{% /notice %}}

---

## Cost & Usage Report Best Practices

The following best practices ensure optimal Cost & Usage report setup.

### Request CUR Setup for Resold Resources

You may not have access to your billing preferences if you have purchased AWS services through a reseller. You must contact your reseller and request to be set up with an S3 bucket to store your CUR data. This [minimal read-only IAM role](http://localhost:1313/integrations/aws-integration/aws-iam-installation/#alternative-create-a-custom-policy-with-minimal-permissions-read-only-role) can be used to allow CloudWisdom read-only access to a single S3 bucket containing the billing files that help to power our cost reporting features.

**Reseller concerned about sharing an S3 bucket?**

Virtana only reads the costs for accounts that we monitor; we discard all data for any unrelated accounts. You can also have them reach out to our support team with any questions they may have.


[1]: /integrations/aws-integration/aws-cloudformation-installation/
