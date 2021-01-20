---
title: "Contextual Bands"
#date: 2018-04-12
draft: false
categories:
tags: ["#getting started", "#analytics", "#metrics"]
author: Lawrence Lane
---
Contextual Bands represent the range of current expected values for a metric based on other correlated metrics in the learned model. In contrast to Baseline bands which look for patterns in a metric in isolation, Contextual bands take into account how the value of one metric may impact another.

The image below provides an example of a Contextual band in purple surrounding the actual, current value for a metric called Bytes In Per Second. The purple band demonstrates how CloudWisdom is able to use other correlated metrics to learn the expected value of the Bytes In Per Sec metric.

![Contextual Band Example](/images/contextual-bands/contextual-band-example.png)

Contextual Deviation conditions allow you to use Contextual bands to monitor the elements in your environment. For more information about creating policies using Contextual Deviation conditions, see Conditions.

## Contextual Example

- A policy with a Static Threshold condition of greater than 90% is applied to the CPU utilization metric for a server element. Often, when network activity increases for this element, so does CPU Utilization.
- However, each time network activity spikes and CPU utilization exceeds 90%, a Critical alert is generated.

By changing the Static Threshold condition to an Upper Contextual Deviation condition, these false alarms can be avoided. If CloudWisdom learns that a CPU utilization metric and a network activity metric belonging to the same server element are positively correlated, then it is able to determine the expected value for CPU utilization at any time, given the value of network activity. So, if the value of CPU utilization suddenly spikes to 96%, but the value of network activity shows a similar increase, CloudWisdom would conclude that the rise in CPU utilization is not cause for an alert, since it is not uncommon to see a rise in CPU utilization when there is also a rise in network activity.
