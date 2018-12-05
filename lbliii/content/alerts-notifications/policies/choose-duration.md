---
title: "Choose Duration"
date: 2018-04-12
draft: true
categories:
tags: ["alerts", "notifications", "events", "policies", "duration"]
author: Lawrence Lane
alwaysopen: false
---
 Duration is the consecutive length of time for which all the conditions in a policy must be met before an event or other optional [notification][1] is created. The default setting for metric condition duration is 5 minutes; the default (and only) setting for external event condition duration is real-time. Because Metricly aggregates data on five-minute cycles, the duration for metric conditions must be at least 5 minutes.

 {{% notice note %}}
 By setting the duration of `ExamplePolicy X` to 10 minutes, an event **will not be created** in Metricly until all the conditions in `ExamplePolicy X` have been met for the same period of 10 consecutive minutes.
 {{% /notice %}}

## Set a Duration
On Policy Editor, under the **2. Conditions** section:

1. **Metric Conditions**: Select between 5 minutes and 6 hours.
2. **External Event Conditions**: Real-time is the only available option.


[1]: afadf 
