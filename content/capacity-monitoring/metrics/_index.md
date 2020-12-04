---
title: "Metrics"
#date: 2018-12-03
draft: false
categories:
tags: ["#getting started", "#metrics",]
author: Lawrence Lane
type: docs
---

A metric is a quantifiable measurement whose values are monitored by CloudWisdom and used to assess the performance of an element. Metrics are always associated with one or more [elements][1].

**Examples of metrics:**

 - CPU Utilization
 - Network Bytes per Second
 - Response Time

## Collected Metrics
CloudWisdom has collected metrics for every element in the application. [Policies][2] can be created using collected metrics to determine if data is missing through [alerts][3], and further configured to fire [notifications][4]. After 15 minutes of missing data, the element suspends and the alert stops. At this point, an external event is posted to the event timeline noting that CloudWisdom has not received data.

**Example**

| Fully Qualified Name(FQN)           | Description                                                                                                               | Units   | BASE | CORR | UTIL |
|-------------------------------------|---------------------------------------------------------------------------------------------------------------------------|---------|------|------|------|
| netuitive.metrics.collected.percent | % of metrics that collected data in the last interval.Computation:((# of collected metrics) / (total # of metrics) * 100) | Percent | yes  | no   | no   |

## Computed Metrics
Computed metrics are metrics that CloudWisdom calculates using the data from multiple metrics collected on a integration. Computed metrics are used to compile utilization reports of your environment and to specify metric behavior in default policies. A metric can be identified as a computed metric if its name begins with “netuitive.”  

**Example**

| FULLY QUALIFIED NAME (FQN)              | DESCRIPTION              | UNITS | BASE |
|-----------------------------------------|--------------------------|-------|------|
| netuitive.aws.alb.totaltargethttperrors | Total Target HTTP Errors | count | yes  |


[1]: /capacity-monitoring/inventory/
[2]: /capacity-monitoring/policies/
[3]: /capacity-monitoring/alerts-page/
[4]: /capacity-monitoring/notifications/
