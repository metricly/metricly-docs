---
title: "Docker Policies"
#date: 2018-04-12
draft: false
categories:
tags: ["#alerts", "#notifications", "#policies", "#default policies", "#docker"]
author: Lawrence Lane
---

| Policy name                                     | Duration     | Conditions                                                                                                   | Category | Description                                                                                   |
|-------------------------------------------------|--------------|--------------------------------------------------------------------------------------------------------------|----------|-----------------------------------------------------------------------------------------------|
| Docker Container – CPU Throttling               | 15 min       | netuitive.docker.cpu.container_throttling_percent has a static threshold >0                                   | WARNING  | The Docker container has had its CPU usage throttled for at least the past 15 minutes.        |
| Docker Container – Elevated CPU Utilization     | 30 min       | netuitive.docker.cpu.container_cpu_percent has an upper baseline deviation + an upper contextual deviation    | INFO     | CPU usage on the Docker container has been higher than expected for 30 minutes or longer.     |
| Docker Container – Elevated Memory Utililzation | 30 min       | netuitive.docker.cpu.container_memory_percent has an upper baseline deviation + an upper contextual deviation | INFO     | Memory usage on the Docker container has been highter than expected for 30 minutes or longer. |
| Docker Container – Extensive CPU Throttling     | 1 hour 5 min | netuitive.docker.cpu.container_throttling_percent has a static threshold >0                                   | CRITICAL | The Docker container has had its CPU usage throttled for over an hour.                        |
