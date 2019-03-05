---
title: "SNMP Interface"
#date: 2018-12-11
draft: false
tags: ["#snmp", "#integrations", "#collectors" ]
author: Lawrence Lane
---

The Simple Network Management Protocol (SNMP) Interface collector is used to allow the Linux agent to monitor the performance of remote SNMP-enabled devices like routers and switches. The collector can gather data from as many devices as necessary by adding additional configuration sections under the [devices] header; see the example below for details.

## Prerequisites
You should have SNMP set-up and your community string ready prior to activating the SNMP collector.

- [Linux Agent][1]

## Configure

1. Navigate to the **collectors** folder, `/opt/netuitive-agent/conf/collectors`.
2. Open the **SNMPInterfaceCollector.conf** file.
3. Change the **enabled** setting to `True`.
4. Update the other settings as necessary, or add additional devices using the defaults as a guide.
6. **Save** the configuration file and **restart** the Linux Agent.

## Collector Options

| Option                 | Default   | Description                                                                                                                                                                        |
|------------------------|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| enabled                | FALSE     | Enable collecting SNMP metrics.                                                                                                                                                    |
| path                   | interface | The file path to the SNMP Interface.                                                                                                                                               |
| interval               | 60        | How often the collector collects metrics (in seconds). Note The 60-second default may be taxing on your hardware. You may want to increase the collection interval to 120 seconds. |
| retries                | 3         | Number of times the collector will retry before stopping.                                                                                                                          |
| timeout                | 5         | Seconds before the SNMP connection will automatically timeout.                                                                                                                     |
| byte_unit              |           | Default numeric output(s).                                                                                                                                                         |
| measure_collector_time |           | Measure the collector’s run time in milliseconds.                                                                                                                                  |
| metrics_blacklist      |           | Regex list to match metrics to block. Mutually exclusive with metrics_whitelistoption.                                                                                             |
| metrics_whitelist      |           | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklistoption.                                                                                          |


[1]: /integrations/agents/linux-agent
