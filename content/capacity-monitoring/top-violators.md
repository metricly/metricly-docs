---
title: "Top Violators"
#date: 2018-04-12
draft: false
categories:
tags: ["alerts", "notifications", "events", "policies"]
author: Lawrence Lane

---
Top Violators reports display the elements in your environment that have triggered the most events within the specified Time Frame setting, allowing you to quickly locate the elements with high event counts. This report provides the same type of data as the Event Explorer, but the data is grouped by element.

![Top Violators](/images/top-violators/top-violators.png)

1. **Summary Table**: This table provides both the number of events triggered by each element (Event Count), and the amount of time that each element triggered events within the specified Time Frame. Click the Element’s name to view the element’s Element Detail panel, or click the event count to view events in the Event Explorer.


{{% notice tip %}}
For example, if the Event Count for an element is 50 and the Time Violating During 7 Days is one hour, then the element triggered 50 events in one hour during the past 7 days.
{{% /notice %}}

2. **Filters**: Contains several filters where you can search for element names, element types, tags, attributes, collectors, and more. Expand the More filter to see additional filters; select a filter to add it to the list of active filters.
3. **Time Frame Controls**: The Time Frame controls the range of data displayed. To refresh data, click the refresh  button.Selecting “1w” in the Time Frame displays the most recent week of data and/or elements. By selecting “Ending Now,” you can specify a range of data beginning with a date other than today. For more information, see Time Frame.
4. **Pie Chart**: The pie chart shows the total number of events by category for all elements that triggered an event within the specified Time Frame setting.
