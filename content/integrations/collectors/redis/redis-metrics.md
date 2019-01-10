---
title: "Metrics"
#date: 2018-12-12
draft: false
tags: ["#redis", "#integrations", "#metrics" ]
author: Lawrence Lane
---

## Collected

| Fully Qualified Name (FQN)   | Friendly Name                          |
|------------------------------|----------------------------------------|
| clients.blocked              | Blocked Clients                        |
| clients.connected            | Connected Clients                      |
| clients.longest_output_list  | Client Longest Output List             |
| cpu.parent.sys               | Used System CPU                        |
| cpu.children.sys             | Used System CPU (Children)             |
| cpu.parent.user              | Used CPU User                          |
| cpu.children.user            | Used CPU User (Children)               |
| hash_max_zipmap.entries      | Maximum Hash Zipmap Entries            |
| hash_max_zipmap.value        | Maximum Hash Zipmap Value              |
| keys.evicted                 | Evicted Keys                           |
| keys.expired                 | Expired Keys                           |
| keyspace.hits                | Keyspace Hits                          |
| keyspace.misses              | Keyspace Misses                        |
| last_save.changes_since      | Changes Since Last Save                |
| last_save.time               | Last Save Time                         |
| memory.internal_view         | Memory Used                            |
| memory.external_view         | Memory Used (Resident Set Size)        |
| memory.fragmentation_ratio   | Memory Fragmentation Ratio             |
| process.commands_processed   | Total Commands Processed               |
| process.connections_received | Total Connections Received             |
| process.uptime               | Process Uptime (in Seconds)            |
| pubsub.channels              | Publish/Subscribe Channels             |
| pubsub.patterns              | Publish/Subscribe Patterns             |
| slaves.connected             | Connected Slaves                       |
| slaves.last_io               | Master Last Input/Output (Seconds Ago) |
