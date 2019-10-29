---
title: "Customize Notification Payloads"
#date: 2018-05-12
draft: false
categories:
tags: ["#alerts", "#notifications"]
author: Lawrence Lane
alwaysopen: false
weight:
---
 Custom JSON payloads in CloudWisdomsupport [FreeMarker writeup](https://freemarker.apache.org/). This page contains a list of examples for you to reference when creating your own notification payloads for emails, SNS, and webhooks.

## JSON Variables Available in CloudWisdom


| Variable              | Description                                              |
|-----------------------|----------------------------------------------------------|
| ${event.data.results} | The description of the event as a policy violation.      |
| ${event.id}           | The ID of the event                                      |
| ${eventCategory.name} | The event category ( (Info), (Warning), or (Critical)).  |
| ${elementFqn}         | The Fully Qualified Name (FQN) of the element.           |
| ${elementId}          | The type of element (e.g., SERVER, ELB, EC2, RDS, etc.). |
| ${elementType}        | The type of element (e.g, SERVER, ELB, RUBY, etc.)       |
| ${elementLocation}    | The location of the element.                             |
| ${elementName}        | The friendly name for the element.                       |
| ${policyId}           | The policy identification number.                        |
| ${policyName}         | The name of the policy.                                  |
| ${eventTimestamp}     | The time (in UTC) the event occurred.                    |
| ${policyDescription}  | The description of the policy that generated the event.  |

### Escaping JSON With Freemarker
Use the official FreeMarker documentation on escaping for an in-depth look on various escaping rules. Note that escaping does not work for ``'``, only ``"`` and `>`. If you do not properly escape your FreeMarker, you may not receive notifications. Remember to test any custom payloads that you create.

**Example**

```
{
  "icon": "https://www.metricly.com/wp-content/uploads/2017/06/METRICLY_LOGO_M_only.png",
  "activity": "Metricly Alerts",
  "title": "${policyName}",
  "body": "Category: ${eventCategory.name}\nElement: ${elementName}\nDescription: ${policyDescription?json_string}\nEventData: <#if event.data??><#if event.data.results??><#assign results = event.data.results?eval><#if results.conditions??><#list results.conditions as condition><#if condition?counter <= 5>${condition.expression}</#if></#list></#if></#if></#if>"
}
```
