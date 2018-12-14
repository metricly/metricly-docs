---
title: "Stride Notifications"
#date: 2018-07-12
draft: false
categories:
tags: ["alerts", "notifications", "stride"]
author: Lawrence Lane

---

Setting up alert [notifications][1] from Metricly to Stride just requires a few quick steps. Once complete, your alerts are forwarded to the designated chat room within Stride.

## Configuration
1. Log in to [Stride](https://app.stride.com/login).
2. Select a room where alerts should be delivered or create a new one.
![Create a Room](/images/notifications-stride/create-a-room.png)
3. Click **Apps** > **Add Custom App**.
![Add an App](/images/notifications-stride/add-an-app.png)
4. Click **API tokens** and input `Metricly Alerts` in **Specify a token name**.
5. Click **Create**.
6. In the popup window, copy the access token and conversation URL. These are used in the Metricly DS creation form and needed for the cURL post in testing.
7. Log into Metricly and navigate to **Account** > **Notifications** > **Stride**.
![Add Stride](/images/notifications-stride/add-stride.png)
8. Provide the new notification with a name and paste the URL obtained in Stride.
![Test and Save](/images/notifications-stride/test-and-save.png)
9. You are now set up with Stride! Remember to invite all relevant users to the channel that you have configured to receive these alerts.


[1]: /alerts-notifications/notifications
