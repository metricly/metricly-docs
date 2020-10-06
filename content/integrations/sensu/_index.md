---
title: "Sensu"
#date: 2018-12-11
draft: false
tags: ["#sensu", "#integrations" ]
author: Lawrence Lane
---
Sensu is a monitoring tool that can create events to alert users about server failures, application health, and more. Sensu can be configured to send external events to CloudWisdom. This feature is only compatible with Linux machines.

## How to Send Events From Sensu

1. Hover on your account name in the top right-hand corner and click **API Keys** from the drop-down menu.
2. Copy the **API key** from the custom integration in the table.
3. Install the [Metricly Event Handler](https://github.com/netuitive/netuitive-event-handler).
4. Download the Metricly Event Handler to the **/bin** directory.

```
sudo curl
http://repos.us.cloudwisdom.virtana.com/cli
-agent/metricly-event-handler-linux -o
"/bin/metricly-event-handler"
```
5\. Ensure the file is executable (use the `chmod` command).  
6. Create and configure the **/etc/metricly/metricly-event-handler.yaml** file using the API key you copied in step 2 and the URL to the events ingest API.

```
url: "https://api.us.cloudwisdom.virtana.com/ingest/events"
```
7\. [Create a handler in Sensu](https://docs.sensu.io/sensu-core/latest/reference/handlers/).  
8. Create a file named **metricly_handler.json** in `etc/sensu/conf.d`

```
{
  "handlers": {
    "metricly-event-handler": {
      "type": "pipe",
      "command": "/bin/metricly
      -event-handler stdin -s Sensu",
      "severities": [
        "critical",
        "ok"
      ]
    }
  }
}
```
9\. [Create at least one check in Sensu](https://docs.sensu.io/sensu-core/latest/guides/intro-to-checks/).  
10. **Restart** the Sensu services to pick up the new check and handler.  
11. Check CloudWisdom for your new Sensu events.  


## Example

To add a check to detect if the Linux Agent supervisor is running:

1. Install the process checks script

```
sudo sensu-install -p process-checks:0.0.6
```
2\. Create a file named **check_linux-agent.json** in `etc/sensu/conf.d`.

```
{
  "checks": {
    "linux-agent": {
      "command": "check-process.rb -p
      'linux-agent - Handlers'
      -W 1 -C 1 -w 1 -c 1",
      "standalone": true,
      "interval": 60,
      "handlers": ["debug", "metricly-event-handler"]
    }
  }
}
```
