---
title: "User Scripts Collector"
#date: 2018-12-12
draft: false
tags: ["#user scripts", "#integrations" ]
author: Lawrence Lane
---
The User Scripts Collector runs external scripts and collects their output for you to view in Metricly.

## Prerequisites
- [Linux Agent][1]


## Configure

1. Navigate to the **collectors** folder, `/opt/netuitive-agent/conf/collectors`.
2. Open the **UserScriptsCollector.conf** file.
3. Change the **enabled** setting to `True`.
4. Update **scripts_path** with the directory where your scripts are located (default: `/opt/netuitive-agent/`).
5. **Save** the configuration file and **restart** the Linux Agent.


### About Scripts

For the collector to work properly, your monitored scripts must be executable and should output metrics in the form of:
```
metric.path.a value
metric.path.b value
metric.path.c value
```
`Value` can be a static integer or the value stored in a variable;only numerical values are valid.

#### Examples

##### Checks Status of Metricly-Agent Service
This example checks the status of the **metricly-agent** service and outputs the value of `1` if it is running or `0` if it is not running. The value is stored in the `processes-running.netuitive-agent.count.value` metric.

```
#!/bin/sh

procscnt=`ps aux | grep -c "[n]etuitive-agent - Handlers"`
echo processes-running.netuitive-agent.count.value $procscnt
```
- Sets the **procscnt** variable to the value output by the command `ps aux | grep -c “[n]etuitive-agent – Handlers”`
- Returns the metric, **processes-running.netuitive-agent.count.value**, with the value stored in the variable proscnt.

##### Checks Total Running Processes & Threads
This example checks for total running processes and total running threads every 60 seconds.

```
#!/bin/sh

PROCTOTAL=`ps -A --no-headers | wc -l`
PROCTHREADS=`ps -AL --no-headers | wc -l`

echo processes.total_processes.count.value $PROCTOTAL
echo processes.total_threads.count.value $PROCTHREADS
```

##### Counts Log Occurrences
This example acknowledges a log every 60 seconds and count how many times a string shows in a log. This script is used to count log occurrences and converts that number into a metric.

```
#!/bin/sh

CHECKCOUNT=(awk -v d1="$(date --date="-1 min" "+%b %_d %H:%M")" -v  d2="$(date "+%b %_d %H:%M")" '$0 > d1 && $0 < d2 || $0 ~ d2' /var/log/secure
 | grep -ci "POSSIBLE BREAK-IN ATTEMPT")
echo possible_sudo_hacks.count.value $CHECKCOUNT
```


## Collector Options

| Option                 | Default               | Description                                                                               |
|------------------------|-----------------------|-------------------------------------------------------------------------------------------|
| enabled                | False                 | Enable collecting User Scripts metrics.                                                   |
| scripts_path           | /opt/netuitive-agent/ | Path used to find scripts to run                                                          |
| byte_unit              |                       | Default numeric output(s).                                                                |
| measure_collector_time |                       | Measure the collector’s run time in milliseconds.                                         |
| metrics_blacklist      |                       | Regex list to match metrics to block. Mutually exclusive with metrics_whitelist option.   |
| metrics_whitelist      |                       | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklistoption. |

[1]: /integrations/agents/linux-agent
