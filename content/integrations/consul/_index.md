---
title: "Consul"
date: 2018-12-11
draft: false
tags: ["consul", "integrations", ]
author: Lawrence Lane
---

Each node (and service per node) has a set of checks.

- A node or service is marked `critical` if any check is marked `critical` for the node or service.
- A node or service is marked  `warning` if any check is marked, so long as there are no `criticals`.
- A node or service is marked `passing` if no checks are marked.

## Configuration
These steps assume you have already set up Consul service. If you have not yet set up Consul, view their [GitHub](https://github.com/hashicorp/consul) to get started.

### 1. Linux Agent
The [Linux Agent][1] must be installed in order to collect Consul metrics.

### 2. ConsulCollector.conf
To enable metric collection, update the `/opt/netuitive-agent/conf/collectors/ConsulCollector.conf` file:
```
enabled = True
url = http://localhost:8500
```


[1]: /integrations/agents/linux-agent
