---
title: "Collectors"
date: 2018-11-30T16:08:13-05:00
draft: true
categories: ["integration", "admin guide", "getting started"]
tags: ["agents", "linux", "collectors" ]
author: Lawrence Lane
---

 There are three ways to configure the Linux Agent default collectors: via the _BaseCollector_, as a combination of _individual collectors_, or with just the _SimpleCollector_. This guide outlines their differences and how to use each; however, we encourage you to try the new SimpleCollector.

## Using the Simple Collector
`netuitive-diamond/src/collectors/simple`

 Where the base or individual collectors include more data (which may be less useful or actionable), this SimpleCollector guarantees a cleaner streamlined experience. The SimpleCollector can be activated by updating the ``/opt/netuitive-agent/conf/netuitive-agent.conf`` file.

![Linux Simple Collector](/images/LINUX-collectors/linux-simple-collector.png)

 The SimpleCollector collects a single metric for CPU, Mem, Disk I/O, and Disk Usage and is set to `FALSE` by default. It should not be used with any of the above collectors active. Here are the metrics collected by the SimpleCollector:

- **CPU**: `cpu.total.utilization.percent`
- **MEM**: `memory.utilizationpercent`
- **Disk I/O**: `iostat.max_util_percentage`
- **Disk Space**: `diskspace.avg_byte_percentused`

## Using the BaseCollector
`netuitive-diamond/src/collectors/base`

The BaseCollector is a compilation of all individual collectors bundled together and reports on all of their supported metrics. The base collector is set to `TRUE` by default and should not be used with any of the later mentioned diamond collectors active.

Collectors are turned on or off by updating the ``/opt/netuitive-agent/conf/netuitive-agent.conf`` file.

![Linux Base Collector](/images/LINUX-collectors/linux-base-collector.png)

