---
title: "Process Resources"
#date: 2018-12-12
draft: false
tags: ["process resource collector", "integrations", "collectors" ]
author: Lawrence Lane
---
The Process Resources Collector can be used to collect CPU- and Memory-type metrics on a per-process level.  

## Prerequisites
- [Linux Agent][1]

## Configure

###  Update the Configuration File
1. Navigate to the **collectors** folder, `opt/netuitive-agent/conf/collectors`.
2. Open the **ProcessResourcesCollector.conf** file.
3. Change the **enabled** setting to `True`.
4. For each process you’d like to monitor, include the following below the **[process]** section:

```
[[process_name]]
name = ".*regex-statement.*"
```

Example

```
[[nginx]]
name = ^nginx
```
5\. **Save** the configuration file and **restart** the Linux Agent.

## Collector Options

| Option                 | Default | Description                                                                                |
|------------------------|---------|--------------------------------------------------------------------------------------------|
| enabled                | FALSE   | Enable collecting these metrics.                                                           |
| process                |         | A subcategory of settings inside of which each collected process has its configuration.    |
| byte_unit              |         | Default numeric output(s).                                                                 |
| name                   |         | Regex that matches the process name.                                                       |
| cmdline                |         | Regex that matches the full command line process name (including all the options).         |
| exe                    |         | Regex that matches the executable file that’s used to run the process.                     |
| measure_collector_time |         | Measure the collector’s run time in milliseconds.                                          |
| metrics_blacklist      |         | Regex list to match metrics to block. Mutually exclusive with metrics_whitelist option.    |
| metrics_whitelist      |         | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklist option. |
| unit                   |         | The unit of the memory data collected.                                                     |


[1]: /integrations/agents/linux-agent
