---
title: "NLB Metrics"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started", "metrics"]
tags: ["aws", "metrics", "nlb"]
author: Lawrence Lane
---

## Collected
| Friendly Name          | FQN                                   | Statistic | Baseline | Correlation |
|------------------------|---------------------------------------|-----------|----------|-------------|
| Active Flow Count      | aws.networkelb.activeflowcount        | AVG       | yes      | no          |
| ELB Consumed ICUs      | aws.networkelb.consumedlcus           | MAX       | no       | no          |
| ELB Healthy Host Count | aws.networkelb.healthyhostcount       | MAX       | no       | no          |
| ELB New Flow Count     | aws.networkelb.newflowcount           | SUM       | yes      | no          |
| ELB Processed Bytes    | aws.networkelb.processedbytes         | SUM       | yes      | no          |
| TCP Client Reset Count | aws.networkelb.tcp_client_reset_count | SUM       | no       | no          |
| TCP ELB Reset Count    | aws.networkelb.tcp_elb_reset_count    | SUM       | no       | no          |
| TCP Target Reset Count | aws.networkelb.tcp_target_reset_count | SUM       | no       | no          |
| Unhealthy Host Count   | aws.networkelb.unhealthyhostcount     | MAX       | no       | no          |

## Computed
| Fully Qualified Name (FQN)          | Description            | Units   | BASE |
|-------------------------------------|------------------------|---------|------|
| aws.networkelb.unhealthyhostpercent | Unhealthy host percent | Percent | yes  |
