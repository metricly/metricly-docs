---
title: "Account Admin"
#date: 2018-12-03
draft: false
categories:
tags: ["#user", "#account profile", "#billing", "#SSO", "#password", "#daily report", "#dark theme",]
author: Lawrence Lane
alwaysopen: false
weight: 8
pre:
---

![accnt-admin-header](/images/_index/accnt-admin-header.png)

## About Account Admin

Control features and functionality found in CloudWisdom through your Account Profile menu.

## Features

![account-profile](/images/account-profile/account-profile.png)

### Account Profile
Hover over any input field (other than username) and click to edit.

- **Daily Report Email**: Sends you a summary of the monitoring activity that occurred the previous day.

- **Alert Badge**: Toggles the open alert count in the navigation pane.

### Password
Update your password here.

### Integrations
A list of all active [integrations][1] in your account.

### Notifications
Home to all of your [notifications][2], divided into the following categories: Email, OpsGenie, PagerDuty, SNS, Slack, and Webhook.

### Users
Create & assume users from the users panel. There are three types of users:

- **Administrator**:
  - Can create, update, delete everything but objects created by another user. All alerts can be deleted.
  - Can create and assume Administrator, Power User, and Read Only users.
  - Can create and assume sub-accounts
  - Cannot view the CloudWisdom Billing page
- **Power User**:
  - Can create, update, delete everything but objects created by another user. All alerts can be deleted.
  - Cannot create and assume users
  - Cannot create and assume sub-accounts
  - Cannot view the CloudWisdom Billing page
- **Read Only User**:
  - Cannot create and assume users
  - Cannot create and assume and sub-accounts
  - Cannot view the CloudWisdom Billing Page
  - Cannot create, edit, or delete content in CloudWisdom

![create-user](/images/account-profile/create-user.png)


### Billing
A monthly breakdown of your CloudWisdom bill.

### SSO
Where you can set up your SSO. [Read our full SSO guide here][3].

[1]: /integrations/
[2]: /capacity-monitoring/notifications/
[3]: /integrations/sso/
