---
title: "Docker Memory Metrics"
#date: 2018-12-11
draft: false
tags: ["#docker", "#integrations", "#metrics", "#memory"]
author: Lawrence Lane
---

## Collected

| Fully Qualified Name(FQN)             | Type    | Units | Statistic* | BASE | CORR | Description                                                                                                                |
|---------------------------------------|---------|-------|------------|------|------|----------------------------------------------------------------------------------------------------------------------------|
| memory.failcnt                        | GAUGE   | count | average    | no   | no   | A count of the number of times that the container requested memory and failed to obtain it. This value should always be 0. |
| memory.limit                          | GAUGE   | bytes | average    | no   | no   | The total amount of memory available to the container.                                                                     |
| memory.max_usage                      | GAUGE   | bytes | average    | no   | no   | The maxiumum amount of memory the container has ever used.                                                                 |
| memory.stats.active_anon              | GAUGE   | bytes | average    | no   | no   |                                                                                                                            |
| memory.stats.active_file              | GAUGE   | bytes | average    | no   | no   |                                                                                                                            |
| memory.stats.cache                    | GAUGE   | bytes | average    | no   | no   |                                                                                                                            |
| memory.stats.hierarchical_memory_lmit | GAUGE   | bytes | average    | no   | no   |                                                                                                                            |
| memory.stats.hierarchical_memsw_limit | GAUGE   | bytes | average    | no   | no   |                                                                                                                            |
| memory.stats.inactive_anon            | GAUGE   | bytes | average    | no   | no   |                                                                                                                            |
| memory,stats.inactive_file            | GAUGE   | bytes | average    | no   | no   |                                                                                                                            |
| memory.stats.mapped_file              | GAUGE   | bytes | average    | no   | no   |                                                                                                                            |
| memory.stats.pgpgin                   | COUNTER | bytes |            | yes  | no   |                                                                                                                            |
| memory.stats.pgpgout                  | COUNTER | bytes |            | yes  | no   |                                                                                                                            |
| memory.stats.rss                      | GAUGE   | bytes | average    | yes  | no   |                                                                                                                            |
| memory.stats.swap                     | GAUGE   | bytes | average    | no   | no   |                                                                                                                            |
| memory.stats.total_active_anon        | GAUGE   | bytes | average    | yes  | no   |                                                                                                                            |
| memory.stats.total_active_file        | GAUGE   | bytes | average    | no   | no   |                                                                                                                            |
| memory.stats_total_cache              | GAUGE   | bytes | average    | no   | no   |                                                                                                                            |
| memory.stats.total_inactive_anon      | GAUGE   | bytes | average    | no   | no   |                                                                                                                            |
| memory.stats.total_inactive_file      | GAUGE   | bytes | average    | no   | no   |                                                                                                                            |
| memory.stats.total_mapped_file        | GAUGE   | bytes | average    | no   | no   |                                                                                                                            |
| memory.stats.total_pgpgin             | COUNTER | bytes |            | yes  | no   |                                                                                                                            |
| memory.stats.total_pgpgout            | COUNTER | bytes |            | yes  | no   |                                                                                                                            |
| memory.stats.total_rss                | GAUGE   | bytes | average    | yes  | no   |                                                                                                                            |
| memory.stats.total_swap               | GAUGE   | bytes | average    | no   | no   |                                                                                                                            |
| memory.stats.total_unevictable        | GAUGE   | bytes | average    | no   | no   |                                                                                                                            |
| memory.stats.unevictable              | GAUGE   | bytes | average    | no   | no   |                                                                                                                            |
| memory.usage                          | GAUGE   | bytes | average    | yes  | no   | The amount of memory currently being used by the container.                                                                |
