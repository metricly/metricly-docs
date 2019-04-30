---
title: "Microsoft Teams Notifications"
#date: 2018-05-12
draft: false
categories:
tags: ["#alerts", "#notifications", "#microsoft teams"]
author: Lawrence Lane

---

## Configuration
### 1. Add an Incoming Webhook in Microsoft Teams
1. Login to your Microsoft Teams account.
2. Navigate to **Store** and search for `Incoming Webhook`.
![Incoming Webhook](/images/notifications-microsoft-teams/incoming-webhook.png)
3. Choose a Microsoft Team that will receive Metricly notifications.
4. Click **Install**.
5. Select a channel from your Microsoft team and click **Set up**.
![Set up Webhook](/images/notifications-microsoft-teams/set-up-webhook.png)
6. Provide a name for your Webhook. You may also upload a photo at this point.
7. Click **Create**.
8. Copy the `Webhook URL` that is generated.
![Copy Webhook URL](/images/notifications-microsoft-teams/copy-webhook-url.png)
9. Click **Done**. The next steps are in Metricly and require the copied Webhook URL.

### 2. Create a Webhook Notification in Metricly
1. In Metricly, navigate to the **Policy Editor**.
2. Click tab **3. Notifications**.
3. Click **Add Notification** and select **Webhook** as the Notification Type.
4. Provide a `name` for the webhook notification.
5. Choose your re-notification frequency.
6. Click **New Webhook**.
7. `Name` the Webhook.
8. For **URL**, paste the endpoint URL from Microsoft Teams.
9. Provided a `username` and `password` if required.
10. Select **Custom** for Payload and input your custom JSON. (See example below on this page.) Note that a default payload does not work for Microsoft Teams notifications.
![Input Everything](/images/notifications-microsoft-teams/input-everything.png)
11. Click **Test and Save**.
{{% notice tip %}}
The endpoint URL must return an HTTP code 200 to pass the validation.
{{% /notice %}}
12. Click **Save**.

**Example**

```
{
    "@context": "http://schema.org/extensions",
    "@type": "MessageCard",
    "summary": "**Metricly Policy Violation <#if payloadType == "event_cleared">CLEARED<#else>${eventCategory.name}</#if>:**",
    "themeColor": "${color}",
    "title": "<#if payloadType == "event_cleared">CLEARED<#else>${eventCategory.name}</#if> Metricly Event:",
    "sections": [
        {
            "activityTitle": "**Metricly Policy Violation:**",
            "activitySubtitle": "${timestamp?datetime?string.iso} UTC",
            "activityImage": "https://s3-us-west-2.amazonaws.com/com-netuitive-app-usw2-slack/metricly_teams_icon.png",
            "facts": [
                {
                    "name": "Title:",
                    "value": "${policyName}"
                },
                {
                    "name": "Element:",
                    "value": "${elementName}"
                },
                {
                    "name": "Type:",
                    "value": "${elementType}"
                },
                {
                    "name": "Category:",
                    "value": "${eventCategory.name}"
                },
                {
                    "name": "Description:",
                    "value": "<#if policyDescription?has_content>${policyDescription?json_string}<#else>No description provided</#if>"
                }
            ],
            "text": "**Violation:**  <#if event.data??><#if event.data.results??><#assign results = event.data.results?eval><#if results.conditions??><#list results.conditions as condition><#if condition?counter <= 5>${condition.expression}</#if></#list></#if></#if></#if>",
            "potentialAction": [
                {
                    "@type": "OpenUri",
                    "name": "Browse Metrics",
                    "targets": [
                        {
                            "os": "default",
                            "uri": "${baseUrl}/metrics?event_id=<#if event.id??>${event.id}</#if>&timeRangeDuration=14400&endTime=${timestamp?datetime?string.iso}"
                        }
                    ]
                },
                {
                    "@type": "OpenUri",
                    "name": "Edit Policy",
                    "targets": [
                        {
                            "os": "default",
                            "uri": "${baseUrl}/policies/${policyId}"
                        }
                    ]
                }

            ]
        }
        <#if images?has_content && (images?size == 1)>
        , {
            "text": "![${images[0].elementFqn} - ${images[0].metricFqn} Metric Graph"](${images[0].url})"
        }
         </#if>         
        <#if images?has_content && (images?size > 1)>
          <#list images as image>
        , {
            "text": "![${image.elementFqn} - ${image.metricFqn} Metric Graph](${image.url})"
        }
          </#list>
      </#if>
    ]
}
```
