---
title: "Choose Scope"
#date: 2018-04-12
draft: false
categories:
tags: ["#alerts", "#notifications", "#events", "#policies", "#scope"]
author: Lawrence Lane
weight: 3
---
The scope of a [policy][1] defines which [element(s)][2] get assigned to that policy. A policy can use a combination of criterion to narrow its selection; for example, all elements tagged with `region-east + EC2` as a type.

## Scope Methods
When using multiple fields, an element must meet each criterion to be included in the policy’s scope.

### Name Contains or Name Excludes
- Input a string of characters into the **Name Contains** or **Name Excludes** field. The policy then includes (or excludes) all elements matching the input
- Name Excludes is located under **More** > **Name Excludes**

### Element or Exclude Element
- Search a drop-down list of all of your elements and **check** each to include (or exclude) all selections
- Input a string of characters to search

### Type, Attribute, Tag, & More
- Search a drop-down list of all each category and **check** all objects that apply to include them in the policy
- Input a string of characters to search

[1]: /capacity-monitoring/policies
[2]: /capacity-monitoring/inventory
