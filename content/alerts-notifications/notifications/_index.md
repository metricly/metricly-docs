---
title: "Notifications"
date: 2018-05-12
draft: true
categories:
tags: ["alerts", "notifications"]
author: Lawrence Lane
alwaysopen: false
weight: 
---
Notifications are optional alerts sent to another source (e.g., email, PagerDuty, OpsGenie) when an event occurs. You will only receive notifications from policies that have a notification(s) configured. While notifications are enabled by default, they will be automatically disabled if they are used in a policy and fail for a period of time.

## Using Notifications

### The Policy Editor
Set up notifications by opening the desired policy in Policy Editor. To enable or disable existing notifications, see below.

1. In the Policy Editor, under Notifications, click **Add Notification**.
2. Select the desired notification type.
3. Once a type is selected, choose a notification you have set up for the selected type. You can also create a new notification directly from here.
4. Select how often--between 5 minutes and 24 hours or never--the policy should re-notify you if a policy is creating events.
5. Enable **Notify on Clear** if you’d like to receive a notification when the policy stops triggering.
6. **Save** the policy.

### Enable/Disable Notifications
1. From the user account drop-down menu, select **Notifications**.
2. Open the desired notification.
3. Select (or clear) the **Enabled** checkbox.
4. Click **Save**.
