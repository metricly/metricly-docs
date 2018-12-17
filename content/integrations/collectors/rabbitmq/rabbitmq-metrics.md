---
title: "Metrics"
#date: 2018-12-12
draft: false
tags: ["rabbitmq", "integrations", "metrics" ]
author: Lawrence Lane
---

## Collected

| Fully Qualified Name (FQN)                                 | Type    | Units | Statistic | Min  | Max  | Sparse Data Strategy (SDS) | BASE | CORR | UTIL |
|------------------------------------------------------------|---------|-------|-----------|------|------|----------------------------|------|------|------|
| rabbitmq.cluster.nodes                                     | GAUGE   | count | average   | 0    | none | none                       | no   | no   | no   |
| rabbitmq.cluster.partitions                                | GAUGE   | count | average   | 0    | none | none                       | no   | no   | no   |
| rabbitmq.health.disk_free                                  | GAUGE   | bytes | average   | 0    | none | none                       | yes  | no   | no   |
| rabbitmq.health.disk_free_limit                            | GAUGE   | bytes | average   | 0    | none | none                       | no   | no   | no   |
| rabbitmq.health.fd_total                                   | GAUGE   | count | average   | 0    | none | none                       | no   | no   | no   |
| rabbitmq.health.fd_used                                    | GAUGE   | count | average   | 0    | none | none                       | yes  | no   | no   |
| rabbitmq.health.mem_limit                                  | GAUGE   | bytes | average   | 0    | none | none                       | no   | no   | no   |
| rabbitmq.health.mem_used                                   | GAUGE   | bytes | average   | 0    | none | none                       | yes  | no   | no   |
| rabbitmq.health.proc_total                                 | GAUGE   | count | average   | 0    | none | none                       | no   | no   | no   |
| rabbitmq.health.proc_used                                  | GAUGE   | count | average   | 0    | none | none                       | yes  | no   | no   |
| rabbitmq.health.sockets_total                              | GAUGE   | count | average   | 0    | none | none                       | no   | no   | no   |
| rabbitmq.health.sockets_used                               | GAUGE   | count | average   | 0    | none | none                       | yes  | no   | no   |
| rabbitmq.message_stats.ack                                 | COUNTER | count |           | 0    | none | none                       | yes  | no   | no   |
| rabbitmq.message_stats.ack_details.rate                    | GAUGE   | ops   | average   | none | none | none                       | yes  | no   | no   |
| rabbitmq.message_stats.deliver                             | COUNTER | count |           | 0    | none | none                       | yes  | no   | no   |
| rabbitmq.message_stats.deliver_details.rate                | GAUGE   | ops   | average   | none | none | none                       | yes  | no   | no   |
| rabbitmq.message_stats.deliver_get                         | COUNTER | count |           | 0    | none | none                       | yes  | no   | no   |
| rabbitmq.message_stats.deliver_get_details.rate            | GAUGE   | ops   | average   | none | none | none                       | yes  | no   | no   |
| rabbitmq.message_stats.publish                             | COUNTER | count |           | 0    | none | none                       | yes  | no   | no   |
| rabbitmq.message_stats.publish_details.rate                | GAUGE   | ops   | average   | none | none | none                       | yes  | no   | no   |
| rabbitmq.message_stats.redeliver                           | COUNTER | count |           | 0    | none | none                       | no   | no   | no   |
| rabbitmq.message_stats.redeliver_details.rate              | GAUGE   | ops   | average   | none | none | none                       | no   | no   | no   |
| rabbitmq.object_totals.channels                            | GAUGE   | count | average   | 0    | none | none                       | no   | no   | no   |
| rabbitmq.object_totals.connections                         | GAUGE   | count | average   | 0    | none | none                       | no   | no   | no   |
| rabbitmq.object_totals.consumers                           | GAUGE   | count | average   | 0    | none | none                       | no   | no   | no   |
| rabbitmq.object_totals.exchanges                           | GAUGE   | count | average   | 0    | none | none                       | no   | no   | no   |
| rabbitmq.object_totals.queues                              | GAUGE   | count | average   | 0    | none | none                       | no   | no   | no   |
| rabbitmq.queue_totals.messages                             | GAUGE   | count | average   | 0    | none | none                       | yes  | no   | no   |
| rabbitmq.queue_totals.messages_details.rate                | GAUGE   | ops   | average   | none | none | none                       | yes  | no   | no   |
| rabbitmq.queue_totals.messages_ready                       | GAUGE   | count | average   | 0    | none | none                       | no   | no   | no   |
| rabbitmq.queue_totals.messages_ready_details.rate          | GAUGE   | ops   | average   | none | none | none                       | no   | no   | no   |
| rabbitmq.queue_totals.messages_unacknowledged              | GAUGE   | count | average   | 0    | none | none                       | yes  | no   | no   |
| rabbitmq.queue_totals.messages_unacknowledged_details.rate | GAUGE   | ops   | average   | none | none | none                       | yes  | no   | no   |
| rabbitmq.health.running                                    | GAUGE   | none  | minimum   | none | none | none                       | no   | no   | no   |

## Computed

| Fully Qualified Name (FQN)                                | Description                                                                                                                                             | Units   | Min | Max | BASE | CORR | UTIL |
|-----------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|---------|-----|-----|------|------|------|
| metricly.linux.rabbitmq.health.fd_utilization_percent     | The percentage of available file descriptors in use.Computation:rabbitmq.health.fd_used / rabbitmq.health.fd_total * 100                                | percent | 0   | 100 | yes  | no   | yes  |
| metricly.linux.rabbitmq.health.mem_utilization_percent    | The percentage of memory in use as a function of the defined memorylimit.Computation:100 – (rabbitmq.health.mem_used / rabbitmq.health.mem_limit * 100) | percent | 0   | 100 | yes  | no   | yes  |
| metricly.linux.rabbitmq.health.proc_utilization_percent   | The percentage of the allowed number of processes which are being run.Computation:rabbitmq.health.proc_used / rabbitmq.health.proc_total * 100          | percent | 0   | 100 | yes  | no   | yes  |
| metricly.linux.rabbitmq.health.socket_utilization_percent | The percentage of the available sockets in use.Computation:rabbitmq.health.sockets_used / rabbitmq.health.sockets_total * 100                           | percent | 0   | 100 | yes  | no   | yes  |
