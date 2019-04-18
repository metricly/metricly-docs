---
title: "HTTP"
#date: 2018-12-11
draft: false
tags: ["#http", "#integrations", "#collectors"]
author: Lawrence Lane
---
The HTTP Collector gathers statistics from an HTTP or HTTPS connection.

## Prerequisites

The [Linux Agent][1] is required before proceeding with the setup of the HTTP Collector. If you need to disable the Linux integration or view the unique API key assigned to your account, navigate to the Integrations page under the user account drop-down menu and click the integration designated as Infrastructure under the Integration column.

## Update the Configuration File
1. Navigate to the **collectors** folder, `/opt/netuitive-agent/conf/collectors`.
2. Open the `HttpCollector.conf` file.
3. Change the **enabled** setting to `True`.
4. For each HTTP(s) you’d like to monitor, update the **`req_url`** list:

```
enabled = True
ttl_multiplier = 2
path_suffix = ""
measure_collector_time = False
byte_unit = byte
req_url = https://www.my_server.com/, https://www.my_server.com/assets/jquery.js
```
5\. **Save** the configuration file and **restart** the Linux Agent.

## Collector Options

| Setting                | Default            | Description                                                                                                                                          | Type     |
|------------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| byte_unit              | byte               | Default numeric output(s)                                                                                                                            | str      |
| enabled                | FALSE              | Enable collecting these metrics                                                                                                                      | bool     |
| measure_collector_time | FALSE              | Collect the collector run time in ms                                                                                                                 | bool     |
| metrics_blacklist      | None               | Regex to match metrics to block. Mutually exclusive with metrics_whitelist                                                                           | NoneType |
| metrics_whitelist      | None               | Regex to match metrics to transmit. Mutually exclusive with metrics_blacklist                                                                        | NoneType |
| req_url                | http://localhost/, | An array of full URL to get. For applications running on ports other than 80 or 443, users can include the port in the URL (http://localhost:8080/). | list     |
| req_vhost              |                    | Host header variable if needed. Will be added to every request                                                                                       | str      |



[1]: /integrations/agents/linux-agent
