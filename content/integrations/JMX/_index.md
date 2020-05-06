---
title: "JMX"
#date: 2018-12-11
draft: false
tags: ["#jmx", "#integrations", "#collectors" ]
author: Lawrence Lane
---
## Prerequisites

The [Linux Agent][1] is required before proceeding with the setup of JMX. If you need to disable the Linux integration or view the unique API key assigned to your account, navigate to the Integrations page under the user account drop-down menu and click the integration designated as Infrastructure under the Integration column.

## Configuration

1. Download the [Jolokia JVM JAR file](http://search.maven.org/remotecontent?filepath=org/jolokia/jolokia-jvm/1.3.4/jolokia-jvm-1.3.4-agent.jar).
2. Move the downloaded file to the `/opt/netuitive-agent/` directory.
3. Restart your application with the following argument added where `port` and `host` indicate where the jolokia agent will be listening: `-javaagent:/opt/netuitive-agent/jolokia-jvm-1.3.4-agent.jar=port=8778,host=0.0.0.0`
4. Navigate to the **/opt/netuitive-agent/conf/collectors** folder.
5. Open the **JolokiaCollector.conf** file.
6. Change the **enabled** setting to `True`.
7. **Save** the configuration file and **restart** the Linux Agent.

## Example

We want to run the java application `hello-world.jar` located in `/opt/java` with the jolokia agent specified in the `-javaagent` option.

```
java -javaagent:/opt/netuitive-agent/jolokia-jvm-1.3.4-agent.jar=port=8778,host=0.0.0.0 -jar /opt/java/hello-world.jar
 ```

## Configuration Options

| Option                 | Default   | Description                                                                                                                 |
|------------------------|-----------|-----------------------------------------------------------------------------------------------------------------------------|
| enabled                | False     | Enable collecting Jolokia metrics.                                                                                          |
| host                   | localhost | Hostname to collect from.                                                                                                   |
| port                   | 8778      | Port to collect from.                                                                                                       |
| path                   | jmx       | The metric prefix, e.g., how you want the metrics to show up in CloudWisdom.                                                   |
| jolokia_path           | jolokia   | Part of the URL path that points to where your application serves metrics. Typically jmx or jolokia.                        |
| mbeans                 | java.*    | Pipe delimited list of MBeans for which to collect stats. If no list is provided, all MBeans stats will be collected. |
| regex                  | TRUE      | Enables the mbeans option to match with regex.                                                                              |
| byte_unit              |           | Default numeric output(s).                                                                                                  |
| measure_collector_time |           | Measure the collector’s run time in milliseconds.                                                                           |
| metrics_blacklist      |           | Regex list to match metrics to block. Mutually exclusive with metrics_whitelistoption.                                      |
| metrics_whitelist      |           | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklistoption.                                   |
| password               |           | Password used for authentication.                                                                                           |
| rewrite                |           | Config sub-section that contains pairs of from-to regex rewrites.                                                           |
| username               |           | Username used for authentication.                                                                                           |

### Rewrite Example
```
mbeans = "..."
[rewrite]
java = coffee
"-v\d+\.\d+\.\d+" = "-AllVersions"
".*Gets2Activities.*" = ""...
```

[1]: /integrations/agents/linux-agent
