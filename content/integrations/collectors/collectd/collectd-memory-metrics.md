---
title: "Memory Metrics"
date: 2018-12-11
draft: false
tags: ["collectd", "integrations", "metrics", "memory", "collectors" ]
author: Lawrence Lane
---

## Collected
| Fully Qualified Name(FQN)    | Description                                                                                                     | Statistic | Units | Min | Max  | Sparse Data Strategy(SDS) | BASE | CORR | UTIL |
|------------------------------|-----------------------------------------------------------------------------------------------------------------|-----------|-------|-----|------|---------------------------|------|------|------|
| memory.memory-buffered.value | Memory being used by buffers; this memory is available to be freed forapplications to use, should they need it. | average   | bytes | 0   | none | none                      | yes  | no   | no   |
| memory.memory-cached.value   | Memory being used by caches; this memory is available to be freed forapplications to use, should they need it.  | average   | bytes | 0   | none | none                      | yes  | no   | no   |
| memory.memory-free.value     | Memory not being used.                                                                                          | average   | bytes | 0   | none | none                      | yes  | no   | no   |
| memory.memory-used.value     | Memory being used by applications.                                                                              | average   | bytes | 0   | none | none                      | yes  | no   | no   |

## Computed
| Fully Qualified Name(FQN)                   | Description                                                                                                                                                                                                                         | Statistic | Units   | Min | Max  | BASE | CORR | UTIL |
|---------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|---------|-----|------|------|------|------|
| metricly.collectd.memory.total              | **Computation**: memory.memory-buffered + memory.memory-cached + memory.memory-free +memory.memory-used                                                                                                                                  | average   | bytes   | 0   | none | no   | no   | no   |
| metricly.collectd.memory.utilizationpercent | Under Linux, memory buffered and cached are part of memory which can beconsidered free. See the following explanation . **Computation**: 100 – ((memory.memory-buffered + memory.memory-cached +memory.memory-free / Total Memory) * 100) | average   | percent | 0   | 100  | yes  | yes  | yes  |
