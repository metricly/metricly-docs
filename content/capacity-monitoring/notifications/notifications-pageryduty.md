---
title: "PagerDuty Notifications"
#date: 2018-05-12
draft: false
categories:
tags: ["#alerts", "#notifications", "#slack"]
author: Lawrence Lane

---

## Configuration

### 1. Create a service in PagerDuty
1. Log into your **PagerDuty** account.
2. Navigate to **Configuration** > **Services**.
3. Click **Add New Services**.
![PagerDuty Add New Service](/images/notifications-pageryduty/pagerduty-add-new-service.png)
4. Type a `name` for the service and select your incident settings.
5. For _Integration Type_, click the **Select a Tool** dropdown > **Netuitive**.
6. Finish all other settings and click **Add Service**.
7. Copy the Integration Key provided. This is needed to set up a new PagerDuty notification in CloudWisdom.
![Integration Key](/images/notifications-pageryduty/integration-key.png)


### 2. Link the service with CloudWisdom
1. Navigate to a Policy and click **Notifications**.
2. Click **Add Notification** and select **PagerDuty**.
3. Type a `name` for the PagerDuty integration and ensure the **Enabled checkbox** is selected.
![Test and Save](/images/notifications-pageryduty/test-and-save.png)
4. Add the **service key** from the CloudWisdom service you created in PagerDuty.
5. Click **Test and Save**.

{{% notice tip %}}
The endpoint URL must return an `HTTP code 200` to pass the validation.
{{% /notice %}}
