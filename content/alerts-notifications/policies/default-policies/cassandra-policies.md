---
title: "Cassandra Policies"
date: 2018-04-12
draft: false
categories:
tags: ["alerts", "notifications", "policies", "default policies", "cassandra",]
author: Lawrence Lane
---

| Policy name                                  | Duration | Conditions                                                                                   | Category | Description                                                                                                                                                                                     |
|----------------------------------------------|----------|----------------------------------------------------------------------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Depressed Key Cache Hit Rate                 | 30 min   | cassandra.Cache.KeyCache.HitRate has an lower baseline deviation + a static threshold ≤ 0.85 | WARNING  | The hit rate for the key cache is lower than expected and is less than 85%. This condition has been persisting for at least the past 30 minutes.                                                |
| Elevated Node Read Latency                   | 30 min   | cassandra.Keyspace.ReadLatency.OneMinuteRate has an upper baseline deviation                 | WARNING  | The overall keyspace read latency on this Cassandra node has been higher than expected for at least 30 minutes.                                                                                 |
| Elevated Node Write Latency                  | 30 min   | cassandra.Keyspace.WriteLatency.OneMinuteRate has an upper baseline deviation                | WARNING  | The overall keyspace write latency on this Cassandra node has been higher than expected for at least 30 minutes.                                                                                |
| Elevated Number of Pending Compaction Tasks  | 15 min   | cassandra.Compaction.PendingTasks has an upper baseline deviation                            | WARNING  | The number of pending compaction tasks has been higher than expected for at least the past 15 minutes. This could indicate that the node is falling behind on compaction tasks.                 |
| Elevated Number of Pending Thread Pool Tasks | 15 min   | cassandra.ThreadPools.*.PendingTasks has an upper baseline deviation                         | WARNING  | For at least the past 15 minutes, the number of pending tasks for one or more thread pools has been higher than expected. This could indicate that the pools are falling behind on their tasks. |
| Unavailable Exceptions Greater Than Zero     | 5 min    | cassandra.*Unavailables.OneMinuteRate has a static threshold ≤1                              | CRITICAL | The required number of nodes were unavailable for one or more requests.                                                                                                                         |
