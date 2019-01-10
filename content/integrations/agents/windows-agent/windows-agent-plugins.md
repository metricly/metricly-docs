---
title: "Plugins"
#date: 2018-12-11
draft: false
tags: ["#windows", "#integrations", "#plugins"]
author: Lawrence Lane
---
There are two types of Windows plugins: Read (which allow our Windows agent to read data) and Write (which allow our Windows agent to write data). The following plugins are enabled by default:

- ReadWindowsPerfCounters
- ReadWindowsAttributes
- ReadWindowsEvents
- WriteNetuitive

This configuration is recommended for monitoring a Windows server with Metricly. Other Read/Write plugins are available as documented below (note that the Write Console plugin has no configuration settings).

## Enable/Disable  
To change which plugins are enabled, edit the **CollectdWin.config** file.

{{% notice tip %}}
The file will be located in `C:\Program Files\CollectdWin\config` or `C:\Program Files (x86)\CollectdWin\config` depending on your environment.
{{% /notice %}}


## Read Windows Performance Metrics plugin
This plugin uses the Windows Performance Count component to collect configured metrics. Each performance counter can be mapped to its Collectd equivalent metadata via configuration.

1. Navigate to the **ReadWindowsPerfCounters.config** file.
2. Add as many entries as you desire using the table below.

| Value                  | Required/Optional | Description                                                                                                                                                                                    |
|------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ReloadInterval         | Required          | The period in seconds before rescanning for new/changed instances (defaults to 3600). This is configured once in the ReadWindowsPerfCounters element.                                          |
| Category               | Required          | The name of the performance counter category.                                                                                                                                                  |
| Name                   | Required          | Comma-separated performance counter names.                                                                                                                                                     |
| Instance               | Required          | This can be set to a specific instance or a regular expression to filter the instances. Some counter categories do not have instances; in this case, this field should be left blank.          |
| CollectdPlugin         | Required          | Collectd plugin name.                                                                                                                                                                          |
| CollectdPluginInstance | Required          | Where the configuration is for a single instance, this value can be used to override the instance name. Where there are multiple instances, this value is automatically set for each instance. |
| CollectdType           | Required          | Metric type and units. This must be a value in types.db, which can be found in the deployment folder.                                                                                          |
| CollectdTypeInstance   | Required          | Name for the metric instance.                                                                                                                                                                  |
| Multiplier             | Optional          | Float scale factor to be applied to the value.                                                                                                                                                 |
| DecimalPlaces          | Optional          | Integer number of decimal places for rounding.                                                                                                                                                 |

- Here’s a default entry in the **ReadWindowsPerfCounters.config** file:

```
<Counter Category="Network Interface"
Name="Packets Received/Sec,Packets
Sent/Sec" Instance="*"
CollectdPlugin="interface"
CollectdType="if_packets"
CollectdTypeInstance="" />
```

3\. **Save** the file.

## Read Windows Event plugin
This plugin reads from the Windows event logs on the server the agent is installed. The WriteNetuitive plugin will process the values it collects, but no other write plugins are able to do so.

1. Navigate to the **ReadWindowsEvents.config** file.
2. Add as many entries as you desire using the table below:

| Value      | Required/Optional | Description                                                                                                                                                 |
|------------|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Title      | Required          | A descriptive title for the events captured by this configuration entry. This is shown as the event title in Metricly.                                      |
| Log        | Required          | The windows log (e.g., Application, System, Security).                                                                                                      |
| Source     | Required          | The source of the event (this is the source field in the event viewer). This value can be left blank for any source.                                        |
| MinLevel   | Optional          | The minimum log level to collect. Defaults to 1. Possible values (in order): 1 = critical, 2 = error, 3 = warning (warn), 4 = information, and 5 = verbose. |
| MaxLevel   | Required          | The maximum log level to collect. Offers the same levels as the MinLevel setting. Set to the same value as MinLevel to restrict to just one level.          |
| MinEventId | Optional          | The minimum event ID to collect between 0 and 65535. Defaults to 0.                                                                                         |
| MaxEventId | Optional          | The maximum event ID to collect between 0 and 65535. Defaults to 65535. Set to the same as MinEventId to restrict collection to a single event.             |
| FilterExp  | Optional          | A regular expression applied to the log message. Messages that do not match are disregarded.                                                                |

