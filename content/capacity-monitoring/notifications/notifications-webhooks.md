---
title: "Webhooks Notifications"
#date: 2018-07-12
draft: false
categories:
tags: ["#alerts", "#notifications", "#webhooks"]
author: Lawrence Lane
---

There are two main uses for webhooks: pushing data into CloudWisdom (_inbound_) and pulling data like notifications out (_outbound_).

- **Inbound**: Achieved via POST URL that can be found on the Webhook integration card.
- **Outbound**: Used by several of our notification integrations and accessible through the Webhook GET API endpoint.

For a great example of an inbound webhook usecase, see how we pushed [CloudWatch Logs into CloudWisdom][1].

When using the outbound method, you can customize the JSON payload using the [freemarker markup language](https://freemarker.apache.org/docs/xgui_imperative_formal.html) from **Account** > **Notifications** > **Webhook**.

## Configuration

###  Add a Webhook Notification
2. In CloudWisdom, navigate to the **Policy Editor**.
3. Click tab 3, **Notifications**.
4. Click **Add Notification** and select **Webhook** as the _Notification Type_.
5. Provide a `name` for the webhook notification.
6. Choose your re-notification frequency.
7. Click **New Webhook**.
8. `Name` the Webhook.
9. For URL, copy and paste the webhook’s payload URL that should receive notifications.
10. Click **Test** to test the webhook. The endpoint URL must return an `HTTP code 200` to pass the validation.
11. Click **Save**.

## Optional Configuration

### Headers
Add one or more headers (key-value pairs) to the webhook notification.

### Custom Payloads
Select **Custom** from the Payload drop-down menu. A text field will open after selecting Custom. Create a custom JSON payload in the textbox. You can use the following variables to make your notification more dynamic.

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

## Examples

### PagerDuty

```
{
  "service_key": "<your service key here from pager duty>",
  "incident_key": "${policyName} ",
  "event_type": "trigger",
  "description": "${category}: ${elementFqn} : ${policyName}",
  "client": "CloudWisdom Cloud Service",
  "client_url": "https://us.cloudwisdom.virtana.com",
  "details": {
    "category": "${category}",
    "elementFqn":"${elementFqn}",
    "elementType": "${elementType}"
  },
  "contexts": [{
    "type": "link",
    "href": "https://us.cloudwisdom.virtana.com/#/element/${elementId}/events"
  }]
}
```

### Microsoft Teams

```
{
  "service_key": "<your service key here from pager duty>",
  "incident_key": "${policyName} ",
  "event_type": "trigger",
  "description": "${category}: ${elementFqn} : ${policyName}",
  "client": "CloudWisdom Cloud Service",
  "client_url": "https://us.cloudwisdom.virtana.com",
  "details": {
    "category": "${category}",
    "elementFqn":"${elementFqn}",
    "elementType": "${elementType}"
  },
  "contexts": [{
    "type": "link",
    "href": "https://us.cloudwisdom.virtana.com/#/element/${elementId}/events"
  }]
}
```

### Slack

```
{
   <#if iconEmoji??>
      "icon_emoji":"${iconEmoji}",
   <#else>
      <#if iconUrl??>
         "icon_url":"${iconUrl}",
      <#else>
         "icon_url":"url.png",
      </#if>
   </#if>
   <#if username??>
      "username": "${username}",
   <#else>
      "username": "Event",
   </#if>
   <#if channel??>
      "channel":"${channel}",
   </#if>
   "attachments":[
      {
         "fallback":"Netuitive Policy Violation:",
         "pretext":"*Netuitive Policy Violation:*",
         "title_link":"https://www.netuitive.com",
         "color":"${color}",
         "mrkdwn_in":[
            "fields",
            "pretext"
         ],
         "fields":[
            {
               "title":"${policyName}",
               "value":"*Element*: ${elementName} \n *Type:* ${elementType}\n *Category:* ${eventCategory.name}",
               "short":true
            },
            {
               "title":"Click here to modify the Policy:",
               "value":"<${baseUrl}/policies/${policyId}|${policyName}>  \n *Click here to browse the Metrics:* \n <${baseUrl}/metrics?event_id=<#if event.id??>${event.id}</#if>&timeRangeDuration=14400&endTime=${timestamp?datetime?string.iso}|Metric Details>",
               "short":true
            },
            {
               "title":" ",
               "value":"\n *Violation:*  <#if event.data??><#if event.data.results??><#assign results = event.data.results?eval><#if results.conditions??><#list results.conditions as condition><#if condition?counter <= 5>${condition.expression}</#if></#list></#if></#if></#if>",
               "short":false
            },
            {
              "title": " ",
              "value":"\n *Description:*   ${policyDescription!"No description provided"}",
              "short":false
            }
         ],
         "footer": "Netuitive Event Message",
         "footer_icon": "url.png",
         "ts": ${timestampSeconds?c}
      }
   ]
}
```

[1]: /capacity-monitoring/events/cloudwatch-events
