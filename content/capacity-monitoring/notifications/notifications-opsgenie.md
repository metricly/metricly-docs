---
title: "OpsGenie Notifications"
#date: 2018-05-12
draft: false
categories:
tags: ["#alerts", "#notifications", "#opsgenie"]
author: Lawrence Lane
---

## Configuration

### 1. Create a CloudWisdom integration within OpsGenie
1. Log in to your OpsGenie account.
2. Under Integrations, select **Metricly**.
3. Copy the **API key** provided on this page to your clipboard. You will use this to set up a new OpsGenie notification in CloudWisdom.
4. Leave the Teams and Recipients fields as ``{{teams}}`` and ``{{recipients}}``, respectively.
{{% notice tip %}}
This ensures that the Teams and Recipients you include in Part 2 are passed from CloudWisdom to your OpsGenie account, and will receive alerts.
{{% /notice %}}
5. Ensure that **Enabled** is selected.
6. Click **Save Integration**.

### 2. Link the integration to CloudWisdom
1. In CloudWisdom, navigate to **Username** > **Notifications**.
2. Click **OpsGenie** > **Add OpsGenie** and type a name for the OpsGenie notification.
3. Ensure the **Enabled checkbox** is selected.
4. For **API Key**, paste the API key you copied from your CloudWisdom Integration in OpsGenie in step 3 of Part 1.
5. For **Description**, add a description of the notification.
6. For **Teams**, type a comma-separated list of any OpsGenie teams that should receive notifications.
7. For **Recipients**, type a comma-separated list of any OpsGenie recipients that should receive notifications.
{{% notice tip %}}
If you include no teams or recipients, and when setting up a CloudWisdom Integration in OpsGenie, left the Teams and Recipients fields as {{teams}} and {{recipients}}, no parties will receive notifications for this policy. However, an alert will still appear in OpsGenie when an event for this policy is generated in CloudWisdom.
{{% /notice %}}
8. For **Tags**, type a comma-separated list of any tags you want to apply to the OpsGenie alert (e.g. tag1, tag2, tag3).
9. Click **Test and Save**.

## Optional Configuration

### About Endpoints
If you have not chosen an API instance for your OpsGenie account, it will default to the US. This can be changed to any supported OpsGenie endpoint.

**Available Endpoints:**

 - **US**: `https://api.opsgenie.com`
 - **EU**: `https://api.eu.opsgenie.com`
 - **Test**: `your test url`
