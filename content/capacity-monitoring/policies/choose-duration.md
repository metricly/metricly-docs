---
title: "Choose Duration"
#date: 2018-04-12
draft: false
categories:
tags: ["#alerts", "#notifications",  "#policies", "#duration"]
author: Lawrence Lane
alwaysopen: false
---
 Duration is the consecutive length of time for which all the conditions in a policy must be met before an alert or other optional [notification][1] is created. The default setting for metric condition duration is 5 minutes; the default (and only) setting for external alert condition duration is real-time. Because CloudWisdom aggregates data on five-minute cycles, the duration for metric conditions must be at least 5 minutes.

 {{% notice note %}}
 By setting the duration of `ExamplePolicy X` to 10 minutes, an alert **will not be created** in CloudWisdom until all the conditions in `ExamplePolicy X` have been met for the same period of 10 consecutive minutes.
 {{% /notice %}}

## Set a Duration
On Policy Editor, under the **2. Conditions** section:

**Metric Conditions**: Select between 5 minutes and 6 hours.


[1]: /capacity-monitoring/notifications/
