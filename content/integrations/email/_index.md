---
title: "Email Notifications"
date: 2018-12-11
draft: true
tags: ["email", "integrations" ]
author: Lawrence Lane
---
You can create email templates with custom messaging that are re-usable across multiple policies, or simply choose Metricly’s default email notifications. Read below for configuration steps.

## Configuration
1. Click your **Username** > **Notifications**.
2. Click **Add Notification**.
3. Select **Email** for _Notification Type_. The following modal appears:
![email modal](/images/_index/email-modal.png)
4. Choose your frequency via the **Re-notify every** field.
5. Check **Notify on clear** if you want to be notified when the alert has ended.
6. Click **New Email** to create a new email template. The following modal appears:
![new email modal](/images/_index/new-email-modal.png)
7. Provide a `Name` for the template. A list of these show up in the Email dropdown.
8. Provide an **Email Address** to send this notification to.
9. Choose a **Default** or **Custom** Template.
  - **Default**: Sends a Metricly pre-formatted message.
  - **Custom**: Allows you to customize the Subject and Body of the email.
10. Click **Test and Save**.
11. Select your template from the **Email** dropdown.
![email dropdown](/images/_index/email-dropdown.png)
12. Click **Save**.

## Regex Variables
Use our [Regex Guide][1] to create custom payloads.

[1]: /alerts-notifications/policies/regex-guide
