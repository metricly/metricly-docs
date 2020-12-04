---
title: "Diamond CPU Metrics"
#date: 2018-12-11
draft: false
tags: ["diamond", "integrations", "agents", "cpu" ]
author: Lawrence Lane
---
## Collected
| Fully Qualified Name(FQN) | Description                                                                                       | Statistic | Units   | Min | Max  | Sparse Data Strategy (SDS) | BASE | CORR | UTIL |
|---------------------------|---------------------------------------------------------------------------------------------------|-----------|---------|-----|------|----------------------------|------|------|------|
| cpu.total.guest           | Percentage of CPU spent running virtual CPUs for guest operatingsystems.                          | average   | percent | 0   | none | none                       | yes  | no   | no   |
| cpu.total.guest_nice      | Percentage of CPU spent running low-priority virtual CPUs for guestoperating systems.             | average   | percent | 0   | none | none                       | yes  | no   | no   |
| cpu.total.idle            | Percentage of CPU not doing any work.                                                             | average   | percent | 0   | none | none                       | yes  | no   | no   |
| cpu.total.iowait          | Percentage of CPU time spent waiting for I/O to complete.                                         | average   | percent | 0   | none | none                       | yes  | no   | no   |
| cpu.total.irq             | Percentage of CPU time spent processing hardware interrupts.                                      | average   | percent | 0   | none | none                       | yes  | no   | no   |
| cpu.total.nice            | Percentage of CPU spent running user processes at low priority.                                   | average   | percent | 0   | none | none                       | yes  | no   | no   |
| cpu.total.softirq         | Percentage of CPU time spent processing software interrupts.                                      | average   | percent | 0   | none | none                       | yes  | no   | no   |
| cpu.total.steal           | Percentage of CPU time spent in other operating systems when running ina virtualized environment. | average   | percent | 0   | none | none                       | yes  | no   | no   |
| cpu.total.system          | Percentage of CPU spent running system processes.                                                 | average   | percent | 0   | none | none                       | yes  | no   | no   |
| cpu.total.user            | Percentage of CPU spent running user processes.                                                   | average   | percent | 0   | none | none                       | yes  | no   | no   |

## Computed

| Fully Qualified Name(FQN)   | Description | Units   | Min | Max | BASE | CORR | UTIL |
|----|--------------|---------|-----|-----|------|------|------|
| netuitive.linux.cpu.total.utilization.percent | The overall average CPU Utilization across all CPUs. This is anormalized metric. **Computation**: (data[‘cpu.total.idle’] != null && data[‘cpu.total.idle’].actual!= null) ? ((data.sum(‘cpu.total.*’) – data[‘cpu.total.idle’].actual) /data.sum(‘cpu.total.*’)) * 100 : data[‘cpu.cpu0.idle’] != null ?((data.sum(‘cpu[.].*’) – data.sum(‘cpu[.].*.idle’)) /data.sum(‘cpu[.].*’)) * 100 : null | percent | 0   | 100 | yes  | yes  | yes  |
| netuitive.linux.cpu.total.normalized.user  | Percentage of CPU spent running user processes. This is a normalizedmetric. **Computation**: attribute[‘cpus’] == null ? null : data[‘cpu.total.user’] /attribute[‘cpus’].value | percent | 0   | 100 | yes  | yes  | no   |
| netuitive.linux.cpu.total.normalized.system   | Percentage of CPU spent running system processes. This is a normalizedmetric. **Computation**: attribute[‘cpus’] == null ? null : data[‘cpu.total.system’] /attribute[‘cpus’].value   | percent | 0   | 100 | yes  | yes  | no   |
