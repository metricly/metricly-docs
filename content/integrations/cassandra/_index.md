---
title: "Cassandra"
date: 2018-12-11
draft: true
tags: ["cassandra", "integrations", ]
author: Lawrence Lane
---

Cassandra is an open source distributed database management system. We use the Jolokia agent to monitor Cassandra’s performance as Cassandra exposes its metrics via JMX. Jolokia connects to a given mbean server and then exposes the server via a REST-like interface, acting as a bridge between JMX and HTTP/JSON.

## Configuration

1. **Download** the [Jolokia JVM JAR](http://search.maven.org/remotecontent?filepath=org/jolokia/jolokia-jvm/1.3.4/jolokia-jvm-1.3.4-agent.jar) file.
 - Move the downloaded file to the `/opt/netuitive-agent/` directory.
 - Add the following line to the very end of the `cassandra-env.sh` file (typically located in `/etc/cassandra/conf or /opt/cassandra/conf`):

```
JVM_OPTS="$JVM_OPTS -javaagent:/opt/netuitive-agent/jolokia-jvm-1.3.4-agent.jar"
```
{{% notice tip %}}
If you’re running Cassandra in a container, you’ll need to add ``–javaagent:/opt/agent.jar=port=8778,host=0.0.0.0`` to the end of the line above.
{{% /notice %}}
2. **Restart** Cassandra, and confirm Jolokia is running by accessing `http://localhost:8778/jolokia/`
3. Navigate to the **collectors** folder. The default location is `/opt/netuitive-agent/conf/collectors`.
4. Open the `CassandraJolokiaCollector.conf` file.
5. Change the **enabled** setting to `True`, **save** the file, and **restart** the Linux agent.

This integration’s package (computed metrics, dashboards, and policies that will give you important events and alerts) will be automatically enabled and provisioned to your account as soon as Metricly receives data from the integration. The PACKAGES button on the integration setup page will become active once data is received, so you’ll be able to disable and re-enable the package at will.

## Collector options

| Option                 | Default                                                                                                                                                                                                                               | Description                                                                                                                                          |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| enabled                | FALSE                                                                                                                                                                                                                                 | Enable collecting Cassandra metrics.                                                                                                                 |
| host                   | localhost                                                                                                                                                                                                                             | Hostname to collect from.                                                                                                                            |
| port                   | 8778                                                                                                                                                                                                                                  | Port to collect from.                                                                                                                                |
| path                   | cassandra                                                                                                                                                                                                                             | The metric prefix, e.g., how you want the metrics to show up in Metricly.                                                                            |
| jolokia_path           | jolokia                                                                                                                                                                                                                               | Part of the URL path that points to where your application serves metrics. Typically jmx or jolokia.                                                 |
| mbeans                 | org.apache.cassandra.metrics                                                                                                                                                                                                          | Pipe ( | ) delimited list of MBeans for which to collect stats. If no list is provided, all MBeans stats will be collected.                          |
| metrics_blacklist      | see below | Regex list to match metrics to block. Mutually exclusive with metrics_whitelistoption.                                                               |
| byte_unit              |                                                                                                                                                                                                                                       | Default numeric output(s).                                                                                                                           |
| histogram_regex        |                                                                                                                                                                                                                                       | Filter to only process attributes that match the specified regex.                                                                                    |
| measure_collector_time |                                                                                                                                                                                                                                       | Measure the collector’s run time in milliseconds.                                                                                                    |
| metrics_whitelist      |                                                                                                                                                                                                                                       | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklistoption.                                                            |
| password               |                                                                                                                                                                                                                                       | Password used for authentication.                                                                                                                    |
| percentiles            |                                                                                                                                                                                                                                       | Comma separated list of statistical percentiles to collect.                                                                                          |
| regex                  |                                                                                                                                                                                                                                       | Enables the mbeans option to match with regex.                                                                                                       |
| rewrite                |                                                                                                                                                                                                                                       | Config sub-section that contains pairs of from-to regex rewrites. See below for example.|
| username               |                                                                                                                                                                                                                                       | Username used for authentication.                                                                                                                    |

### Metrics Blacklist
```
.*Histogram.*|.*Percentile$|.*\.Min$|.*\.Max$|.*\.Mean$|.*\.Count$|.*\.StdDev$|.*\.
MeanRate$|.*\.FiveMinuteRate$|.*\.FifteenMinuteRate$|.*DroppedMessage.*|.*Last
GcInfo.*|Keyspace._Keyspaces.system.*|Keyspace._Keyspaces.*_Tables.*
```
### Rewrite
```
mbeans = "..."
[rewrite]
java = coffee
"-v\d+\.\d+\.\d+" = "-AllVersions"
".*Gets2Activities.*" = "...
```
