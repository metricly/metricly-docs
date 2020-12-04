---
title: "Docker Computed Metrics"
#date: 2018-12-11
draft: false
tags: ["docker", "integrations", "metrics",]
author: Lawrence Lane
---

##  Computed

| Name                         | FQN                                               | Computation                                                                                                                                                   | Units   | Min | Max | BASE | CORR | Description                                                                                            |
|------------------------------|---------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|-----|-----|------|------|--------------------------------------------------------------------------------------------------------|
| Container CPU Percent        | netuitive.docker.cpu.container_cpu_percent        | data[‘cpu.system_cpu_usage’].actual == 0 ? 0 :(data[‘cpu.cpu_usage.total_usage’].actual /data[‘cpu.system_cpu_usage’].actual) * 100                           | percent | 0   | 100 | yes  | yes  | The percentage of total CPU being used by the container.                                               |
| Container Memory Percent     | netuitive.docker.cpu.container_memory_percent     | (data[‘memory.usage’].actual / data[‘memory.limit’].actual) * 100                                                                                             | percent | 0   | 100 | yes  | yes  | The amount of memory in use by the container, expressed as a percentage of the memory available to it. |
| Container Throttling Percent | netuitive.docker.cpu.container_throttling_percent | data[‘cpu.throttling_data.periods’].actual == 0 ? 0 :(data[‘cpu.throttling_data.throttled_periods’].actual /data[‘cpu.throttling_data.periods’].actual) * 100 | percent | 0   | 100 | yes  | yes  | The percentage of periods that the container spent having its CPU usage throttled.                     |
