---
title: "Email Reports"
#date: 2018-12-03
draft: false
categories:
tags: ["#tools", "#email", "#getting started" ]
author: Lawrence Lane
---

As a CloudWisdom user, you can opt-in to receiving email reports through your account profile. Email Reports enable you to stay up-to-date on cost trends, high-event elements, and recommendations for your environments _without_ having to log in to CloudWisdom. Selecting any of the links within the email opens CloudWisdom to the appropriate section.

## Email Schedule

Email Reports are generated after business hours (EST) and then sent the following day at 10:00 AM EST.

## Available Reports
There are five main email reports available for you to enable:

- Weekly Recommendation Report
- CloudWisdom Daily Report
- Daily AWS Services Report
- Daily Unattached EBS Report
- Daily EBS volumes on stopped EC2s

### Weekly Recommendation Report
To save a recommendation report:

1. Navigate to **Cost Management** > **Right Sizing**.
2. Select the **EC2 Recommendation** tab.
3. Select **Configure** to create a new report.
4. Complete steps 1-5 in the report creation modal.
3. Select **Apply**. This generates an unsaved report.
4. Select **SAVE AS...**.
4. Input a `Name` for the report.
5. Toggle **Send Weekly Email** to active.
6. Confirm your email address or select one from the dropdown.

![send-weekly-email](/images/reports-email/send-weekly-email.png)

{{% notice tip %}}
You can unsubscribe from the weekly email report by editing the saved report and disabling the **Send Weekly Email** toggle.
{{% /notice %}}


### CloudWisdom Daily Report (per Account)
You can enable the CloudWisdom Daily Report through your account settings.

1. Navigate to **User Settings** > **Profile**.
2. Toggle **Daily Report Email** to active.

![daily-report-email](/images/reports-email/daily-report-email.png)

### Daily AWS Services Report
Your Account must have the [AWS Cost Explorer API][1] enabled before being able to send an email.

1. Navigate to **Cost Management** > **Bill Analysis**.
2. Select **Configure** to create a new report.
3. Complete steps 1-5 in the report creation modal.
4. Select **Apply**. This generates an unsaved report.
5. Select **SAVE AS...**.
6. Input a `Name` for the report.
7. Toggle **Send Weekly Email** to active.
8. Confirm your email address or select one from the dropdown.

![aws-services-report](/images/reports-email/aws-services-report.png)

[1]: /integrations/aws-integration/#prerequisite-enable-cost-explorer
