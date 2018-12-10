---
title: "Upgrade"
date: 2018-11-30T16:08:13-05:00
draft: true
categories: ["integration", "admin guide", "getting started"]
tags: ["agents", "linux", "upgrade"]
author: Lawrence Lane
weight: 5
---

It’s important you upgrade to the latest version of the Linux Agent whenever possible, as we’re constantly improving it. Check out the recently closed issues and pull requests, as well as the release history, to see why you should upgrade.

1. Stop the Linux Agent (use the appropriate command for your distro). The most common being:
 - `service netuitive-agent stop`
 - ``/etc/init.d/netuitive-agent stop``
 - `initctl stop netuitive-agent`
 - `systemctl stop netuitive-agent`
2. Run `yum -y update netuitive-agent`.
 - or `apt-get update netuitive-agent`
 - or `apt-get install --only-upgrade netuitive-agent`
 {{% alert theme="info" %}}If you have not customized the Netuitive configuration file in any way (other than inputting the API key), jump to step 6. If you’ve customized the configuration file, continue on. {{% /alert %}}
3. Get the difference between the old configuration file `netuitive-agent.conf` and the new configuration file `netuitive-agent.conf.rpmnew`
 - `diff -u /opt/netuitive-agent/conf/netuitive-agent.conf.rpmnew /opt/netuitiveagent/conf/netuitive-agent.conf`
4. Copy your changes from the old file to new file.
5. Rename the old file to `netuitive-agent.conf.old` and the new configuration file to `netuitive-agent.conf`.
6. Start the Linux Agent. The most common commands being:
 - `service netuitive-agent start`
 - ``/etc/init.d/netuitive-agent start``
 - `initctl start netuitive-agent`
 - `systemctl start netuitive-agent`

{{% alert theme="info" %}} You can delete the element in Metricly, and it will reappear after the next processing cycle. Your element will not lose any data. {{% /alert %}}
