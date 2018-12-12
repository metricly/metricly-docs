---
title: "Load Average Metrics"
date: 2018-12-11
draft: true
tags: ["diamond", "integrations", "agents", "load average" ]
author: Lawrence Lane
---

## Computed
| Fully Qualified Name(FQN)                | Description                                                                                                                                                                           | Units | Min | Max  | BASE | CORR | UTIL |
|------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------|-----|------|------|------|------|
| metriclyicly.linux.loadavg.01.normalized | The is the average run queue size over the past minute, normalizedacross CPUs. **Computation**: attribute[‘cpus’] == null ? null : (data[‘loadavg.01’].actual /attribute[‘cpus’].value)     |       | 0   | none | yes  | no   | no   |
| metriclyicly.linux.loadavg.05.normalized | The is the average run queue size over the past 5 minutes, normalizedacross CPUs. **Computation**: attribute[‘cpus’] == null ? null : (data[‘loadavg.05’].actual /attribute[‘cpus’].value)  |       | 0   | none | yes  | yes  | no   |
| metriclyicly.linux.loadavg.15.normalized | The is the average run queue size over the past 15 minutes, normalizedacross CPUs. **Computation**: attribute[‘cpus’] == null ? null : (data[‘loadavg.15’].actual /attribute[‘cpus’].value) |       | 0   | none | yes  | no   | no   |
