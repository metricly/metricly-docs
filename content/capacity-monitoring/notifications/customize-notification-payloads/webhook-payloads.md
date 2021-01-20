---
title: "Webhook Payloads"
#date: 2018-05-12
draft: false
categories:
tags: ["#alerts", "#notifications", "#webhook"]
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

**Example**

```
[
    {
        "source":"Sub Tenant Alert",
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
