---
title: "Solr"
#date: 2018-12-11
draft: false
tags: ["solr", "integrations"]
author: Lawrence Lane
---
Solr is an open source search platform, allowing for full-text search, hit highlighting, faceted search, and much more. Metricly can be used to monitor the performance of your Solr server.

## Prerequisites
- [Linux Agent][1]


## Configuration
1. Navigate to the **collectors** folder, `/opt/netuitive-agent/conf/collectors`.
2. Open the **SolrCollector.conf** file.
3. Change the **enabled** setting to `True`.
4. **Save** the configuration file and **restart** the Linux Agent.

## Collector Options

| Option                 | Default | Description                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|------------------------|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| enabled                | FALSE   | Enable collecting Solr metrics.                                                                                                                                                                                                                                                                                                                                                                                                                         |
| byte_unit              |         | Default numeric output(s).                                                                                                                                                                                                                                                                                                                                                                                                                              |
| core                   |         | Which cores the collector should report information on.                                                                                                                                                                                                                                                                                                                                                                                                 |
| host                   |         | Hostname to collect from.                                                                                                                                                                                                                                                                                                                                                                                                                               |
| measure_collector_time |         | Measure the collector’s run time in milliseconds.                                                                                                                                                                                                                                                                                                                                                                                                       |
| metrics_blacklist      |         | Regex list to match metrics to block. Mutually exclusive with metrics_whitelistoption.                                                                                                                                                                                                                                                                                                                                                                  |
| metrics_whitelist      |         | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklistoption.                                                                                                                                                                                                                                                                                                                                                               |
| port                   |         | Port to collect from.                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| stats                  |         | Types of stats reported from the collector.  All options are enabled by default. |


###  Stats Options

- **core**: Stats on the different cores on your machine.
- **response**: Stats on ping response.
- **query**: Stats on query handling. update: Stats on update handling.
- **cache**: Stats on fieldValue, filter, document, and queryResult caches.
- **jvm**: Stats on the JVM.
- **replication**: Stats on replication.Values should be formatted as a comma separated list.

[1]: /integrations/agents/linux-agent
