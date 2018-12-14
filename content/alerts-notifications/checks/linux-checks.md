---
title: "Linux Checks"
#date: 2018-04-12
draft: false
categories:
tags: ["alerts", "notifications", "checks", "linux"]
author: Lawrence Lane
alwaysopen: false
---

## Enable Linux Checks
Currently, Metricly comes with three pre-built checks; Heartbeat, Processes, and Ports. These are turnkey checks that do not require any scripting or coding, just simple configuration setting in the respective configuration files.

1. Make sure the Linux agent is installed.
2. Metricly checks can be enabled via the configuration files included with the agent.
3. All checks configuration files for the Linux agent can be found in ``/opt/netuitive-agent/conf/collectors``
4. Some of the checks are enabled by default, while you would need to enable other checks.

### Heartbeat Check
This check **is enabled** by default. For additional configuration, you can modify the following in the `HeartbeatCollector.conf` file where TTL represents Time To Live of the check and is expressed in seconds:

```
enabled = True
ttl = 120
```

### Port Checks
This check **is not enabled** by default. To enable Port Checks, update the `PortCheckCollector.conf` file. Make sure to follow the structure indicated in the file for ``[port]`` and ``[port_app_name]``.

```
# To enable the collector, set to True.
# Configure the ports that need to be monitored.

# [port] is the parent and [[port_app_name]] are the child entries.  
# Child entries must be listed below the parent as shown below.

enabled = False
ttl = 150

[port]

[[port_app_name]]
number = 8888
```

### Process Checks
This check **is not enabled** by default. Users need to update `ProcessCheckCollector.conf` to enable the collector and configure the processes that need to be monitored. There are three options for matching a process: process name, process executable or process command line.

{{% notice tip %}}
`exe` and `name` are both lists of comma-separated `regexps`.
{{% /notice %}}

#### Match by Name

```
[[nginx]]
name=^nginx
```

#### Match by Executable

```
[[postgres]]
exe=^/usr/lib/postgresql/+d.+d/bin/postgres$
```

#### Match by Command Line

```
[[elasticsearch]]
cmdline=java.*Elasticsearch
```

#### DNS Checks
The DNS check is **not enabled** by default. Users need to update the `DNSLookupCheckCollector.conf` file to enable this collector. URLs added to this list must be in the following format: `www.google.com`.  Note that the `dnsAddressLis`t requires a comma even when only one URL is provided. If the comma is not added, the collector returns with a ‘`cannot resolve hostname`‘ error.

```
enabled = true
ttl = 150

#Replace www.google.com and www.yahoo.com with the DNS names you want to check
dnsAddressList = www.google.com, www.yahoo.com
```
