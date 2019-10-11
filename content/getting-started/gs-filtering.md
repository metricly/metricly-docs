---
title: "In-App Filtering"
#date: 2018-12-3
description: How to filter metrics and elements in the Metricly UI.
draft: false
categories:
tags: ["#getting started", "#filtering", "#widgets", "#reports", "#policies", "#metrics", "#alerts"]
author: Lawrence Lane
pre:
weight: 4
---
Learning the basics of in-app filtering enables you to easily create/edit **widgets**, **reports**, and **policies**---as well as filter **metrics** and **alerts**.

## Filter Types

There are several types of filters used in Metricly. Each one provides a unique perspective into your environment.

### Inclusion Filters  

Inclusion filters limit the scope of your search results to a set of items matching a given criteria, such as an `element name` or `tag value`. This filter is best used when you have a few, specific items you want selected.

#### Inclusion Filter Examples

- **Name contains**: A search field that returns a list of items with names including the value provided (e.g., `ECS-spot`).
- **Element**: A dropdown multi-select of all elements; includes a search field.  
- **Type**: A dropdown multi-select of all element types; includes a search field.
- **Attribute**: A dropdown multi-select of all attributes; includes a search field and all/any option.
- **Tag**: A dropdown multi-select of all tags; includes a search field and all/any option.
- **Collector**: A dropdown multi-select of all collectors; includes a search field.

![inclusion-filters](/images/gs-filtering/inclusion-filters.png)

### Exclusion Filters

Exclusion filters limit the scope of your search results to everything _except_ the selected items that match a given criteria. For example, excluding the App tag `VPN` would return a list of all elements which **do not include** the VPN tag. This filter is best used when you want the bulk of given elements available--except for those with certain attributes or tags.

#### Exclusion Filter Examples

- **Name excludes**: A search field that removes items from a displayed list which match the value provided (e.g., `EC2`).
- **Exclude Attribute**: A dropdown multi-select of all excludable attributes ; includes a search field and all/any option.
- **Exclude Tag**: A dropdown multi-select of all excludable tags; includes a search field and all/any option.

![exclusion-filters](/images/gs-filtering/exclusion-filters.png)

### All vs Any Filters

All vs Any Filters are available on a subset of filters in Metricly. These filters allow you to select multiple tags or attributes and determine whether the search results return items that include _all_ tags/attributes included (AND operator), or just _any one_ of them (boolean OR operator).

#### All vs Any Examples
- **Attribute**: A dropdown multi-select of all attributes; includes a search field and all/any option.
- **Tag**: A dropdown multi-select of all tags; includes a search field and all/any option.

![all-vs-any-filters](/images/gs-filtering/all-vs-any-filters.png)
