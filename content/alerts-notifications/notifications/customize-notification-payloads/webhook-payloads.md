---
title: "Webhook Payloads"
date: 2018-05-12
draft: false
categories:
tags: ["alerts", "notifications", "webhook"]
author: Lawrence Lane
alwaysopen: false
weight:
---

## Webhook Payloads
Webhooks have two main payload types: inbound and outbound. Outbound payloads can be customized and sent as notifications.

To create a customized webhook payload:

1. Navigate to your **Account Profile** > **Notifications** > **Webhook**.
2. Click **+ Add Webhook**.
3. Fill out all fields; select Custom from the **Payload** dropdown.
4. Input your custom JSON + Freemarker writeup.
5. **Save**.

**Example 1**

```
{
   "message_type":"<#if payloadType == "event">${eventCategory.name}</#if><#if payloadType == "event_cleared">RECOVERY</#if>",
   "entity_id":"${elementId}",
   "entity_display_name":"${elementName}",
   "state_message":"<#if payloadType == "event"> [${elementName}] [${policyName}] [${eventTimestamp}] : ${policyDescription}</#if><#if payloadType == "event_cleared">The policy ${policyName} has CLEARED for ${elementName} and is no longer generating events as of ${eventTimestamp}</#if>"
}
```
**Example 2**

```
{"text": "${eventTimestamp}: The CPU on ${elementId} has exceeded 5% for at least 5 minutes. \n Event Category: ${eventCategory.name} \n Fqn: ${elementFqn} \n location: ${elementLocation}"}
```

**Example 3**

```
[
    {
        "source":"Scality Tenant Alert",
        "title": "${policyName}",
        "tags": [
            {
                "name":"Event Tag",
                "value": "External"
            }
        ],
        "type": "INFO",
        "data": {
            "elementId": "${elementId}",
            "level": "WARNING",
            "message": "${policyDescription}"
        }
    }
]
```
