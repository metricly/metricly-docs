---
title: "Troubleshooting"
date: 2018-12-03
draft: false
categories:
tags: ["getting started", "metrics",]
author: Lawrence Lane
pre: "<i class='fa fa-bug'></i> &nbsp;"
---

## Collected Metrics
If you are seeing metrics that will not collect continually, there are two common scenarios:
- Your agent-based (Linux, Windows) collector has metrics that are not available anymore being collected
- Your agentless-based collector (AWS, Azure) is collecting metrics from a service that’s not being used, e.g., a lambda function not firing or an SQS queue is empty.

Removing these metrics from being collected is the optimal solution.  

### Remove via Agent Based Collector

Use a metric whitelist or blacklist for agent-based collectors

**Example Blacklist**
you could use a negative lookahead ``(?! )`` to specify a group that cannot match after the main expression--if something matches, the result is discarded: `metrics_blacklist = elasticsearch.indices.(?!_all$|datastore$|docs$)`

### Remove  via Agentless Collector

Tweak your filtering in Metricly; if that does not work, you may be experiencing ingestion issues.
