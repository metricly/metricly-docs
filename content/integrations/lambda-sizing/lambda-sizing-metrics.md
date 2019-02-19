---
title: "Metrics"
#date: 2018-12-11
draft: false
tags: ["#metrics", "#integrations", "#lambda" ]
author: Lawrence Lane
---

## Collected

| Parameters | Required/Optional | Description |
|------------|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id | Required | URL (path) parameter. The ID of the element. |
| levels | Optional | The number of levels of relationships returned, e.g., 2 would return an element related to a listed element related to the given element. |
| startTime | Optional | Query parameter. The start of the window of time from which elements will be returned. The startTime must be in ISO 8601 format. The default startTime is 12:00 AM in the authenticating user’s specified time zone. |
| endTime | Optional | Query parameter. The end of the window of time from which elements will be returned. The endTime must be in ISO 8601 format. The default endTime is the current time. |
