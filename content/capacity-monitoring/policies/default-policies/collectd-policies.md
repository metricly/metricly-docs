---
title: "Collectd Policies"
#date: 2018-04-12
draft: false
categories:
tags: ["#alerts", "#notifications", "#policies", "#default policies", "#collectd",]
author: Lawrence Lane
---

| Policy name                              | Duration | Conditions                                                                  | Category | Description                                                                                       |
|------------------------------------------|----------|-----------------------------------------------------------------------------|----------|---------------------------------------------------------------------------------------------------|
| Elevated Memory Usage (Collectd)         | 30 min   | netuitive.collectd.memory.utilizationpercent has an upper baseline deviation | INFO     | Indicates an increase in memory usage above what is considered to be normal.                      |
| Elevated Process Count                   | 30 min   | netuitive.collectd.processes.total has an upper baseline deviation           | INFO     | Indicates that the total number of processes has increased above what is considered to be normal. |
| Elevated Percentage of Blocked Processes | 30 min   | netuitive.collectd.processes.blockedpercent has an upper baseline deviation  | WARNING  | Indicates a higher-than-normal percentage of blocked processes.                                   |
| Elevated Percentage of Zombie Processes  | 30 min   | netuitive.collectd.processes.zombiepercent has an upper baseline deviation   | WARNING  | Indicates a higher-than-normal percentage of zombie processes.                                    |
