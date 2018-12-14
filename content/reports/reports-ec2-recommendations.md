---
title: "EC2 Recommendations"
#date: 2018-12-03
draft: false
categories:
tags: ["reports", "ec2" ]
author: Lawrence Lane
---

The EC2 Recommendation report is designed to help you reduce EC2 instance running costs by suggesting alternative instance types that may provide a similar level of service at a lower cost. The report presents details on the current EC2 instance types and their respective memory, VCPUs, and hourly instance running costs. Using these characteristics and the utilization observed during the reporting period, it estimates the memory and number of VCPUs that are actually needed, subject to optional constraints such as CPU utilization not exceeding a particular level, etc.

The report defaults to showing the top 10 savings opportunities, but this can be adjusted in combination with element filters to find and highlight additional savings.

## Report Features
Refer to the image above when reading these sections.

### (1) Graph
The graph displays two markers (connected by a dotted line) for each instance in the summary table below it. The solid marker represents the current state of the element: aggregated CPU utilization for the instance vs. estimated weekly instance cost. The empty marker shows the projected state of the instance for the same period it had been of the proposed type. The length of the dotted line connecting the two markers can be a useful indicator: a longer line represents significant changes. Conversely if the two markers coincide exactly, then the proposed type is the same as the current type. The direction of the line us useful too: a vertical line indicates a change in price without an expected change in utilization whereas a horizontal line suggests a change in utilization without a change in prices.The graph can be adjusted to show CPU vs. Cost, Memory vs. Cost, or CPU vs. Memory, or it can be also be hidden to make room for a larger table.

### (2) Summary Table
This table shows information about the current and proposed instance types.

### (3) View Options
These options let you tune the recommendations generated in the chart and graph.

**Show**: Allows you to choose the number of elements to display on the graph and in the table. The Estimated Weekly Instance Savings value only includes savings for the filtered element set.

**Chart View**: Changes the axes on the graph to help you visualize the impact of changing instance types on cost, CPU utilization, and memory utilization.

- Cost vs. CPU Utilization
- Cost vs. Memory Utilization
- CPU vs. Memory Utilization
- None (hides the graph)

**Metric Statistic**: Changes the aggregated CPU and/or Memory statistic used to determine the peak observed load during the reporting period.

- Maximum:  This is the most conservative; at no time during the report period did the CPU or memory exceed this value.
- 95th Percentile: This is slightly more aggressive: 95% of the time the CPU and memory utilization were at or below this level.
- 75th Percentile
- Mean
- Median
- 5th Percentile
- Minimum

**Family Constraint**: Determines which instance types are considered possible alternatives to the current instance type.

- Any Family: There are no constraints on the instance types other than they must have the calculated minimum VCPUs and Memory.
- Same Family: The proposed instance type must be in the same family as the current type. For example, if the current type is in the Compute Optimized family, then the proposed must be as well.
- Same Family and Generation: In addition to being in the same family, the new type must also be of the same generation. For example, an `m4.2xlarge` can be switched to an `m4.xlarge` but not an `m3.xlarge`.

**Maximum CPU Utilization**: The maximum CPU Utilization percent allowed in calculating for projections. Note that 100% is the most aggressive setting and results in instances with fewer VCPUs (normally cheaper). Instance types with enough VCPUs to keep the projected CPU utilization below 100% are OK. Also note that 50% is the most conservative setting and results in instances with more VCPUs.

**Maximum Memory Utilization**: The maximum Memory Utilization percent allowed in calculating for projections. Note that 100% is the most aggressive setting and results in instances with lower memory (normally cheaper). Instance types with enough memory to keep the projected memory utilization below 100% are OK. Also note that 50% is the most conservative setting and results in instances with more memory.

**Assumed Memory**: The amount of Memory Utilization percent to assume when no agent (Linux / Windows) is installed on the EC2 and hence Metricly does not have memory utilization data. Below is some contextual information included with a few of the options available in the drop-down menu to help you make an informed choice:

- Use CPU Utilization — In this case, the report takes the observed CPU utilization for the period and uses this figure for the memory also.
- 100% — This is the most conservative setting; we assume that at some point during the reporting period the memory utilization reached 100% and use this as the measure to determine the required memory.
- 50% — This is the most aggressive setting; we assume that the highest memory utilization reached during the reporting period was 50% and use this as the measure to determine the required memory.

### (4) Filters
Contains several filters where you can search for element names, element types, tags, attributes, collectors, and more. Expand the More filter to see additional filters; select a filter to add it to the list of active filters.

### (5) Estimated Weekly Savings
The estimated potential savings calculated by the report based on switching to the proposed instance types. A negative number indicates that the report is suggesting more expensive instance types. This can occur if you set utilization targets that are lower than the current level of utilization.
