---
title: "HTTPD"
#date: 2018-12-11
draft: false
tags: ["#httpd", "#integrations", "#collectors"]
author: Lawrence Lane
---
The HTTP Collector gathers statistics from an HTTP or HTTPS connection.

## Prerequisites

The [Linux Agent][1] is required before proceeding with the setup of HTTPD. If you need to disable the Linux integration or view the unique API key assigned to your account, navigate to the Integrations page under the user account drop-down menu and click the integration designated as Infrastructure under the Integration column.

## Update the Configuration File
1. Navigate to the **collectors** folder, `/opt/netuitive-agent/conf/collectors`.
2. Open the `HttpCollector.conf` file.
3. Change the **enabled** setting to `True`.
4. For each HTTP(s) you’d like to monitor, update the **`req_url`** list:

## Collector Options

| Option                 | Default                                            | Description                                                                                |
|------------------------|----------------------------------------------------|--------------------------------------------------------------------------------------------|
| enabled                | FALSE                                              | Enable collecting HTTPD metrics.                                                           |
| urls                   | localhost http://localhost:8080/server-status?auto | URLs to server-status in auto format, separated by commas.                                 |
| byte_unit              |                                                    | Default numeric output(s).                                                                 |
| measure_collector_time |                                                    | Measure the collector’s run time in milliseconds.                                          |
| metrics_blacklist      |                                                    | Regex list to match metrics to block. Mutually exclusive with metrics_whitelist option.    |
| metrics_whitelist      |                                                    | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklist option. |


[1]: /integrations/agents/linux-agent
