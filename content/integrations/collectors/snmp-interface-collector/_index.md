---
title: "SNMP"
#date: 2018-12-11
draft: false
tags: ["snmp", "integrations", "collectors" ]
author: Lawrence Lane
---

The SNMP Collector is used to allow Metricly to monitor the performance of SNMP-enabled devices using a set of specified OIDs. The collector can gather data from as many devices as necessary by adding additional configuration sections under the [devices] header.

## Prerequisites
You should have SNMP set-up and your community string ready prior to activating the SNMP collector.

- [Linux Agent][1]

## Configure

1. Navigate to the **collectors** folder, `/opt/netuitive-agent/conf/collectors`.
2. Open the **SNMPCollector.conf** file.
3. Change the **enabled** setting to `True`.
4. Change the **my-identification-for-this-host** header to the name of the host you want to monitor.
5. Under the **[[[oids]]]** section, add additional `OID-metric pairs` list as necessary for the metrics you want Metricly to collect.
6. **Save** the configuration file and **restart** the Linux Agent.

## Collector Options

| Option                 | Default | Description                                                                                                                                                                   |
|------------------------|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| enabled                | FALSE   | Enable collecting SNMP metrics.                                                                                                                                               |
| interval               | 60      | How often the collector collects metrics (in seconds). The 60-second default may be taxing on your hardware. You may want to increase the collection interval to 120 seconds. |
| byte_unit              |         | Default numeric output(s).                                                                                                                                                    |
| measure_collector_time |         | Measure the collector’s run time in milliseconds.                                                                                                                             |
| metrics_blacklist      |         | Regex list to match metrics to block. Mutually exclusive with metrics_whitelistoption.                                                                                        |
| metrics_whitelist      |         | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklistoption.                                                                                     |
| retries                |         | Number of times the collector will retry before stopping.                                                                                                                     |
| timeout                |         | Seconds before the SNMP connection will automatically timeout.                                                                                                                |



[1]: /integrations/agents/linux-agent
