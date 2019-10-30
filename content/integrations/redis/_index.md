---
title: "Redis"
#date: 2018-12-12
draft: false
tags: ["#redis", "#integrations" ]
author: Lawrence Lane
---
Redis is an adaptable, open source, in-memory data structure store that can be used as a database, cache, and message broker. CloudWisdom can be used to monitor the performance of your Redis server.

## Prerequisites
- [Linux Agent][1]


## Configure

1. Navigate to the **collectors** folder, `/opt/netuitive-agent/conf/collectors`.
2. Open the **RedisCollector.conf** file.
3. Change the **enabled** setting to `True`.
4. Update the **instances** setting to contain any number of Redis instances you want to monitor as long as it follows the format `hostname:port`.
5. **Save** the configuration file and **restart** the Linux Agent.



## Collector Options

| Option                 | Default                                      | Description                                                                                                                                              |
|------------------------|----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| enabled                | FALSE                                        | Enable collecting RabbitMQ metrics.                                                                                                                      |
| host                   | 127.0.0.1:15672                              | Hostname and port to collect from.                                                                                                                       |
| user                   | guest                                        | User name authentication for RabbitMQ.                                                                                                                   |
| password               | guest                                        | Password authentication for RabbitMQ.                                                                                                                    |
| replace_dot            | ‘_’                                          | A value to replace the “.” in queue names and vhosts names. This option helps CloudWisdom’s metadata usage if you use dots in your queue naming convention. |
| cluster                | TRUE                                         | If this node is part of a cluster, the collector will collect metrics on the cluster health.                                                             |
| metrics_blacklist      | “(.*-test__[abc]-.*)|(rabbitmq\.queues\..*)” | Regex list to match metrics to block. Mutually exclusive with metrics_whitelist option.                                                                  |
| byte_unit              |                                              | Default numeric output(s).                                                                                                                               |
| measure_collector_time |                                              | Measure the collector’s run time in milliseconds.                                                                                                        |
| metrics_whitelist      |                                              | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklist option.                                                               |
| queues                 |                                              | List of queues to publish. Leave empty to publish all.                                                                                                   |
| queues_ignored         |                                              | A list of queues or regexes for queue names not to report on.                                                                                            |
| vhosts                 |                                              | A list of vhosts and queues to collect.                                                                                                                  |


[1]: /integrations/agents/linux-agent
