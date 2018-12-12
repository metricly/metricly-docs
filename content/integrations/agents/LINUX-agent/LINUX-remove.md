---
title: "Remove"
date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["agents", "linux", "upgrade"]
author: Lawrence Lane
weight: 10
---

1. Stop the Linux Agent (use the appropriate command for your distro). The most common being:
 - `service netuitive-agent stop`
 - ``/etc/init.d/netuitive-agent stop``
 - `initctl stop netuitive-agent`
 - `systemctl stop netuitive-agent`
2. Remove the directory containing the Linux Agent. Default: ``rm -r /opt/netuitive-agent``.
 - If you don’t want to be prompted for each file that needs to be deleted, use `rm -rf /opt/netuitive-agent`
