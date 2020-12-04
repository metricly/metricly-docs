---
title: "Email Reports"
#date: 2018-12-03
draft: false
categories:
tags: ["tools", "email", "getting started" ]
author: Lawrence Lane
---

As a CloudWisdom user, you can opt-in to receiving email reports through your account profile. Email Reports enable you to stay up-to-date on cost trends, high-event elements, and recommendations for your environments _without_ having to log in to CloudWisdom. Selecting any of the links within the email opens CloudWisdom to the appropriate section.

## Available Reports
There are five main email reports available for you to enable:

- Weekly EC2 Recommendation Report
- CloudWisdom Daily Report
- Daily AWS Services Cost Report
- Daily Unattached EBS Report
- Daily EBS volumes on stopped EC2s

## Email Schedule
_CloudWisdom Daily Reports_ are generated after business hours (EST) and then sent the following day at 10:00 AM EST. _AWS Services Cost Report_ are sent daily at 08:30 AM EST. _Weekly EC2 Recommendation Reports_ for the previous week are typically sent on Sundays or Mondays. _Daily Unattached EBS Reports_ and _Daily EBS volumes on stopped EC2s_ are sent daily at 11:00 PM EST.

### Weekly EC2 Recommendation Report
How to generate a recommendation report and subscribe to weekly emails:

1. Navigate to **Cost Management** > **Right Sizing**.
2. Select the **EC2 Recommendation** tab.
3. Select **Configure** to create a new report.
4. Complete steps 1-5 in the report creation modal.
5. Select **Apply**. This generates an unsaved report.
6. Select **SAVE AS...**.
7. Input a `Name` for the report.
8. Toggle **Send Weekly Email** to active.
9. Confirm your email address or select one from the dropdown.
![send-weekly-email](/images/reports-email/send-weekly-email.png)

{{% notice tip %}}
You can unsubscribe from the weekly email report by editing the saved report and disabling the **Send Weekly Email** toggle.
{{% /notice %}}


### CloudWisdom Daily Report (per user account)
How to enable the CloudWisdom Daily Report through your account settings.

1. Navigate to **User Settings** > **Profile**.
2. Toggle **Daily Report Email** to active.
![daily-report-email](/images/reports-email/daily-report-email.png)

### Daily AWS Services Cost Report

Your Account must have the [AWS Cost Explorer API][1] enabled before being able to send an email.

How to generate a AWS Services Cost Report and subscribe to daily emails:

1. Navigate to **Cost Management** > **Bill Analysis**.
2. Select **Configure** to create a new report.
3. Complete steps 1-5 in the report creation modal.
4. Select **Apply**. This generates an unsaved report.
5. Select **SAVE AS...**.
6. Input a `Name` for the report.
7. Toggle **Send Daily Email** to active.
8. Confirm your email address or select one from the dropdown.
![aws-services-report](/images/reports-email/aws-services-report.png)


### Daily Unattached EBS Report

How to subscribe to daily Unattached EBS Report emails:

1. Navigate to **Cost Management**.
2. Scroll to the **Unattached EBS** card.
3. Toggle **Enable Daily Email**.
![unattached-ebs-daily-emails](/images/reports-email/unattached-ebs-daily-emails.png)


### Daily EBS volumes on stopped EC2s

How to subscribe to daily EBS volumes on stopped EC2s emails:

1. Navigate to **Cost Management**.
2. Scroll to the **EBS volumes on stopped EC2s** card.
3. Toggle **Enable Daily Email**.
![ebs-daily-emails](/images/reports-email/ebs-daily-emails.png)



[1]: /integrations/aws-integration/#prerequisite-enable-cost-explorer
