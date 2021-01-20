---
title: "Custom Metrics"
#date: 2018-12-11
draft: false
tags: ["#windows", "#integrations", "#custom metrics", "#metrics"]
author: Lawrence Lane
---

Custom Metrics are enabled by Windows plugins. There are two types of Windows plugins: Read (which allow our Windows agent to read data) and Write (which allow our Windows agent to write data). The following plugins are enabled by default:

- ReadWindowsPerfCounters
- ReadWindowsAttributes
- WriteNetuitive

This configuration is recommended for monitoring a Windows server with CloudWisdom. Other Read/Write plugins are available as documented below (note that the Write Console plugin has no configuration settings).

## Enable/Disable  
To change which plugins are enabled, edit the **CollectdWin.config** file.

{{% notice tip %}}
The file will be located in `C:\Program Files\CollectdWin\config` or `C:\Program Files (x86)\CollectdWin\config` depending on your environment.
{{% /notice %}}


## Read Windows Performance Metrics plugin
This plugin uses the Windows Performance Count component to collect configured metrics. Each performance counter can be mapped to its Collectd equivalent metadata via configuration.

### 1. Open the Add Counters window
1. Open **perfmon** (Performance Monitor) on your computer.
2. Click **Performance Monitor** in the Monitoring Tools folder. A graph generates.
3. Click **Add**  above the graph. An “Add Counters” window opens. Leave the window open.

### 2. Prepare a new Counter
1. Navigate to the **ReadWindowsPerfCounters** file (`C:\Program Files\CollectdWin\config`) and open it.
2. Optionally, at the top of the file but below the <Counters> tag, place a comment to section off your new custom category of counters.
`<!-- CustomCategoryName -->`
3. Add a blank Counter tag template:

```
<Counter
  Category=""
  Name=""
  Instance=""
  CollectdPlugin=""
    CollectdType=""
    CollectdTypeInstance=""
/>
```

##### **Values**

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

### 3. Fill in Counter information
1. Follow the diagram below to fill out the Category, Name, and Instance fields (case sensitive) in the blank counter template you added in step 2.3. The picture outlines the expanded Processor counter category.
  ![processor screenshot](/images/windows-agent-custom-metrics/processor-screenshot.png)

2. Navigate to the **types.db** file (`C:\Program Files\CollectdWin`) and open it.  
3. Use your best judgment to match a type in types.db to the category you selected in step 3.1. Input the type (case sensitive) you wish to use into the **CollectdType** field.
4. Create a metric category for the **CollectdPlugin** field. This category displays in the Metrics tree and search field (squared in green).
![CloudWisdom Search Screenshot](/images/windows-agent-custom-metrics/metricly-search-screenshot.png)
5. Create a metric name using the** CollectdTypeInstance** field. This field is used as the metric’s name in CloudWisdom, but be sure to make it entirely unique.
6. Save the **ReadWindowsPerfCounters** file.


### About Categories

Not all categories have instances available. In the above example, the instances correlate to the processor’s cores, where `_Total` would calculate the metric selected for all four cores. Options you can use for the Instance field:

- `“”` for no specific instances.
- `_Total` for an aggregate of all instances.
- `.*` to make a branch for each instance.
- `{specific_instance_name}` for only a specific instance.

## Read Windows Attribute plugin
This plugin reads non-numeric attributes of the server. The WriteNetuitive plugin will process the values it collects, but no other write plugins are able to do so. Three attributes are available by default:

| Name      | Description                   |
|-----------|-------------------------------|
| os        | The operating system version. |
| cpus      | The number of CPUs.           |
| ram bytes | Total system RAM.             |

If the server is hosted on an AWS EC2 and the **ReadEC2InstanceMetadata** attribute on the _ReadWindowsAttributes_ element is set to `true`, the plugin will read metadata from the host EC2 instance as attributes (e.g., `instanceId`, `instanceType`, etc.) and also record the relationship between the two elements in CloudWisdom.

Any environment variable can be read as an attribute by adding it to the configuration section:

1. Navigate to the **ReadWindowsAttributes.config** file.
2. Following the format of the other available attributes, add as many attributes as you desire.


```
<EnvironmentVariable Name="architecture"
Value="PROCESSOR_ARCHITECTURE"/>
```
3\. **Save** the file.



## Write Netuitive plugin
This plugin is already configured to send all data gathered by the read plugins to CloudWisdom via its REST API in step 2 of the installation instructions. The following are additional, advanced settings that should only be changed in discussion with Virtana support.

| Name        | Description                                                                                                                     |
|-------------|---------------------------------------------------------------------------------------------------------------------------------|
| Url         | CloudWisdom ingest API URL.                                                                                                        |
| PayloadSize | (Optional) The number of metrics that are batched into a single POST. Set to -1 to send all metrics at once; the default is 25. |
| Location    | (Optional) Sets element location attribute.                                                                                     |
| Type        | (Optional) Overrides the element type in CloudWisdom; the default is WINSRV.                                                       |

### Configure

1. Navigate to the **WriteNetuitive.config** file.
2. Add any of the optional configuration attributes to the line in the file.

Example with API Key
```
<WriteNetuitive
 Url="https://api.us.cloudwisdom.virtana.com/ingest/windows/de2b497468d863accb9c402dfff22689"/>
```

3\. **Save** the file.
