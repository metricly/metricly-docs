---
title: "Baseline Bands"
#date: 2018-04-12
draft: false
categories:
tags: ["#getting started", "#analytics", "#metrics"]
author: Lawrence Lane
---
Baseline Bands represent the normal operating range of a metric. CloudWisdom determines the normal operating range of a metric based on weekly patterns in the behavior of that metric.

The image below provides an example of Baseline bands in green surrounding the actual, current value for a CPU utilization metric in black. The green band demonstrates how CloudWisdom learns the expected behavior of the metric based on patterns in the behavior of that metric.

![Baseline Band Example](/images/baseline-bands/baseline-band-example.png)

To leverage the behavior learning capabilities of Baseline bands, use Upper or Lower Baseline Deviation condition tests in a policy. For more information about Baseline Deviation tests, see Conditions.

##  Baseline Example

- A policy with a Static Threshold condition of greater than 95% is applied to the CPU utilization metric for a server element.
- The actual value of that CPU utilization metric is often greater than 95% at 2:00 PM every Monday.

Using a Static Threshold test, the policy **generates a Critical event every Monday at 2:00 PM** when the value of the metric exceeds 95%. After changing the Static Threshold test to an Upper Baseline Deviation test, alerts are no longer generated when the CPU utilization metric exceeds 95% on Mondays at 2:00 PM. This is because CloudWisdom uses Baseline bands to learn this pattern. So, the spike in CPU utilization that occurs on Monday afternoons is not perceived as abnormal behavior, resulting in fewer false alarms.