- Here’s a default entry in the **ReadWindowsEvents.config** file:

```
<Event Title="Error 99 occurred in MyApp"
Log="Application" Source="MyApp"
MinLevel="2" MaxLevel="2" MinEventId="99"
MaxEventId="99" />
```

3\. **Save** the file.

## Read Windows Attribute plugin
This plugin reads non-numeric attributes of the server. The WriteNetuitive plugin will process the values it collects, but no other write plugins are able to do so. Three attributes are available by default:

| Name      | Description                   |
|-----------|-------------------------------|
| os        | The operating system version. |
| cpus      | The number of CPUs.           |
| ram bytes | Total system RAM.             |

If the server is hosted on an AWS EC2 and the **ReadEC2InstanceMetadata** attribute on the _ReadWindowsAttributes_ element is set to `true`, the plugin will read metadata from the host EC2 instance as attributes (e.g., `instanceId`, `instanceType`, etc.) and also record the relationship between the two elements in Metricly.

Any environment variable can be read as an attribute by adding it to the configuration section:

1. Navigate to the **ReadWindowsAttributes.config** file.
2. Following the format of the other available attributes, add as many attributes as you desire.


```
<EnvironmentVariable Name="architecture"
Value="PROCESSOR_ARCHITECTURE"/>
```
3\. **Save** the file.

## Read StatsD Plugin
The Read StatsD plugin implements the StatsD Network Protocol. It listens on
a UDP port and receives metrics from applications. The plugin supports four
event types:

### Gauges
A gauge is an instantaneous measurement of a value. It differs from
a counter by being calculated at the client rather than the server.

```
<metric name>:<value>|g
```

### Counters

A counter is a gauge calculated at the server. Metrics sent by the
client increment or decrement the value of a gauge rather than
giving its current value. Counters may also have an associated
sample rate given as a decimal of the number of samples per event
counter.

```
<metric name>:<value>|c[|@<sample rate>]

```

### Timers
A timer is a measure of the number of milliseconds elapsed between a
start and end time.

```
<metric name>:<value>|ms

```

### Sets
Unique occurrences of events within an interval.

```
uniques:765|s
```
#### Properties Available
Several properties are available by default:

| Name                                                                | Description                                                          |
|---------------------------------------------------------------------|----------------------------------------------------------------------|
| Statsd.Host                                                         | Host name for StatsD UDP listener.                                   |
| Statsd.Port                                                         | Port number for StatsD UDP listener.                                 |
| DeleteCache.Counters, DeleteCache.Timers, DeleteCache.Gauges,       |                                                                      |
| DeleteCache.Sets                                                    | This option controls the behavior when metrics are not updated in an |
| interval. If set to false, metrics are dispatched unchanged. If set |                                                                      |
| to true, metrics are not dispatched and removed from the internal   |                                                                      |
| cache.                                                              |                                                                      |
| Timer.Lower, Timer.Upper, Timer.Sum, Timer.Count                    | This option is to enable aggregate functions for timer metrics. If   |
| enabled for each timer metric, its equivalent aggregate metric is   |                                                                      |
| also dispatched with appropriate extensions (“-lower”, “-upper”,    |                                                                      |
| “-sum”, “-count”).                                                  |                                                                      |
| Percentiles.Percentile                                              | Calculate and dispatch the configured percentile, i.e. compute the   |
| latency so that Percent of all reported timers are smaller than or  |                                                                      |
| equal to the computed latency. If enabled for each time metric, its |                                                                      |
| equivalent percentile metric is also dispatched with appropriate    |                                                                      |
| extensions (“-percentile-90”, “-percentile-95”). If not configured, |                                                                      |
| no percentile is calculated or dispatched.                          |                                                                      |

