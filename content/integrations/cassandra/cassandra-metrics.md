---
title: "Cassandra Metrics"
#date: 2018-12-11
draft: false
tags: ["#cassandra", "#integrations", "#metrics" ]
author: Lawrence Lane
---

Due to the sheer volume of Cassandra metrics, the individual metrics won’t be documented here. Instead, here are some general properties of the groups of metrics:

## All Metrics Share the Following Properties:
- **Type**: GAUGE
- **Statistic**: average
- **Min**: 0
- **Sparse Data Strategy**: None
- **BASE**: Yes
- **CORR**: No
- **UTIL**: No

### Ending in `Latency.OneMinuteRate`:
- **Unit**: ms (milliseconds)

### Non-latency `OneMinuteRate` Metrics:
- Unit = ops (operations per second)

### Contains `HeapSize`, `DataSize`, `DiskSpace`, `Memory`, or `RowSize`:
- **Unit**: bytes

### Ending with HitRate or Ratio:
- **Unit**:  `percentunit` (i.e. percentage represented as a value between 0 and 1)
- **Max**: 1
