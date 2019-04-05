---
title: "Troubleshooting"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#agents", "#linux", "#logs", "#metadata"]
author: Lawrence Lane
#pre: "<i class='fa fa-bug'></i> &nbsp;"
weight: 11
---
# Linux Agent
##  Set Logs to Debugging Mode
To set the Linux Agent logs to Debugging Mode, update the `netuitive-agent.conf` file.

1. Navigate to the `netuitive-agent.conf` file.
2. `Update level = INFO` to `level = DEBUG`.
3. **Save** and **restart** your agent.

```
# to increase verbosity, set DEBUG
level = DEBUG
handlers = rotated_file
propagate = 1
```

## Need Help?
### 1. Save as Zip File

Copy `/opt/netuitive-agent/bin/get-support` and paste it into your command line interface to zip up your agent configurations, logs, and system metadata. The file will be stored in `/opt/netuitive-agent/`

**Success Message:**
```
Collecting logs and configuration....
creating file....
Please open a support case and upload
/opt/netuitive-agent/support-YYYYMMDD_173454
with a detailed description of the issue.
Thank you
```

### 2. Send Zip to Support

 Open a support ticket by emailing `support@metricly.com` with the file attached and a subject / message body describing the issue(s) you experienced.
 
 
 # Docker Container Agent
 ### Agent Logging
Agent logs will not be available from the netuitive-agent container directly, as they're redirected to stdout via /proc for viewing from the docker CLI. See https://docs.docker.com/config/containers/logging/

To change the log level, you may pass the desired level (ERROR, WARN, INFO, DEBUG) via the initial `docker run` command using the `-e` flag.
`docker run -d -p 8125:8125/udp --name netuitive-agent `**`-e DEBUG`**` -e DOCKER_HOSTNAME="my-docker-host" -e APIKEY="my-api-key" -v /proc:/host_proc:ro -v /var/run/docker.sock:/var/run/docker.sock:ro netuitive/docker-agent`


To view agent logs from the Docker CLI run `docker logs netuitive-agent`
```
Configuring...
Configuring APIKEY with [removed]
Configuring HTTPVAR with https
Configuring loglevel with DEBUG
Configuring interval with 60
Configuring APIHOST with api.app.netuitive.com
Configuring HOSTNAME with my-docker-host
Configuring LISTEN_IP with 0.0.0.0
Configuring LISTEN_PORT with 8125
Configuring FORWARD_IP with 127.0.0.2
Configuring FORWARD_PORT with 8125
Configuring FORWARD with False
Starting Services...
[2019-04-05 21:31:50,999] [MainThread] Changed UID: 0 () GID: 0 ().
[2019-04-05 21:31:51,730] [INFO] : Listening on 0.0.0.0:8125
```
