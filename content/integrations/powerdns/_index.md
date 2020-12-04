---
title: "PowerDNS"
#date: 2018-12-12
draft: false
tags: ["powerdns", "integrations" ]
author: Lawrence Lane
---

## Prerequisites
- [Linux Agent][1]

## Configure

You cannot activate the PowerDNS integration until CloudWisdom begins receiving data. Once data arrives, the package ([Dashboards][2] and [Policies][3]) is automatically provisioned. To remove those Dashboards and Policies, click the toggle on the PowerDNS integration card.

### 1. Get API Key

1. In CloudWisdom, Navigate to **Integrations** > **PowerDNS**.
2. Copy the **API Key**.
3. Add this key to your Linux Agent.

### 2. Update the Configuration File

1. Open **PowerDNSCollector.conf** in the collectors folder, `/opt/netuitive-agent/conf/collectors`.
2. Change the **enabled** setting to `True`,]
3. **Save** the file and **restart** the agent.

## Collector Options

| Setting                | Default               | Description                                                                   | Type     |
|------------------------|-----------------------|-------------------------------------------------------------------------------|----------|
| bin                    | /usr/bin/pdns_control | The path to the pdns_control binary                                           | str      |
| byte_unit              | byte                  | Default numeric output(s)                                                     | str      |
| enabled                | FALSE                 | Enable collecting these metrics                                               | bool     |
| measure_collector_time | FALSE                 | Collect the collector run time in ms                                          | bool     |
| metrics_blacklist      | None                  | Regex to match metrics to block. Mutually exclusive with metrics_whitelist    | NoneType |
| metrics_whitelist      | None                  | Regex to match metrics to transmit. Mutually exclusive with metrics_blacklist | NoneType |
| sudo_cmd               | /usr/bin/sudo         | Path to sudo                                                                  | str      |
| use_sudo               | FALSE                 | Use sudo?                                                                     | bool     |

[1]: /integrations/agents/linux-agent
[2]: /dashboards/
[3]: /capacity-monitoring/policies
