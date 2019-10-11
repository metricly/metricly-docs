---
title: "Detailed Billing"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#aws", "#detailed billing", "#s3 bucket",]
author: Lawrence Lane
weight: 4
---

## 1. Enable Detailed Billing Reports in AWS

1. Log in to your AWS console.
2. Navigate to **Username** > **My Billing Dashboard**.
![my-billing-dboard](/images/AWS-Detailed-Billing/my-billing-dboard.png)
3. Navigate to **Billing Preferences**.
![navigate-billing-preferences](/images/AWS-Detailed-Billing/navigate-billing-preferences.png)
4. Expand **Detailed Billing Reports [Legacy]** and check **Turn on the legacy Detailed Billing...**.
![enable-detail-billing-legacy](/images/AWS-Detailed-Billing/expand legacy.gif)
5. Select **Configure**. A modal appears.
6. Create an S3 bucket with a name, such as `metricly-detailed-billing`.
![create s3](/images/AWS-Detailed-Billing/create-s3.png)
7. Select **Next**. A default policy is generated.
8. Confirm the policy is correct.
![confirm policy](/images/AWS-Detailed-Billing/confirm-policy.png)
9. **Save**. Report options populate on your AWS console's Billing Preferences.
11. Enable all reports.
![enable all reports](/images/AWS-Detailed-Billing/enable-all-reports.png)
12. Select **Save Preferences**.


## 2. Update your AWS integration in Metricly

If you have just created your IAM role, **wait 2-5 minutes** for AWS to finalize its creation before proceeding to these steps. This ensures the new role has the correct s3 access permissions when added to Metricly.

1. From the top navigation menu, select **Integrations**.
2. Select the **Amazon Web Services** card.
3. Toggle **Detailed Billing** and scroll to the final section.
![Enable Detailed billing](/images/AWS-Detailed-Billing/enable-detailed-billing.png)
4. Type the `S3 bucket name` into the corresponding field.
The bucket name is case sensitive and must exactly match the bucket created in Step 1.  
5. Select **Save**.  

---


## Detailed Billing Best Practices

The following best practices ensure optimal detailed billing setup.

### 1. Use Dedicated S3  Buckets

Keep your billing files in a dedicated S3 bucket. Having a large number of other files in the same S3 bucket requires more API calls to locate your billing files.

Don't write billing files from more than one AWS account into the same S3 bucket, as the filenames can be confused.


### 2. Request Detailed Billing Setup for Resold Resources

You may not have access to your billing preferences if you have purchased AWS services through a reseller. You must contact your reseller and request to be set up with an S3 bucket to store your detailed billing data.

{{% notice tip %}}
Extracts or summaries of your billing data must have the exact same file name format and file structure of AWS detailed billing files to be ingested by Metricly.
{{% /notice %}}

**Reseller concerned about sharing an S3 bucket?**

Metricly only reads the costs for accounts that we monitor; we discard all data for any unrelated accounts. You can also have them reach out to our support team with any questions they may have.
