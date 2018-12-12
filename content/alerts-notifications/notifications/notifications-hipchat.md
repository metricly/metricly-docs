---
title: "HipChat Notifications"
date: 2018-05-12
draft: false
categories:
tags: ["alerts", "notifications", "hipchat"]
author: Lawrence Lane
---

Send a notification to a HipChat room when an event occurs on your Metricly Policies. HipChat notifications are re-usable across multiple policies. Read below for configuration steps.

## Configuration

### 1. Generate a room token
1. Log in to your [Hipchat](www.hipchat.com) account.
2. Navigate to the **Rooms** section.
3. Under **My Rooms**, select or create the desired room.
4. On the left panel, select **Tokens**.
5. Type a `Label` for the room and select **Send Notification** from the scopes list.
6. Click **Create** to generate a token.

### 2. Link the room with Metricly
1. Navigate to a **Policy** > **Notifications**.
2. Click **Add Notification** and choose **HipChat**.
![Select HipChat](/images/notifications-hipchat/select-hipchat.png)
3. After clicking **Add Hipchat**, ensure the **Enabled checkbox** is selected.
4. Paste the **Room Name** and **Room Token** to the corresponding fields.
5. Click **Test** and **Save**.
