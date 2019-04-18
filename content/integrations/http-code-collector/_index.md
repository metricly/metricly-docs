---
title: "HTTP Code"
#date: 2018-12-11
draft: false
tags: ["#http code", "#integrations", "#collectors"]
author: Lawrence Lane
---
HTTP status codes are useful diagnostic tools for a website to help determine if all content on a website is being delivered properly. Enabling the HTTP code collector for your preferred website will log every status code returned by the website. The first time a status code is returned, our Linux agent will create a metric for that code in Metricly; each subsequent time the status code is returned, another metric will begin to count how many times the code has been returned. Thanks to this unique collector and its metrics, you can create a policy to monitor the status codes that are returned from your website, which can act as a basic check for website status.

## Prerequisites

The [Linux Agent][1] is required before proceeding with the setup of the HTTP Code Collector. If you need to disable the Linux integration or view the unique API key assigned to your account, navigate to the Integrations page under the user account drop-down menu and click the integration designated as Infrastructure under the Integration column.

## Update the Configuration File

1. Navigate to the **collectors** folder, `/opt/netuitive-agent/conf/collectors`.
2. Open the `HttpCodeCollector.conf` file.
3. Change the **enabled** setting to `True`.
4. Change the **`req_url`** setting to contain the web page you want to collect statistics on.
5. **Save** the file, and **restart** the Linux Agent.

## Collector Options

| Option                 | Default             | Description                                                                                                                                                                                |
|------------------------|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| enabled                | False               | Enable collecting HTTP metrics.                                                                                                                                                            |
| req_url                | http://example.com/ | Comma-separated array of the full URLs to collect statistics on. For applications running on ports other than 80 or 443, users can include the port in the URL (http://example.com:8080/). |
| byte_unit              |                     | Default numeric output(s).                                                                                                                                                                 |
| measure_collector_time |                     | Measure the collector’s run time in milliseconds.                                                                                                                                          |
| metrics_blacklist      |                     | Regex list to match metrics to block. Mutually exclusive with metrics_whitelist option.                                                                                                    |
| metrics_whitelist      |                     | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklist option.                                                                                                 |
| req_vhost              |                     | A host header variable (if necessary) that will be added to each request.               |                     |                                                                                                                                                                                            |

[1]: /integrations/agents/linux-agent
