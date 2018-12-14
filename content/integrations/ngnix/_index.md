---
title: "NGNIX"
#date: 2018-12-12
draft: false
tags: ["ngnix", "integrations" ]
author: Lawrence Lane
---

## Prerequisites

## Configure

1. Navigate to the collectors folder, `/opt/netuitive-agent/conf/collectors`.
2. Open the **NginxCollector.conf** file.
4. Change the **enabled** setting to `True`.
5. **Save** the file.
6. Navigate to your Nginx server configuration file.
7. Add an additional section to your file:

```
server {
  listen 127.0.0.1;
  server_name localhost;
  location /nginx_status {
    # turns on nginx stats #
    stub_status on;
    # turns off logging #
    access_log off;
    allow 127.0.0.1;
    # sends rest of world to /dev/null #
    deny all;
  }
}
```
8\. **Save** the Nginx configuration file, and **restart** the Linux Agent.

This integration’s package (computed metrics, dashboards, and policies that will give you important events and alerts) will be automatically enabled and provisioned to your account as soon as Metricly receives data from the integration. The PACKAGES button on the integration setup page will become active once data is received, so you’ll be able to disable and re-enable the package at will.

## Collector Options

| Option                 | Default       | Description                                                                                |
|------------------------|---------------|--------------------------------------------------------------------------------------------|
| enabled                | FALSE         | Enable collecting Nginx metrics.                                                           |
| req_host               | localhost     | Hostname to collect from.                                                                  |
| req_port               | 80            | Port to collect from.                                                                      |
| req_path               | /nginx_status | Path to Nginx server.                                                                      |
| byte_unit              |               | Default numeric output(s).                                                                 |
| measure_collector_time |               | Measure the collector’s run time in milliseconds.                                          |
| metrics_blacklist      |               | Regex list to match metrics to block. Mutually exclusive with metrics_whitelist option.    |
| metrics_whitelist      |               | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklist option. |
| req_host_header        |               | The name of the HTTP host header (required for SSL certificate validation).                |
| req_ssl                |               | Enable SSL support.                                                                        |
