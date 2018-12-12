---
title: "RabbitMQ Policies"
date: 2018-04-12
draft: false
categories:
tags: ["alerts", "notifications", "policies", "default policies", "rabbitMQ"]
author: Lawrence Lane
---

{{% notice info %}}
Policy names are prefixed with **RabbitMQ –**
{{% /notice %}}

| Policy name                      | Duration | Conditions                                                                         | Category | Description                                                                                             |
|----------------------------------|----------|------------------------------------------------------------------------------------|----------|---------------------------------------------------------------------------------------------------------|
| Depressed Message Count          | 30 min   | rabbitmq.queue_totals.messages has a lower baseline deviation                      | WARNING  | The number of messages across all queues has been lower than expected for at least the past 30 minutes. |
| Elevated Memory Usage            | 30 min   | rabbitmq.health.mem_used has an upper baseline deviation                           | WARNING  | Memory usage has been higher than expected for at least the past 30 minutes.                            |
| Elevated Message Count           | 30 min   | rabbitmq.queue_totals.messages has an upper baseline deviation                     | WARNING  | The number of messages across all queues has been higher than expectedfor at least the past 30 minutes. |
| Exceeded Disk Free Limit         | 5 min    | rabbitmq.health.disk_free has a metric threshold < rabbitmq.health.disk_free_limit | CRITICAL | Free disk space has dropped below the configured disk free space limit.                                 |
| Exceeded Memory Limit            | 5 min    | rabbitmq.health.mem_used has a metric threshold < rabbitmq.health.mem_limit        | CRITICAL | Memory utilization has exceeded the configured memory limit.                                            |
| Memory Usage Approaching Limit   | 5 min    | metricly.aws.elb.unhealthyhostpercenthas a static threshold = 90%                  | WARNING  | Memory utilization has reached 90% of the configured limit.                                             |
| Unexpectedly Low Free Disk Space | 30 min   | rabbitmq.health.disk_free has an lower baseline deviation                          | WARNING  | Free disk space on the RabbitMQ node has been lower than expected for at least the past 30 minutes.     |
