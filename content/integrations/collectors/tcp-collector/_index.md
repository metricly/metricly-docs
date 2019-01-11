---
title: "TCP"
#date: 2018-12-11
draft: false
tags: ["#snmp", "#integrations", "#collectors" ]
author: Lawrence Lane
---

The TCP Collector collects metrics on TCP stats.



## Prerequisites

- [Linux Agent][1]

## Configure

1. Navigate to the **collectors** folder, `/opt/netuitive-agent/conf/collectors`.
2. Open the **TCPCollector.conf** file.
3. Change the **enabled** setting to `True`.
6. **Save** the configuration file and **restart** the Linux Agent.

## Collector Options

| Setting                | Default                                                                                                                                                                                                                                  | Description                                                                   | Type     |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|----------|
| allowed_names          | ListenOverflows, ListenDrops, TCPLoss, TCPTimeouts, TCPFastRetrans, TCPLostRetransmit, TCPForwardRetrans, TCPSlowStartRetrans, CurrEstab, TCPAbortOnMemory, TCPBacklogDrop, AttemptFails, EstabResets, InErrs, ActiveOpens, PassiveOpens | list of entries to collect, empty to collect all                              | str      |
| byte_unit              | byte                                                                                                                                                                                                                                     | Default numeric output(s)                                                     | str      |
| enabled                | False                                                                                                                                                                                                                                    | Enable collecting these metrics                                               | bool     |
| gauges                 | CurrEstab, MaxConn                                                                                                                                                                                                                       | list of metrics to be published as gauges                                     | str      |
| measure_collector_time | False                                                                                                                                                                                                                                    | Collect the collector run time in ms                                          | bool     |
| metrics_blacklist      | None                                                                                                                                                                                                                                     | Regex to match metrics to block. Mutually exclusive with metrics_whitelist    | NoneType |
| metrics_whitelist      | None                                                                                                                                                                                                                                     | Regex to match metrics to transmit. Mutually exclusive with metrics_blacklist | NoneType |

[1]: /integrations/agents/linux-agent
