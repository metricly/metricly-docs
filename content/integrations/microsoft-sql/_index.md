---
title: "Microsoft SQL"
#date: 2018-12-12
draft: false
tags: ["microsoft sql", "integrations" ]
author: Lawrence Lane
---

 Microsoft SQL Server metrics come packaged with the Metricly Windows agent. Our Windows agent is a Microsoft Windows service that collects, aggregates, and publishes windows performance counters and attributes. For more information on the Agent itself as well as any plugins available, see the Windows Agent page.

## Configuration

There’s no additional configuration necessary for the Microsoft SQL Server if you’ve already installed the Windows agent unless you want to add additional custom metrics to supplement the default collected metrics.

### 1. Add Custom Metrics

1. Open the **Add Counters** window
2. Open **perfmon** (Performance Monitor) on your computer.
3. Click **Performance Monitor** in the Monitoring Tools folder. A graph generates.
4. Click **Add** above the graph. An _Add Counters_ window opens. Leave the window open.

### 2. Prepare a New Counter
1. Navigate to the **ReadWindowsPerfCounters** file (typically located in `C:\Program Files\CollectdWin\config`) and open it.
2. Optionally, at the top of the file but below the `<Counters>` tag, place a comment to section off your new custom category of counters.

```
<!-- CustomCategoryName -->
```
3\. Add a blank Counter tag template:

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

### 3. Fill in Counter information
1. Follow the diagram below to fill out the Category, Name, and Instance fields (case sensitive) in the blank counter template you added in step 2.3. The picture outlines the expanded Processor counter category.
![counter tag template](/images/_index/counter-tag-template.png)

{{% notice tip %}}
Not all categories have instances available. In the above example, the instances correlate to the processor’s cores, where `_Total` would calculate the metric selected for all four cores.
{{% /notice %}}

2\. Navigate to the **types.db** file (typically located in `C:\Program Files\CollectdWin)` and open it.  
3. Use your best judgment to match a type in `types.db` to the category you selected in step 3.1. Input the type (case sensitive) you wish to use into the **CollectdType** field.  
4. Create a metric category for the **CollectdPlugin** field. This category displays in the Metrics tree and search field.
![metric search field](/images/_index/metric-search-field.png)
5. Create a metric name using the **CollectdTypeInstance** field. This field is used as the metric’s name in Metricly, but be sure to make it entirely unique.  
6. **Save** the` ReadWindowsPerfCounters` file.

#### Example Counters

A Web Service Tracking Total Instances of Current Connections:

```
<Counter
  Category="Web Service"
  Name="Current Connections"
  Instance="_Total"
  CollectdPlugin="custom_iis"
    CollectdType="current_connections"
    CollectdTypeInstance="curr_connections"
/>
```

Three Process Counters Checking Status of different aspects of the Windows agent service:

```
<Counter
  Category="Process"
  Name="% Processor Time"
  Instance="^CollectdWinService$"
  CollectdPlugin="processes"
    CollectdPluginInstance=""
    CollectdType="percent"
    CollectdTypeInstance="collectdwin.percent_processor_time"
/>
```

```
<Counter
  Category="Process"
  Name="Thread Count"
  Instance="^CollectdWinService$"
  CollectdPlugin="processes"
    CollectdPluginInstance=""
    CollectdType="count"
    CollectdTypeInstance="collectdwin.thread_count"
/>
```

```
<Counter
  Category="Process"
  Name="Private Bytes"
  Instance="^CollectdWinService$"
  CollectdPlugin="processes"
    CollectdPluginInstance=""
    CollectdType="bytes"
    CollectdTypeInstance="collectdwin.private_bytes"
/>
```ph. An _Add Counters_ window opens. Leave the window open.
