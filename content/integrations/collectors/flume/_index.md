---
title: "Flume"
#date: 2018-12-11
draft: false
tags: ["flume", "integrations", "collectors" ]
author: Lawrence Lane
---
Flume collects and aggregates all of your log files distributed across your environment. Metricly can be used to monitor the performance of your Flume service.

## Configuration
1. Navigate to the **collectors** folder, `/opt/netuitive-agent/conf/collectors`.
2. Open the `FlumeCollector.conf` file.
3. Change the **enabled** setting to `True`.
4. Update the `req_host`, `req_port`, and/or `req_path` settings as necessary.
5. **Save** the configuration file and **restart** the Linux Agent.

## Collector Options

| Option                 | Default   | Description                                                                                |
|------------------------|-----------|--------------------------------------------------------------------------------------------|
| enabled                | FALSE     | Enable collecting Flume metrics.                                                           |
| req_host               | localhost | Hostname to collect from.                                                                  |
| req_port               | 41414     | Port to collect from.                                                                      |
| req_path               | /metrics  | File path to your Flume service.                                                           |
| byte_unit              |           | Default numeric output(s).                                                                 |
| measure_collector_time |           | Measure the collector’s run time in milliseconds.                                          |
| metrics_blacklist      |           | Regex list to match metrics to block. Mutually exclusive with metrics_whitelist option.    |
| metrics_whitelist      |           | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklist option. |
