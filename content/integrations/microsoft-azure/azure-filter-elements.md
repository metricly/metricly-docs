---
title: "Filter Elements"
date: 2018-12-11
draft: true
categories: ["integration", "admin guide", "getting started"]
tags: ["microsoft", "azure", "integrations", "optional config"]
author: Lawrence Lane
---
You can filter what Azure elements are included in Metricly’s monitoring by using regex to match key-value pairs. Metricly offers opt-in (include) or opt-out (exclude) element filtering.

## Using opt-in filtering
1. In your Azure portal, create or choose an existing tag (key-value pair). Then, assign the tag to the Azure elements you do not want Metricly to monitor.
2. In Metricly, navigate to your **Azure integration** card. Expand the element types you want to filter. Key-value pair fields display.
![Azure vm expand filters](/images/azure-filter-elements/azure-vm-expand-filters.png)
3. Select the **Filtering** checkbox.
4. Select **Include**. Type the proper `Regex` to match the tag(s) you created in your Azure portal for each element type you want to filter.
5. Click **Save**.

## Using opt-out filtering
1. In your Azure portal, create or choose an existing tag (key-value pair). Then, assign the tag to the Azure elements you do not want Metricly to monitor.
2. In Metricly, navigate to your **Azure integration** card. Expand the element types you want to filter. Key-value pair fields display.
![Azure vm expand filters](/images/azure-filter-elements/azure-vm-expand-filters.png)
3. Select the **Filtering** checkbox.
4. Select **Exclude**. Type the proper `Regex` to match the tag(s) you created in your Azure portal for each element type you want to filter.
5. Click **Save**.

## Using Regex
Check out our [Regex Guide][1] for some examples.

[1]: /alerts-notifications/policies/regex-guide
