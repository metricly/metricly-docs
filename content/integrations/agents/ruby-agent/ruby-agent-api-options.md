---
title: "API Options"
#date: 2018-12-12
draft: false
tags: ["#ruby", "#integrations", "#agents" ]
author: Lawrence Lane
---

## Log properties

- **logLocation**: The absolute path of the log file. Leave this option blank to use the default location in the gem directory.
- **logAge**: Specify either the number of log files to keep or the frequency of rotation (daily, weekly, or monthly).
- **logSize**: Specify the maximum log file size (in bytes).
- **debugLevel**: Options include (in ascending order of severity) error, info, and debug.

## Netuitived Connection Properties

Netuitived address and port information.


## Cache Properties
The cache settings are related to the threads and events on your host ruby application. It allows for a small buffer to limit the amount of calls made to the daemon. The main purpose is to cache enough data to not have excessive thread growth when making calls to the daemon.

- **sampleCacheEnabled**: Set to `true` to enable the sample cache.
- **sampleCacheSize**: The maximum number of samples cached before the samples are sent to netuitived.
- **sampleCacheInterval**: Interval (in seconds) at which the cached samples are sent to `netuitived`.
- **eventCacheEnabled**: Set to `true` to enable the sample cache.
- **eventCacheSize**: The maximum number of events cached before the events are sent to `netuitived`.
- **eventCacheInterval**: Interval (in seconds) at which the cached events are sent to `netuitived`.
