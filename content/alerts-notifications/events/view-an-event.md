---
title: "View an Event"
date: 2018-04-12
draft: false
categories:
tags: ["alerts", "notifications", "events" ]
author: Lawrence Lane
weight: 1
---

The following tools allow you to view and analyze events in the Metricly UI:

- **Event Explorer**: Event Explorer displays a comprehensive list of all the events in your environment. You can filter the list by the event category, source (Metricly or External), element, element type, and/or tag of the element(s) to which an event is associated. You can also filter events within a specific time frame. For more information about Event Explorer, see below.
- [**Metrics page**][1]: Metrics page displays the events and metric data for a specified element. The amount of data displayed can be limited by selecting a time frame setting and by showing or hiding metric charts. For more information about Metrics page, see Metrics page.

## Event Explorer
Event Explorer allows you to view, search, and analyze events.

{{% notice tip %}}
If one of your policies is particularly noisy, you can delete all events associated with the policy. See **Create or Edit a Policy** for more information.
{{% /notice %}}

![Event Explorer ](/images/view-an-event/event-explorer.png)

1. **Search**: Contains several filters where you can search for Event (i.e. the policy that created the event), event category, source (Metricly or External), element, element type, Element tag, and/or Event tag. Expand the More filter to see additional filters; select a filter to add it to the list of active filters. For more information on creating event tags, see the external events section below.
2. **Events list**: The Events list lists events by the date and time they occurred, the name of the policy that generated the event, the event category, the source of the event (Metricly or External), the name of the element(s) to which they are associated, and the type of the element(s) to which they are associated. Click the name of the policy in the Event column to view the violating metrics on the Metrics page (source = Metricly) or the event message (source = External). Click the Element’s name to view the element’s Element Detail panel. You can also navigate to Policy Editor to edit the policy associated with the event by clicking the Event name (events from Metricly only).
3. **Events graph**: The Events graph displays the events in your environment based on the Time Frame setting and other search filters. Click an event to have the option of viewing the violating metrics on the Metrics page or edit the policy the event is associated with.
4. **Time Frame**: The Time Frame controls the range of data displayed. To refresh data, click the refresh  button. Selecting “1w” in the Time Frame displays the most recent week of data and/or elements. By selecting “Ending Now,” you can specify a range of data beginning with a date other than today. For more information, see Time Frame.


[1]: /data-visualization/metrics/metric-page
[2]: /data-visualizaiton/metrics/create-edit-policies
