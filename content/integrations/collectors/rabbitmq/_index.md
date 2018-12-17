---
title: "rabbitMQ"
#date: 2018-12-12
draft: false
tags: ["rabbitmq", "integrations" ]
author: Lawrence Lane
---
Rabbit MQ is a message broker that manages queues between message producers and consumers. Metricly can be used to monitor your RabbitMQ server’s queuing performance.

## Prerequisites
- [Linux Agent][1]

Before editing the configuration file, you should verify the RabbitMQ management module is enabled. If the module is not enabled, do the following:

- If the package is installed globally, type this into your command prompt:
```
rabbitmq-plugins enable rabbitmq_management
```

- If the package is installed in a directory, type this into your command prompt instead:
```
/usr/lib/rabbitmq/bin/rabbitmq-plugins enable rabbitmq_management
```

## Configure

1. Navigate to the **collectors** folder, `/opt/netuitive-agent/conf/collectors`.
2. Open the **RabbitMQCollector.conf** file.
3. Change the **enabled** setting to `True`.
4. Replace the default host address and/or port number if necessary.
5. Replace the `user` and `password` settings with the appropriate values.
6. Optionally, **change** the cluster value to `false` if you aren’t using a cluster or do not wish to collect several additional cluster metrics.
7. **Save** the file and **restart** the Linux Agent.

## Collector Options

| Option                 | Default                                      | Description                                                                                                                                              |
|------------------------|----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| enabled                | FALSE                                        | Enable collecting RabbitMQ metrics.                                                                                                                      |
| host                   | 127.0.0.1:15672                              | Hostname and port to collect from.                                                                                                                       |
| user                   | guest                                        | User name authentication for RabbitMQ.                                                                                                                   |
| password               | guest                                        | Password authentication for RabbitMQ.                                                                                                                    |
| replace_dot            | ‘_’                                          | A value to replace the “.” in queue names and vhosts names. This option helps Metricly’s metadata usage if you use dots in your queue naming convention. |
| cluster                | TRUE                                         | If this node is part of a cluster, the collector will collect metrics on the cluster health.                                                             |
| metrics_blacklist      | “(.*-test__[abc]-.*)|(rabbitmq\.queues\..*)” | Regex list to match metrics to block. Mutually exclusive with metrics_whitelist option.                                                                  |
| byte_unit              |                                              | Default numeric output(s).                                                                                                                               |
| measure_collector_time |                                              | Measure the collector’s run time in milliseconds.                                                                                                        |
| metrics_whitelist      |                                              | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklist option.                                                               |
| queues                 |                                              | List of queues to publish. Leave empty to publish all.                                                                                                   |
| queues_ignored         |                                              | A list of queues or regexes for queue names not to report on.                                                                                            |
| vhosts                 |                                              | A list of vhosts and queues to collect.                                                                                                                  |


[1]: /integrations/agents/linux-agent
