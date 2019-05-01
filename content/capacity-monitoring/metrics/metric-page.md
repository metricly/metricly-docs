---
title: "Page Features"
#date: 2018-12-03
draft: false
categories:
tags: ["#getting started", "#metrics",]
author: Lawrence Lane
---
## Sub Navigation
### Filters
![Metric Page Features](/images/metric-page/metric-page-features.png)  

- **Name Contains**: Specific search based on name  
-  **Search Metrics**: Broad filter based on metric type, provided in tree and list form
- **Element, Type, More**:  Additional expandable filter options  
- **Grouped By**: Contains a menu of all quick groups, tags, and attributes available to Metricly. After you’ve rendered some metric charts, choose one of the groupings and Metricly will automatically group the metric charts based on your selection.

{{% notice note %}}
If you chose to display all EC2 metrics and then grouped by instance ID, each instance’s set of metrics would be grouped in a section together under the instance’s ID.
{{% /notice %}}

Once you have added all needed search criteria, click **Render Charts** to populate results.

#### Quick Filters / Metric Charts
Click a **Quick Filter** to render metric charts automatically for the selected filter. Metric charts are a visualization of a metric for an element. See [below][1] to learn more.

### Events Graph
The Events graph displays the events in your environment based on the Time Frame setting and other search filters. For more information, see Events graph. Click an event to have the option of viewing the violating metrics on the Metrics page or edit the policy the event is associated with.

![Events Graph](/images/metric-page/events-graph.png)


### Metric Chart Size
Select how wide or how tall you want your metric charts to be.
![Change Chart Size](/images/metric-page/change-chart-size.png)

### Time Frame Controls
The Time Frame controls the range of data displayed. To refresh data, click the refresh button. Selecting “1w” in the Time Frame displays the most recent week of data and/or elements. By selecting “Ending Now,” you can specify a range of data beginning with a date other than today. For more information, see Time Frame.


### Data Aggregation
Select the type of data displayed on the metric charts.

| Option                                                                         | Description                                                                                                                     |
|--------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Raw                                                                            | Shows data that has not been aggregated by Metricly. Computed metrics do not have raw data because they are calculated by Metricly.                                |
| 5 Min                                                                          | Displays aggregate data that Metricly generates by averaging the data collected from a given integration at 5 minute intervals. |
| 1 Hour                                                                         | Displays aggregate data that Metricly generates by averaging the data collected from a given integration at 1 hour intervals.   |
