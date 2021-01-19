---
title: "Slack Notifications"
#date: 2018-05-12
draft: false
categories:
tags: ["#alerts", "#notifications", "#slack"]
author: Lawrence Lane

---

## Configuration

### 1. Install Incoming Webhooks on Slack

{{% notice tip %}}
If you’ve already installed the Incoming Webhooks app, you can skip to step 2.
{{% /notice %}}

1. Go to [Slack’s app directory](https://slack.com/apps).
2. Search for **Incoming Webhooks**. It should dynamically update a drop-down beneath the search bar.
3. Click **Incoming Webhooks**.
![Incoming Webhooks](/images/notifications-slack/incoming-webhooks.png)
4. Click **Add Configuration**.
![Add Configuration](/images/notifications-slack/add-configuration.png)
5. Select a channel from **Choose a Channel…** or create a new one.
![Choose a Chanel](/images/notifications-slack/choose-a-chanel.png)
6. Click **Add Incoming WebHooks Integration**.

### 2. Add an Integration to Slack
1. Log into your Slack client.
2. Click your username in the top left-hand corner. A menu will open.
3. Click **Administration** > **Manage Apps**.
![Manage Apps](/images/notifications-slack/manage-apps.png)
4. Navigate to **Custom Integrations**.
5. Click **Incoming WebHooks**.
6. In the Customize Name section, type your desired name. We recommend naming it CloudWisdom Event.
7. Click **Copy URL** in the Webhook URL section.
8. Click **Save Settings** at the bottom of the page.

### 3. Create a Slack Notification in CloudWisdom

{{% notice tip %}}
If you want to display a custom message for your Slack notification, you’ll have to add and configure a Webhook notification instead, using the URL in 2.11 as your Webhook notification’s URL.
{{% /notice %}}

1. Type a name for the Slack notification. We recommend naming it `Slack-{yourChannelName}` so it’s easy to find later.
![New Notification Details](/images/notifications-slack/new-notification-details.png)
2. Ensure the **Enabled checkbox** is selected.
3. For **Webhook URL**, paste the URL you obtained from creating the Slack integration.
4. Input a bot username that will be used when CloudWisdom posts to your Slack channel.
5. Click **Test and Save** to test the Slack notification. The test must return an `HTTP code 200` to pass the validation. If the test succeeds, the notification will automatically save.

## Optional Configuration

### Icons & Emojis
You can customize the icon from slack by returning to the custom Webhook integration you’ve created and editing it. To distinguish your CloudWisdom alerts in the chat, we recommend saving our logo to your computer and uploading it. You can also add an emoji or icon via CloudWisdom when editing your notification.

### Channel Override
Input a channel override. This can be a different channel (`#other-channel`), another user (`@otheruser`), or multiple users.
