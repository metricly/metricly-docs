---
title: "Create External Event Conditions"
#date: 2018-04-12
draft: false
categories:
tags: ["alerts", "notifications", "events", "policies", "conditions", "external events", "webhooks"]
author: Lawrence Lane
weight: 3
---

External Event conditions for policies are typically used in conjunction with Webhook integrations. See the Webhook integration setup or Webhook API documentation for more information.

1. Open Policy Editor.
2. Click **Conditions**.
3. Click **Add Condition**, then select **Add External Event Condition**.
![Add External Event Condition](/images/create-external-event-conditions/add-external-event-condition.png)
4.  Type into the fields to create a proper filter:
  - **Message Contains**: A regex statement that attempts to match a word or phrase in the event message.
  - **Title Contains**: A regex statement that attempts to match a word or phrase in the event’s title.
  - **Source Contains**: A regex statement that attempts to match a word or phrase in the event’s source.
  - **Level**: What level of event should trigger this condition (_Info_, _Warning_, _Critical_).
5. After completing the remaining fields in Policy Editor, click **Save**.
