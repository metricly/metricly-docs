---
title: "Policies"
#date: 2018-04-12
draft: false
categories:
tags: ["alerts", "notifications", "events", "policies", "conditions", "scope"]
author: Lawrence Lane
alwaysopen: false
type: docs
---

A policy is a set of conditional tests used to set custom rules for when CloudWisdom will generate an event or other notifications. In other words, policies allow you to define various types of abnormal element behavior, then notify you when that abnormal behavior occurs.

Use the [Policy Editor][1] to add, edit, enable, disable, or delete policies.

A policy is made up of a scope, condition(s), duration, and notification(s).

- The **Scope** defines the element or elements to which a policy is applied.
- A **condition** is a test applied to an individual metric (or several) that is either true or false at any given time. For a policy to execute an event and/or notification, each of its conditions must be met.
- The **Duration** is the length of time for which the conditions in a policy must be met before an event and/or notification is executed. For example, if duration is 10 minutes, each of the conditions in a policy must be met for 10 consecutive minutes before you will receive a notification or see an event in CloudWisdom.
- A **Notification** is sent if each of a policy's conditions are met.

{{% notice tip %}}
Policies with CloudWisdom listed in the Created By column are called **default policies**. They serve as recommended policy configurations that you can edit, enable, disable, or delete. For more information about default policies, see Default policies.
{{% /notice %}}

[1]: /capacity-monitoring/policies/create-edit-policies
