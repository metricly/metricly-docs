---
title: "Docker Collectors"
#date: 2018-12-11
draft: false
tags: ["#docker", "#integrations", "#collectors"]
author: Lawrence Lane
---
There are three Docker Agent collector modes: Simple Mode, Minimal Mode, and Standard mode. Minimal Mode is enabled by default. You can activate different collector modes from the `/opt/netuitive-agent/conf/netuitive-agent.conf` file.

![docker-agent-conf-file](/images/docker-collectors/docker-agent-conf-file.png)

## Minimal Mode (Default)

### Metrics Collected - Computed Only

| Name                     | FQN                                           | Computation                                                                                                                         | Units   | Min | Max | BASE | CORR | Description                                                                                            |
|--------------------------|-----------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|---------|-----|-----|------|------|--------------------------------------------------------------------------------------------------------|
| Container CPU Percent    | netuitive.docker.cpu.container_cpu_percent    | data[‘cpu.system_cpu_usage’].actual == 0 ? 0 :(data[‘cpu.cpu_usage.total_usage’].actual /data[‘cpu.system_cpu_usage’].actual) * 100 | percent | 0   | 100 | yes  | yes  | The percentage of total CPU being used by the container.                                               |
| Container Memory Percent | netuitive.docker.cpu.container_memory_percent | (data[‘memory.usage’].actual / data[‘memory.limit’].actual) * 100                                                                   | percent | 0   | 100 | yes  | yes  | The amount of memory in use by the container, expressed as a percentage of the memory available to it. |

## Simple Mode

### Metrics Collected

#### Computed
| Name                         | FQN                                               | Computation                                                                                                                                                   | Units   | Min | Max | BASE | CORR | Description                                                                                            |
|------------------------------|---------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|-----|-----|------|------|--------------------------------------------------------------------------------------------------------|
| Container CPU Percent        | netuitive.docker.cpu.container_cpu_percent        | data[‘cpu.system_cpu_usage’].actual == 0 ? 0 :(data[‘cpu.cpu_usage.total_usage’].actual /data[‘cpu.system_cpu_usage’].actual) * 100                           | percent | 0   | 100 | yes  | yes  | The percentage of total CPU being used by the container.                                               |
| Container Memory Percent     | netuitive.docker.cpu.container_memory_percent     | (data[‘memory.usage’].actual / data[‘memory.limit’].actual) * 100                                                                                             | percent | 0   | 100 | yes  | yes  | The amount of memory in use by the container, expressed as a percentage of the memory available to it. |
| Container Throttling Percent | netuitive.docker.cpu.container_throttling_percent | data[‘cpu.throttling_data.periods’].actual == 0 ? 0 :(data[‘cpu.throttling_data.throttled_periods’].actual /data[‘cpu.throttling_data.periods’].actual) * 100 | percent | 0   | 100 | yes  | yes  | The percentage of periods that the container spent having its CPU usage throttled.                     |

#### CPU

