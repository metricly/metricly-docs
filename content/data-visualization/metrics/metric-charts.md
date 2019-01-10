---
title: "Chart Features"
#date: 2018-12-03
draft: false
categories:
tags: ["#getting started", "#metrics", "#charts",]
author: Lawrence Lane
---

# Metric Charts
Metric charts on the Metrics page allow you to view time-series data collected on [elements][2] in your environment. The range of data shown in metric charts corresponds to the range of data shown in the Events graph. This allows you to compare event data to the metric behavior that caused it.

## Metric Metadata
Click the **`metric name`** to open the metric metadata panel.
![Metric Metadata Modal](/images/metric-page/metric-metadata-modal.png)

| Metadata       | Description                                                                                                                                           |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| Avg            | The average value recorded in the last cycle.                                                                                                         |
| Baselined      | If the Baseline Band analysis is enabled or disabled for the metric.                                                                                  |
| Correlated     | If the Contextual Band analysis is enabled or disabled for the metric.                                                                                |
| Count          | The amount of values recorded in the last cycle.                                                                                                      |
| Created        | When the metric was created.                                                                                                                          |
| Element Detail | Opens that element’s [Element Detail panel][3] in the Inventory Explorer.                                                                             |
| FQN            | The fully qualified name (FQN) of the metric.                                                                                                         |
| Historical Max | Historically, the highest value the metric has experienced.                                                                                           |
| Historical Min | Historically, the lowest value the metric has experienced.                                                                                            |
| ID             | The full ID of the metric.                                                                                                                            |
| Max.           | The maximum value recorded in the last cycle.                                                                                                         |
| Min.           | The minimum value recorded in the last cycle.                                                                                                         |
| Sparse Mode    | Defines the strategy for replacing missing data. Either missing data is replaced with a zero (ReplaceWithZero) or no strategy is taken at all (None). |
| Sum            | The sum of values recorded in the last cycle.                                                                                                         |
| Type           | The type of metric; currently, the only two values are “collected” or “computed.”                                                                     |
| Units          | The type of measurement the metric is collected in.                                                                                                   |
| Updated        | The time the last five-minute cycle occurred in which the data was updated.                                                                           |
| Valid Max      | If set, the valid maximum value the metric can have.                                                                                                  |
| Valid Min      | If set, the valid minimum value the metric can have.                                                                                                  |
| Value Used     | The type of aggregation used in the analysis cycle                                                                                                    |



## Metric Submenu
![Metric Submenu](/images/metric-page/metric-submenu.png)

 - **Metric Unit**: Change the displayed unit (UI only; does not affect default unit metadata).
 - **Aggregation(s**): Select which aggregate values you want to display on the metric chart. Avg is the default. Each aggregation corresponds to a different color. Computed metrics do not have aggregations available.
 - **Download Buttons**: Download the current chart for this metric to a .png, .jpg, or .svg file.
 - **Add to Dashboard**: Add any metric chart to the desired dashboard as a single metric time series widget (see below).
 - **Other Elements with this Metric**: View other elements with the same metric and open the respective elements’ metric chart (see below).




[1]: adfafa
[2]: adfa
[3]: adfa