## Using Individual Collectors
`netuitive-diamond/src/collectors/*``

Each individual collector can be turned on or off to get exactly what you want. Set to `FALSE` by default; should not be used with the base collector set to `TRUE`. These are the individual collectors:

- CPUCollector
- MemoryCollector
- LoadAverageCollector
- NetworkCollector
- DiskUsageCollector
- DiskSpaceCollector
- VMStatCollector

Some of the individual collectors have their own simple mode. This can be activated by  updating the ``/opt/netuitive-agent/conf/netuitive-agent.conf`` file.

![Linux Individual Collectors](/images/LINUX-collectors/linux-individual-collectors.png)

## Conf File Example

```
[[BaseCollector]]
-enabled = False
+enabled = True

 [[CPUCollector]]
 enabled = True
 simple = False
 percore = False
 include_cpu_pct = True

 [[DiskSpaceCollector]]
 enabled = True
 simple = True
 # exclude everything that begins /boot or /mnt
 exclude_filters = ^/boot, ^/mnt

 [[DiskUsageCollector]]
 enabled = True
 devices = (PhysicalDrive[0-9]+$|md[0-9]+$|sd[a-z]+$|x?vd[a-z]+$|disk[0-9]+$|dm\-[0-9]+$|nvme[0-9]+(n[0-9]+)(p[0-9]+)?$)
 metrics_whitelist = (?:^.*\.io$|^.*\.average_queue_length$|^.*\.await$|^.*\.iops$|^.*\.read_await$|^.*\.reads$|^.*\.util_percentage|^.*\.write_await$|^.*\.writes$)

 [[LoadAverageCollector]]
 enabled = True
 simple = False

 [[MemoryCollector]]
 enabled = True

 [[VMStatCollector]]
 enabled = True

 [[NetworkCollector]]
 enabled = True
 metrics_whitelist = (?:^.*\.rx_byte$|^.*\.rx_errors$|^.*\.tx_byte$|^.*\.tx_errors$)

 [[NetuitiveDockerCollector]]
 enabled = False
 ```

## Collector Options
| Collector  | Option                 | Default                                                                                                                                         | Description                                                                                                               |
|------------|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| VM Stat    | metrics_whitelist      | None                                                                                                                                            | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklist option.                                |
| VM Stat    | metrics_blacklist      | None                                                                                                                                            | Regex list to match metrics to block. Mutually exclusive with metrics_whitelist option.                                   |
| VM Stat    | measure_collector_time | FALSE                                                                                                                                           | Measure the collectorâ€™s run time in milliseconds.                                                                       |
| VM Stat    | enabled                | TRUE                                                                                                                                            | Enable collecting VM Stat metrics.                                                                                        |
| VM Stat    | byte_unit              | byte                                                                                                                                            | Default numeric output(s).                                                                                                |
| Network    | metrics_whitelist      | (?:^.*\.rx_byte$|^.*\.rx_errors$|^.*\.rx_packets$|^.*\.tx_byte$|^.*\.tx_errors$|^.*\.tx_packets$)                                               | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklist option.                                |
| Network    | metrics_blacklist      | None                                                                                                                                            | Regex list to match metrics to block. Mutually exclusive with metrics_whitelist option.                                   |
| Network    | measure_collector_time | FALSE                                                                                                                                           | Measure the collectorâ€™s run time in milliseconds.                                                                       |
| Network    | interfaces             | eth, bond, em, p1p, eno, enp, ens, enx                                                                                                          | List of interface types to collect.                                                                                       |
| Network    | greedy                 | FALSE                                                                                                                                           | Greedy match interfaces.                                                                                                  |
| Network    | enabled                | TRUE                                                                                                                                            | Enable collecting Memory metrics.                                                                                         |
| Network    | byte_unit              | bit, byte,                                                                                                                                      | Default numeric output(s).                                                                                                |
| Memory     | metrics_whitelist      | None                                                                                                                                            | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklist option.                                |
| Memory     | metrics_blacklist      | None                                                                                                                                            | Regex list to match metrics to block. Mutually exclusive with metrics_whitelist option.                                   |
| Memory     | measure_collector_time | FALSE                                                                                                                                           | Measure the collectorâ€™s run time in milliseconds.                                                                       |
| Memory     | enabled                | TRUE                                                                                                                                            | Enable collecting Memory metrics.                                                                                         |
| Memory     | detailed               | FALSE                                                                                                                                           | Set to True to collect all nodes.                                                                                         |
| Memory     | byte_unit              | byte                                                                                                                                            | Default numeric output(s).                                                                                                |
| Load Avg.  | simple                 | FALSE                                                                                                                                           | Reduces the amount of metrics collected to the bare minimum necessary.                                                    |
| Load Avg.  | metrics_whitelist      | None                                                                                                                                            | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklist option.                                |
| Load Avg.  | metrics_blacklist      | None                                                                                                                                            | Regex list to match metrics to block. Mutually exclusive with metrics_whitelist option.                                   |
| Load Avg.  | measure_collector_time | FALSE                                                                                                                                           | Measure the collectorâ€™s run time in milliseconds.                                                                       |
| Load Avg.  | enabled                | TRUE                                                                                                                                            | Enable collecting Load Average metrics.                                                                                   |
| Load Avg.  | byte_unit              | byte                                                                                                                                            | Default numeric output(s).                                                                                                |
| Heartbeat  | path                   | metricly                                                                                                                                        | Path to the Metricly agent.                                                                                               |
| Heartbeat  | enabled                | TRUE                                                                                                                                            | Enable collected the Heartbeat metric.                                                                                    |
| Disk Usage | send_zero              | FALSE                                                                                                                                           | Tells the collector to send IO data even when there is no IO.                                                             |
| Disk Usage | sector_size            | 512                                                                                                                                             | The size used to calculate sector usage.                                                                                  |
| Disk Usage | metrics_whitelist      | (?:^.*\.io$|^.*\.average_queue_length$|^.*\.await$|^.*\.iops$|^.*\.read_await$|^.*\.reads$|^.*\.util_percentage|^.*\.write_await$|^.*\.writes$) | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklist option.                                |
| Disk Usage | metrics_blacklist      | None                                                                                                                                            | Regex list to match metrics to block. Mutually exclusive with metrics_whitelist option.                                   |
| Disk Usage | measure_collector_time | FALSE                                                                                                                                           | Measure the collectorâ€™s run time in milliseconds.                                                                       |
| Disk Usage | enabled                | TRUE                                                                                                                                            | Enable collecting Disk Usage metrics.                                                                                     |
| Disk Usage | devices                | None                                                                                                                                            | Regex pattern to determine which device metrics to collect.                                                               |
| Disk Usage | byte_unit              | byte                                                                                                                                            | Default numeric output(s).                                                                                                |
| Disk Space | simple                 | TRUE                                                                                                                                            | Reduces the amount of metrics collected to the bare minimum necessary. Switching simpleto False will allow inode metrics. |
| Disk Space | metrics_whitelist      | None                                                                                                                                            | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklist option.                                |
| Disk Space | metrics_blacklist      | None                                                                                                                                            | Regex list to match metrics to block. Mutually exclusive with metrics_whitelist option.                                   |
| Disk Space | measure_collector_time | FALSE                                                                                                                                           | Measure the collectorâ€™s run time in milliseconds.                                                                       |
| Disk Space | filesystems            | None                                                                                                                                            | Types of filesystems to examine.                                                                                          |
| Disk Space | exclude_filters        | ^/boot, ^/mnt                                                                                                                                   | A list of regex patterns to exclude from collection.                                                                      |
| Disk Space | enabled                | TRUE                                                                                                                                            | Enable collecting Diskspace metrics.                                                                                      |
| Disk Space | byte_unit              | byte                                                                                                                                            | Default numeric output(s).                                                                                                |
| CPU        | include_cpu_pct        | TRUE                                                                                                                                            | Includes the CPU percentage metric in collection.                                                                         |
| CPU        | simple                 | FALSE                                                                                                                                           | Enable returning only the aggregate CPU percentage metric.                                                                |
| CPU        | percore                | FALSE                                                                                                                                           | Enable collecting metrics per CPU core or just the total of the cores.                                                    |
| CPU        | normalize              | FALSE                                                                                                                                           | Enable dividing by the number CPUs for CPU totals.                                                                        |
| CPU        | metrics_whitelist      | None                                                                                                                                            | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklist option.                                |
| CPU        | metrics_blacklist      | None                                                                                                                                            | Regex list to match metrics to block. Mutually exclusive with metrics_whitelist option.                                   |
| CPU        | measure_collector_time | FALSE                                                                                                                                           | Measure the collectorâ€™s run time in milliseconds.                                                                       |
| CPU        | enabled                | TRUE                                                                                                                                            | Enable collecting CPU metrics.                                                                                            |
| CPU        | byte_unit              | byte                                                                                                                                            | Default numeric output(s).                                                                                                |
| CPU        | byte_unit              | byte                                                                                                                                            | Default numeric output(s).                                                                                                |
| CPU        | enabled                | TRUE                                                                                                                                            | Enable collecting CPU metrics.                                                                                            |
| CPU        | measure_collector_time | FALSE                                                                                                                                           | Measure the collectorâ€™s run time in milliseconds.                                                                       |
| CPU        | include_cpu_pct        | TRUE                                                                                                                                            | Includes the CPU percentage metric in collection.                                                                         |
| Disk Space | byte_unit              | byte                                                                                                                                            | Default numeric output(s).                                                                                                |
| Disk Usage | byte_unit              | byte                                                                                                                                            | Default numeric output(s).                                                                                                |
| Heartbeat  | enabled                | TRUE                                                                                                                                            | Enable collected the Heartbeat metric.                                                                                    |
| Load Avg.  | byte_unit              | byte                                                                                                                                            | Default numeric output(s).                                                                                                |
| Memory     | byte_unit              | byte                                                                                                                                            | Default numeric output(s).                                                                                                |
| Network    | byte_unit              | bit, byte,                                                                                                                                      | Default numeric output(s).                                                                                                |
| VM Stat    | byte_unit              | byte                                                                                                                                            | Default numeric output(s).                                                                                                |
