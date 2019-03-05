---
title: "Kafka Metrics"
#date: 2018-12-11
draft: false
tags: ["#kafka", "#integrations", "#collectors", "#metrics" ]
author: Lawrence Lane
---

Due to the sheer volume of Kafka metrics, the individual metrics won’t be documented here. Instead, this page outlines general properties for the groups of metrics.

## Properties All Metrics Share:
- **Statistic**: `average`
- **Min**: `0`
- **CORR**: no
- **UTIL**: no
- **BASE**:
  - **On** for most metrics
  - **Off** for metrics matching the following regexes:
    - `^kafka.cluster.*`
    - `^kafka\.utils\..*`
    - `^kafka\.log\..*(LogEndOffset|LogStartOffset)$`
    - `^kafka\.controller\.((?!broker-\d).).*`
    - `^kafka\.consumer_group\.((?!consumer_lag$).)*$`

## Metrics That End With Percent:
  - **Unit**: `percent`
  - **Max**: `1`

## Metrics With `Bytes.*PerSec` or `byte-rate`:
  - **Unit**: `Bps` (bytes per second)
  - **SDS**: `ReplaceWithZero`

## Metrics For Units of Time:
  - **Unit**
    - If the metric name ends with `Ms.Mean`, `time-avg`, or `time-max` then the units are ms (milliseconds)
    - If the metric name contains `time-ns`, then the units are `ns`(nanoseconds)
    - If the metric name contains `time-secs`, then the units are
seconds
 - **SDS**: `ReplaceWithZero`

## Other Metrics
 - For metrics matching `kafka\.(server|network)\..*Metrics\..*\.Count orkafka.zookeeper.zk_packets.*`:
    - **Type**: `COUNTER`

 - The Zookeeper `has_owner` metric:
    - **Max**: `1`
- All Zookeeper latency metrics (`zk_.*latency`):
    - **Unit**: `ms` (milliseconds)
- All Zookeeper data size metrics (`zk_.*data_size`):
    - **Unit**: `bytes`
