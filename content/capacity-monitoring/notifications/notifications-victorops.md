---
title: "VictorOps Notifications"
#date: 2018-07-12
draft: false
categories:
tags: ["#alerts", "#notifications", "#victorops"]
author: Lawrence Lane
---

## Configuration
### 1. Copy REST API URL From VictorOps
1. Login to your VictorOps account.
2. Navigate to **Alert Behavior** > **Integrations**.
![Alert Behavior Integrations](/images/notifications-victorops/alert-behavior-integrations.png)
3. Search for `Metricly` and select the card.
![Search CloudWisdom](/images/notifications-victorops/search-metricly.png)
4. Click **Enable Integration**.
5. Copy the **Service API Endpoint**. This is required for the next step.
![API Key](/images/notifications-victorops/api-key.png)

### 2. Create a Webhook notification in CloudWisdom
1. In CloudWisdom, navigate to the **Policy Editor**.
2. Click tab 3, **Notifications**.
3. Click **Add Notification** and select **Webhook** as the _Notification Type_.
4. Provide a `name` for the webhook notification.
5. Choose your re-notification frequency.
6. Click **New Webhook**.
7. `Name` the Webhook.
8. For URL, paste the **Service API Endpoint** from VictorOps.
![Test and Save](/images/notifications-victorops/test-and-save.png)
9. Provided a `username` and `password` if required.
10. Click **Test and Save**.
{{% notice tip%}}
The endpoint URL must return an `HTTP code 200` to pass the validation.
{{% /notice %}}
11. Click **Save**.

### Optional Configuration
#### Headers
Add one or more headers (key-value pairs) to the webhook notification.

#### Custom Payload
Select **Custom** from the Payload drop-down menu. A text field will open after selecting Custom. You can use the following variables and/or VictorOps fields to make your notification more dynamic.

**Example**
The below example sends a notification that states the event’s category name, the name and ID of the element in violation, and the policy name of the violating element. Once the event has ended, it sends a RECOVERY notification stating the time that the event ended.

```
{
   "message_type":"<#if payloadType == "event">${eventCategory.name}</#if><#if payloadType == "event_cleared">RECOVERY</#if>",
   "entity_id":"${elementId}",
   "entity_display_name":"${elementName}",
     "state_message":"<#if payloadType == "event"> [${elementName}] [${policyName}] [${eventTimestamp}] : ${policyDescription}</#if><#if payloadType == "event_cleared">The policy ${policyName} has CLEARED for ${elementName} and is no longer generating events as of ${eventTimestamp}</#if>"
}
```

## VictorOps Fields
You can visit the [VictorOps knowledge base](http://victorops.force.com/knowledgebase/articles/Integration/Alert-Ingestion-API-Documentation/) for more information.

| Field Name              | Description                                                                                              |
|-------------------------|----------------------------------------------------------------------------------------------------------|
| message_type            | String value. This field allows the following values: INFO, WARNING, ACKNOWLEDGMENT, CRITICAL, RECOVERY.|                                                                                                          |
| entity_id               | String value. The name of the alerting entity.                                                           |
| timestamp               | Number value. Timestamp of the alert in seconds since epoch.                                             |
| state_start_time        | Number value. The time the entity entered its current state (in seconds since epoch).                    |
| state_message           | String value. Any additional status information from the alert.                                          |
| monitoring_tool         | String value. The name of the monitoring system software/application.                                    |

## Freemarker Variables

| Variable              | Description                                              |
|-----------------------|----------------------------------------------------------|
| ${elementFqn}         | The Fully Qualified Name (FQN) of the element.           |
| ${elementId}          | The type of element (e.g., SERVER, ELB, EC2, RDS, etc.). |
| ${elementLocation}    | The location of the element.                             |
| ${elementName}        | The friendly name for the element.                       |
| ${elementType}        | The type of element (e.g, SERVER, ELB, RUBY, etc.)       |
| ${event.data.results} | The description of the event as a policy violation.      |
| ${event.id}           | The ID of the event                                      |
| ${eventCategory.name} | The event category ( (Info), (Warning), or (Critical)).  |
| ${eventTimestamp}     | The time (in UTC) the event occurred.                    |
| ${policyDescription}  | The description of the policy that generated the event.  |
| ${policyId}           | The policy identification number.                        |
| ${policyName}         | The name of the policy.                                  |

```
{
  "message_type":"INFO",
  "entity_is_host":"Yes",
  "entity_id":"${elementId}",
  "state_message":"${elementName} is up,
but an event occurred at ${eventTimestamp}."
}
```
