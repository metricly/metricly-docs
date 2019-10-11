---
title: "Efficiency Index"
#date: 2018-04-12
draft: false
categories:
tags: ["#benchmarking", "#efficiency index", ]
author: Lawrence Lane
alwaysopen: false
weight: 3
---

Metricly’s Efficiency Indexing provides an at-a-glance view of your optimization scores in terms of:
- average cost per unit (e.g., cost per CPU in the case of EC2s)
- average per-unit utilization in various dimensions (e.g., Utilization of CPU, Memory, I/O).
- an index score ranking your efficiency against fellow peers in the cloud

Simply graph your improvements by watching cost-per-unit decreasing and utilization-per-unit increasing over weeks and months.

## AWS Daily Cost

Track your total AWS Daily Cost.

![daily-cost](/images/efficiency-index/daily-cost.png)

## AWS CPU Utilization

Get a per-instance breakdown of your CPU Utilization across your AWS accounts. This value goes up as you continue to right-size resources.

![average-cpu-utilization](/images/efficiency-index/average-cpu-utilization.png)

## The Efficiency Index

The Efficiency Index generates a score by dividing your total EC2 utilization by the average cost per element. A lower score means better maximization of your cloud budget.

![index score](/images/efficiency-index/index-score.png)