#### Configure

1. Navigate to the **ReadStatsD.config** file.
2. Following the format of the default configuration, manipulate the
properties as desired.
3. **Save** the file.

## Write Netuitive plugin
This plugin is already configured to send all data gathered by the read plugins to Metricly via its REST API in step 2 of the installation instructions. The following are additional, advanced settings that should only be changed in discussion with Metricly support.

| Name        | Description                                                                                                                     |
|-------------|---------------------------------------------------------------------------------------------------------------------------------|
| Url         | Metricly ingest API URL.                                                                                                        |
| PayloadSize | (Optional) The number of metrics that are batched into a single POST. Set to -1 to send all metrics at once; the default is 25. |
| Location    | (Optional) Sets element location attribute.                                                                                     |
| Type        | (Optional) Overrides the element type in Metricly; the default is WINSRV.                                                       |

### Configure

1. Navigate to the **WriteNetuitive.config** file.
2. Add any of the optional configuration attributes to the line in the file.

Example with API Key
```
<WriteNetuitive
 Url="https://api.app.metricly.com/ingest/windows/de2b497468d863accb9c402dfff22689"/>
```

3\. **Save** the file.


## Write StatsD plugin
The Write StatsD plugin posts metrics as UDP datagrams to a StatsD server. The metric buckets follow the naming convention:

```
[Prefix].[Hostname].[CollectdPlugin].[CollectdPluginInstance].[
  CollectdTypeInstance]
```
Three attributes are available by default:

| Name   | Description                             |
|--------|-----------------------------------------|
| Host   | Statsd hostname.                        |
| Port   | UDP Port number.                        |
| Prefix | (Optional) Optional bucket name prefix. |

### Configure

1. Navigate to the **WriteStatsd.config** file.
2. Add any of the optional configuration attributes to the line in the file.
3. **Save** the file.

## Write HTTP plugin
The Write HTTP plugin works similarly to the collectd Write HTTP plugin. It posts metrics to the target URL in the following JSON format.

```
[
      {
        "values": [197141504, 175136768],
    	"dstypes": ["counter", "counter"],
    	"dsnames": ["read", "write"],
    	"time": 1251533299,
    	"interval": 10,
    	"host": "leeloo.lan.home.verplant.org",
    	"plugin": "disk",
    	"plugin_instance": "sda",
    	"type": "disk_octets",
    	"type_instance": ""
      },
      ...
    ]
```

### Configure

1. Navigate to the **WriteHTTP.config** file.
2. Update the **Url** attribute to the target URL.
3. **Save** the file.

## Write AMQP plugin
The Advanced Messaging Queuing Protocol (AMQP) is an open standard application layer protocol for message-oriented middleware. The Write AMQP plugin publishes metrics to the configured message broker in JSON format. Several attributes are available by default:

| Name             | Description                                                                                                                                                                                                                           |
|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Name             | Name of the AMQP publisher.                                                                                                                                                                                                           |
| Host             | Message broker’s host name.                                                                                                                                                                                                           |
| Port             | Message broker’s AMQP listening port.                                                                                                                                                                                                 |
| VirtualHost      | The name of the “virtual host” (or vhost) that specifies the namespace for entities (exchanges and queues) referred to by the protocol. Virtual hosts provide a way to segregate applications using the same message broker instance. |
| User             | User name for authentication.                                                                                                                                                                                                         |
| Password         | Password for authentication.                                                                                                                                                                                                          |
| Exhange          | Exchanges are AMQP entities where messages are sent. Exchanges take a message and route it into zero or more queues.                                                                                                                  |
| RoutingKeyPrefix | A message sent to a message broker contains a routing key and message body.                                                                                        |

### Configure

1. Navigate to the **WriteAMQP.config** file.
2. Add any of the optional configuration attributes to the Publishline in the file.
3. **Save** the file.
