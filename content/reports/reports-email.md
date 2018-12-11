---
title: "Email Reports"
date: 2018-12-03
draft: true
categories:
tags: ["reports", "email" ]
author: Lawrence Lane
---

Email Reports are generated and sent after business hours (EST) and can be enabled from your user account profile. Email Reports provide a quick look into your environment from the last 24 hours. Clicking any of the links within the email opens Metricly to the appropriate section.

## Available Reports
There are three main email reports available: the Weekly Recommendation Report, the Daily Top Violator Report, and the Daily AWS Cost Report.


### Weekly Recommendation Report
To save a recommendation report:

1. Navigate to **Reports** > under **Recommendations**, click **EC2** or **ASG**.
2. Set up the report with your desired filters and criteria.
3. Click **Save Report**. The Saved Reports modal appears.
4. Input a `Name` for the report.
5. Toggle **Email** to active.

![enable email](/images/reports-email/enable-email.png)

{{% notice tip %}}
You can remove a saved report from your daily report email by following the previous steps and toggling a report to inactive.
{{% /notice %}}


### Daily Top Violator Report (per Account)
You can enable the Top Violator Report through your account settings.

1. Navigate to **Account Profile**.
2. Toggle **Daily Report Email** to active.

![daily top violator report](/images/reports-email/daily-top-violator-report.png)

### Daily AWS Cost Report
Your Account must have the AWS Cost report activated before being able to send an email.

1. Navigate to your **Username** > **Beta** > **AWS Cost Report**.
2. Choose your desired View and Comparison Period.
3. Click **Save Report**. The Saved Reports modal appears.
![daily aws cost save report](/images/reports-email/daily-aws-cost-save-report.png)
4. Input a `Name` for the report.
5. Toggle **Email** to active.
![toggle email to active](/images/reports-email/toggle-email-to-active.png)
6. Select what email receives this daily report by clicking the expansion icon on the email input box. You can also add a new email to the list at this point by typing it out and hitting enter.
