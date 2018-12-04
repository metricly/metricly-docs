---
title: "Chart Features"
date: 2018-12-03
draft: true
categories:
tags: ["getting started", "metrics",]
author: Lawrence Lane
---

# Metric Charts
Metric charts on the Metrics page allow you to view time-series data collected on [elements][2] in your environment. The range of data shown in metric charts corresponds to the range of data shown in the Events graph. This allows you to compare event data to the metric behavior that caused it.

## Metric Metadata
Click the **`metric name`** to open the metric metadata panel.
![Metric Metadata Modal](/images/metric-page/metric-metadata-modal.png)

## Element
Click the **`element name`** to open that element’s [Element Detail panel][3] in the Inventory Explorer.

## Metric Submenu
![Metric Submenu](/images/metric-page/metric-submenu.png)

 - **Metric Unit**: Change the displayed unit (UI only; does not affect default unit metadata).
 - **Aggregation(s**): Select which aggregate values you want to display on the metric chart. Avg is the default. Each aggregation corresponds to a different color. Computed metrics do not have aggregations available.
 - **Download Buttons**: Download the current chart for this metric to a .png, .jpg, or .svg file.
 - **Add to Dashboard**: Add any metric chart to the desired dashboard as a single metric time series widget (see below).
 - **Other Elements with this Metric**: View other elements with the same metric and open the respective elements’ metric chart (see below).

## Add a Metric Chart to a Dashboard

### Add as Single Metric Widget
1. Open the Metric chart sub-menu {{< icon name="option-horizontal" size="large" >}}.
2. Click **Add to Dashboard**.
3. In the** Add to Dashboard** window, click Dashboards and select a dashboard or type to search.
4. Change the widget name if desired.
5. Click **Save**.
6. The widget is now available on the selected dashboard.


### Add as Multi-Metric Widget
1. Merge as many metrics as desired.
2. Open the Metric Chart sub-menu {{< icon name="option-horizontal" size="large" >}}.
3. Click **Add to Dashboard**.
4. In the **Add to Dashboard** window, click **Dashboards** and select a dashboard or type search.
5. Change the widget name if desired.
6. Click **Save**.
7. The widget is now available on the selected dashboard


## View Charts of Same Type on Other Elements
1. Open the Metric Chart sub-menu {{< icon name="option-horizontal" size="large" >}}.
2. Click Other Elements with this Metric.
3. Select as many elements as desired.
 - Click All to select all the elements with the selected metric.
 - Click None to clear all elements with the selected metrics.
 - You can also search for an element using the Search Elements field.
4. Click Done. The metric charts open in the Metrics page.


[1]: adfafa
[2]: adfa
[3]: adfa
