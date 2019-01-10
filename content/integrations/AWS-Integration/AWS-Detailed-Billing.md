---
title: "Detailed Billing"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#aws", "#detailed billing", "#s3 bucket",]
author: Lawrence Lane
weight: 4
---

## How to Enable Detailed Billing
- If you already have an S3 bucket receiving billing files from Amazon, then you do not need to complete steps 1 and 2. You can go directly to step 3 to provide Metricly access to the existing files.
- If you have already created an S3 bucket, you will not need to create a separate one. Just be sure to select the correct S3 bucket in step 2.

### 1. Create an S3 Bucket

1. Log into AWS and navigate to the **Services** > **S3**.  
2. Click **Create Bucket**.  
![Create s3 Bucket](/images/AWS-Detailed-Billing/create-s3-bucket.png)
3. Type a unique `Bucket Name`, select a region, and click **Create**.  
![Create s3 Bucket pt2](/images/AWS-Detailed-Billing/create-s3-bucket-pt2.png)

## 2. Enable Detailed Billing Reports
1. In AWS, click your **Username** > **My Billing Dashboard**. Then in the left-hand menu, click **Preferences**.  
2. Select the **Receive Billing Reports** checkbox.  
3. In the Save to S3 Bucket field, enter the bucket name of the bucket you created in Step 1 and click **Sample Policy**.    
![Recieve Billing Reports](/images/AWS-Detailed-Billing/recieve-billing-reports.png)
4. Copy the generated policy.
5. In a new, separate tab, navigate to the S3 bucket you created in Step 1 (**Services** > **S3** > **Bucket Name**).
6. Navigate to the Permissions tab and click **Bucket Policy**.
7. Paste the following policy and click **Save**:
![Bucket Policy](/images/AWS-Detailed-Billing/bucket-policy.png)

```  
{
  "Version": "2008-10-17",
  "Id": "Policy1335892530063",
  "Statement": [
    {
      "Sid": "Stmt1335892150622",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::386209384616:root"
      },
      "Action": [
        "s3:GetBucketAcl",
        "s3:GetBucketPolicy"
      ],
      "Resource": "arn:aws:s3:::metricly-example"
    },
    {
      "Sid": "Stmt1335892526596",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::386209384616:root"
      },
      "Action": [
        "s3:PutObject"
      ],
      "Resource": "arn:aws:s3:::metricly-example/*"
    }
  ]
}
```
8. Return to the previous tab (Preferences section in the Billing & Cost Management page), and click **Verify** next to the Save to S3 Bucket field. For Amazon to correctly verify the bucket, the bucket must exist--_match the name you typed in the field_--and have appropriate permissions set (e.g., the sample policy you added in the previous step).  
9. Once your bucket is verified, select the check boxes within the Report section next to all of the reports, including Monthly report, Detailed billing report, Cost allocation report, and Detailed billing report with resources and tags.  
![Select Reports](/images/AWS-Detailed-Billing/select-reports.png)
10. Optionally, click **Manage report tags** below the billing report options and enable all desired tags.  
11. Click **Save Preferences**. It can take up to 24 hours before files start arriving in the S3 bucket.  

## 3. Update your AWS integration in Metricly
1. From the top navigation menu, select **Integrations**.
2. Click the **Amazon Web Services** card.
3. Toggle **Detailed Billing** and scroll to the final section.
![Enable Detailed billing](/images/AWS-Detailed-Billing/enable-detailed-billing.png)
4. Type the `S3 bucket name` into the corresponding field.
The bucket name is case sensitive and must exactly match the bucket created in Step 1.  
5. Click **Save**.  
