---
title: "Events"
#date: 2018-04-12
draft: false
categories:
tags: ["#alerts", "#notifications", "#events",]
author: Lawrence Lane
type: docs
---

Events indicate that a policy has been violated, meaning all of the [policy conditions][1] have been met for the set duration. In other words, events indicate that CloudWisdom has detected anomalous behavior in one or more of the elements in your environment.

{{% notice info %}}
For example, if you create a policy for all EC2 elements with the **condition** `CPU Utilization greater than 90%` and a **duration** of `10 minutes`, an event will be generated when an EC2 element’s CPU Utilization metric exceeds 90% for 10 consecutive minutes.  
{{% /notice %}}

## Event Categories
Event categories are user-assigned via the [Policy Editor][2] and associated with the severity of the event. Each event can be assigned one category. There are three color-coded categories that indicate the severity of the event.

| Category | Color  | Description                                                                                                                   |
|----------|--------|-------------------------------------------------------------------------------------------------------------------------------|
| Info     | Blue   | The Info category indicates that a policy has been violated, but the anomalous behavior is not critical.                      |
| Warning  | Yellow | The Warning category indicates that a policy has been violated, and there will likely be a more critical event in the future. |
| Critical | Red    | The Critical category indicates that a policy has been violated, and the cause of the event should be addressed quickly.      |

## Assigning an Event Category
1. Open Policy Editor.
2. Underneath the Policy’s name, in the Category drop-down menu, select _Info_, _Warning_, or _Critical_.
3. After completing the remaining fields in Policy Editor, click **Save**.

[1]: /capacity-monitoring/policies/create-conditions
[2]: /capacity-monitoring/policies/create-edit-policies
