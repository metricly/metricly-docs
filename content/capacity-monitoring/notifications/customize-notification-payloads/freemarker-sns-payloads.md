---
title: "SNS Payloads"
#date: 2018-05-12
draft: false
categories:
tags: ["#alerts", "#notifications", "#sns"]
author: Lawrence Lane
alwaysopen: false
weight:
---

## SNS Payloads
You must have AWS SNS setup in your console to use this payload type. The below payload returns the event category when active; once the event has cleared it returns CLEAR.
```
{
  "timestamp": "${eventTimestamp}",
  "category": "<#if payloadType == 'event_cleared'>CLEAR<#else>${eventCategory.name}</#if>",
  "element": "${elementFqn}",
  "policy": "${policyName}"
}
```
