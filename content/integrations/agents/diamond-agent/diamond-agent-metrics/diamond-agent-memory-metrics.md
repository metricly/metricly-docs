---
title: "Memory Metrics"
date: 2018-12-11
draft: false
tags: ["diamond", "integrations", "agents", "memory" ]
author: Lawrence Lane
---

## Computed
| Fully Qualified Name(FQN)                    | Description                                                                                                                                                                                                            | Units   | Min | Max | BASE | CORR | UTIL |
|----------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|-----|-----|------|------|------|
| metriclyicly.linux.memory.utilizationpercent | Under Linux, memory buffered and cached are part of memory which can beconsidered available. See the following explanation . **Computation**: 100 – (memory.Buffers + memory.Cached + memory.MemFree) /memory.MemTotal * 100 | percent | 0   | 100 | yes  | yes  | yes  |
