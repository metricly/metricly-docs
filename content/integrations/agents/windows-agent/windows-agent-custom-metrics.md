---
title: "Custom Metrics"
#date: 2018-12-11
draft: false
tags: ["#windows", "#integrations", "#custom metrics", "#metrics"]
author: Lawrence Lane
---
You can create additional Windows performance counters to add custom metrics monitored by Metricly.

## Add Custom Metrics

### 1. Open the Add Counters window
1. Open **perfmon** (Performance Monitor) on your computer.
2. Click **Performance Monitor** in the Monitoring Tools folder. A graph generates.
3. Click **Add**  above the graph. An “Add Counters” window opens. Leave the window open.

### 2. Prepare a new Counter
1. Navigate to the **ReadWindowsPerfCounters** file (`C:\Program Files\CollectdWin\config`) and open it.
2. Optionally, at the top of the file but below the <Counters> tag, place a comment to section off your new custom category of counters.

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

![processor screenshot](/images/windows-agent-custom-metrics/processor-screenshot.png)

2\. Navigate to the **types.db** file (`C:\Program Files\CollectdWin`) and open it.  
3. Use your best judgment to match a type in types.db to the category you selected in step 3.1. Input the type (case sensitive) you wish to use into the **CollectdType** field.
4. Create a metric category for the **CollectdPlugin** field. This category displays in the Metrics tree and search field (squared in green).
![Metricly Search Screenshot](/images/windows-agent-custom-metrics/metricly-search-screenshot.png)
5. Create a metric name using the** CollectdTypeInstance** field. This field is used as the metric’s name in Metricly, but be sure to make it entirely unique.
6. Save the **ReadWindowsPerfCounters** file.


#### About Categories

Not all categories have instances available. In the above example, the instances correlate to the processor’s cores, where `_Total` would calculate the metric selected for all four cores. Options you can use for the Instance field:

- `“”` for no specific instances.
- `_Total` for an aggregate of all instances.
- `.*` to make a branch for each instance.
- `{specific_instance_name}` for only a specific instance.