| Fully Qualified Name(FQN) | Type | Units | Statistic* | BASE | CORR | Description |
|---------------------------------------|---------|-------------|------------|------|------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| cpu.cpu_usage.percpu_usage* | COUNTER | nanoseconds |  | yes | no | Each CPU has a separate metric which tracks the number of nanoseconds that that specific CPU has been used since the container was started. |
| cpu.cpu_usage.total_usage | COUNTER | nanoseconds |  | yes | no | This metric is the sum of all of the per-CPU usage metrics. Thus, it represents the total number of nanoseconds that all CPUs have been in use since the container was started. It is important to bear in mind that there could be overlap. In other words, if this metric shows 10 seconds of CPU usage, it could be that both CPUs were busy for the same 5 seconds of time. |
| cpu.cpu_usage.usage_in_kernelmode | COUNTER | nanoseconds |  | yes | no | This is the number of nanoseconds of total_usage that was spent on kernel (OS) level threads. |
| cpu.cpu_usage.usage_in_usermode | COUNTER | nanoseconds |  | yes | no | This is the number of nanoseconds of total_usage that was spent on user threads. |
| cpu.system_cpu_usage | COUNTER | nanoseconds |  | yes | no | This metric is a little confusing, as it is the number of nanseconds used by the host since the host started; however, it is the sum of all CPU metrics, including idle, so it should be increasing at a constant rate. Put another way, when doing the deltas between intervals, the value should always be equal to the interval length times the number of CPUs. In practice, the number is always a bit less than this and experiences variations, possibly due to measurement error. |
| cpu.throttling_data.periods | COUNTER | count |  | yes | no | The number of “periods” during which the CPU for the container could have been thottled. If throttling is not enabled for the container, this value will always be 0. |
| cpu.throttling_data.throttled_periods | COUNTER | count |  | no | no | The number of “periods” during which the CPU for the container actuallywas thottled. If throttling is not enabled for the container, this value will always be 0. In all cases, this value will be less than or equal to the periods metric. |
| cpu.throttling_data.throttled_time | COUNTER | count |  | no | no | “The amount of time in nanoseconds taht the container has spent being throttled.” |

#### Memory

| Fully Qualified Name(FQN) | Type | Units | Statistic* | BASE | CORR | Description |
|----------------------------------|---------|-------|------------|------|------|-------------------------------------------------------------|
| memory.limit | GAUGE | bytes | average | no | no | The total amount of memory available to the container. |
| memory.max_usage | GAUGE | bytes | average | no | no | The maxiumum amount of memory the container has ever used. |
| memory.stats.active_anon | GAUGE | bytes | average | no | no |  |
| memory.stats.active_file | GAUGE | bytes | average | no | no |  |
| memory.stats.inactive_anon | GAUGE | bytes | average | no | no |  |
| memory,stats.inactive_file | GAUGE | bytes | average | no | no |  |
| memory.stats.mapped_file | GAUGE | bytes | average | no | no |  |
| memory.stats.total_active_anon | GAUGE | bytes | average | yes | no |  |
| memory.stats.total_active_file | GAUGE | bytes | average | no | no |  |
| memory.stats_total_cache | GAUGE | bytes | average | no | no |  |
| memory.stats.total_inactive_anon | GAUGE | bytes | average | no | no |  |
| memory.stats.total_inactive_file | GAUGE | bytes | average | no | no |  |
| memory.stats.total_mapped_file | GAUGE | bytes | average | no | no |  |
| memory.stats.total_pgpgin | COUNTER | bytes |  | yes | no |  |
| memory.stats.total_pgpgout | COUNTER | bytes |  | yes | no |  |
| memory.stats.total_rss | GAUGE | bytes | average | yes | no |  |
| memory.stats.total_unevictable | GAUGE | bytes | average | no | no |  |
| memory.usage | GAUGE | bytes | average | yes | no | The amount of memory currently being used by the container. |
| memory.stats.total_rss_huge | GAUGE | bytes | average | yes | no |  |
| memory.stats.total_writeback | GAUGE | bytes | average | yes | no |  |

#### Network

| Fully Qualified Name(FQN) | Type | Units | Statistic* | BASE | CORR | Description |
|---------------------------|------|-------|------------|------|------|-------------|
| network.eth0.rx_bytes |  |  |  |  |  |  |
| network.eth0.rx_dropped |  |  |  |  |  |  |
| network.eth0.rx_errors |  |  |  |  |  |  |
| network.eth0.rx_packets |  |  |  |  |  |  |
| network.eth0.tx_bytes |  |  |  |  |  |  |
| network.eth0.tx_dropped |  |  |  |  |  |  |
| network.eth0.tx_errors |  |  |  |  |  |  |
| network.eth0.tx_packets |  |  |  |  |  |  |

## Standard Mode

See our [docker metrics][1] pages for a list of all metrics ingested by Standard Mode.

[1]: /integrations/docker/docker-metrics
