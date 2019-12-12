---
title: "Dashboard API"
draft: false
categories:
tags: ["#api",]
author: Lawrence Lane
alwaysopen: false
pre: ""
---
## Create a Dashboard
Creating a dashboard through the API requires 3 endpoint actions.

### 1. POST to /dashboards
This creates your dashboard object. Grab its ID after you have completed this step; you need the ID to create widgets. For this example, `f1234ee1-a123-123a-1dbd-1d2b34e5f678` is the **dashboardId**.

```
{
"dashboard": {
"name": "API Test Board",
}
}
```
```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ \
 "dashboard": { \
 "name": "API Test Board" \
 } \
 }' 'https://us.cloudwisdom.virtana.com/dashboards'
 ```

### 2. POST to /widgets
Now you must create all of the widgets you wish to use for the dashboard.

```
{
  "widget":
    {
      "dashboardId": "f1234ee1-a123-123a-1dbd-1d2b34e5f678",
      "name": "CPU Utilization",
      "widgetType": "single-metric",
      "generated": "true",
      "properties": {
        "visualization": "time series",
        "showBands": "true",
        "showHighest": "true",
        "metric_fqn": "aws.rds.cpuutilization",
        "useAllMetricScopeTags": "true",
        "element_fqn": "123456789:RDS:us-east-1:colorado-mysql47",
        "useAllElementScopeAttributes": "true",
        "metricAgg": "avg",
        "topNLimit": "5"
      }
    }
}
```

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ \
   "widget":  \
     { \
       "dashboardId": "f2747ee5-a128-456a-8dbd-1d3b15e3f735", \
       "name": "cpuutilization", \
       "widgetType": "single-metric", \
       "generated": "true", \
       "properties": { \
         "visualization": "time series", \  
         "showBands": "true", \
         "showHighest": "true", \
         "metric_fqn": "aws.rds.cpuutilization", \  
         "useAllMetricScopeTags": "true", \
         "element_fqn": "502379301106:RDS:us-east-1:aurora-mysql57", \
         "useAllElementScopeAttributes": "true", \
         "metricAgg": "avg", \
         "topNLimit": "5" \
       } \
     } \
 }' 'https://us.cloudwisdom.virtana.com/widgets'
 ```

### 3. PUT to /dashboards/{Id}
Finally, update the dashboard you initially created by adding the widgets so that they render in the UI. Manipulating the **gridstackContents** arranges the ordering and sizing of the widgets.

**Required Parameters**
- `dashboardId`

```
{
  "dashboard": {
    "id": "f1234ee1-a123-123a-1dbd-1d2b34e5f678",
    "name": "API Test Board",
    "properties": {
      "timeRangeDuration": 3600,
      "refreshIntervalSeconds": 300,
      "wrap": true,
      "gridstackContents": "[{\"id\":\"ac627f78-4d28-4d53-90a7-a74c3e95895a\",\"width\":4,\"height\":7,\"x\":0,\"y\":0}]"
    }
  }
}
```

```
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: */*' -d '{ \
   "dashboard": { \
     "id": "f1234ee1-a123-123a-1dbd-1d2b34e5f678", \
     "name": "API Test Board", \
     "properties": { \
       "timeRangeDuration": 3600, \
       "refreshIntervalSeconds": 300, \
       "wrap": true, \
       "gridstackContents": "[{\"id\":\"ac627f78-4d28-4d53-90a7-a74c3e95895a\",\"width\":4,\"height\":7,\"x\":0,\"y\":0}]" \
     } \
   } \
 }' 'https://us.cloudwisdom.virtana.com/dashboards/42f718e4-b447-49c2-90e2-80844265b776'
 ```

#### gridstackContents Breakdown

The sample below reflects the screenshot included, ordered from left to right. The first section is the top row and the second section is the bottom row. **Minimum Width**: 2; **Minimum Height**: 6.

```
"gridstackContents": "[
{\"id\":\"{id}\",\"x\":0,\"y\":0,\"width\":2,\"height\":6},
{\"id\":\"{id}\",\"x\":2,\"y\":0,\"width\":2,\"height\":6},
{\"id\":\"{id}\",\"x\":4,\"y\":0,\"width\":2,\"height\":6},
{\"id\":\"{id}\",\"x\":6,\"y\":0,\"width\":2,\"height\":6},
{\"id\":\"{id}\",\"x\":8,\"y\":0,\"width\":2,\"height\":6},
{\"id\":\"{id}\",\"x\":10,\"y\":0,\"width\":2,\"height\":6},

{\"id\":\"{id}\",\"x\":0,\"y\":6,\"width\":3,\"height\":6},
{\"id\":\"{id}\",\"x\":3,\"y\":6,\"width\":2,\"height\":7},
{\"id\":\"{id}\",\"x\":5,\"y\":6,\"width\":2,\"height\":9},
{\"id\":\"{id}\",\"x\":7,\"y\":6,\"width\":5,\"height\":10}]"
```
![grid-stack-example](/images/dashboards/grid-stack-example.png)

## Methods

| Header Name          | Header Value                          |
|----------------------|---------------------------------------|
| Content-Type         | application/json                      |
| Authorization: Basic | (Base64 encoded authentication value) |

### POST  to /dashboards
Creates a dashboard.

**Body Attributes**

| Attribute | Required/Optional | Description |
|--------------|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| created | Optional | The time the dashboard was created. This must be in ISO 8601 format. |
| creatorEmail | Optional | The email of the user who created the dashboard. |
| description | Optional | The description of the dashboard. |
| id | Optional | The ID of the dashboard. |
| layout | Optional | Specifies the layout of the dashboard’s row(s). Layout contains a single attribute: contents (optional) Array of JSON objects that correspond to each row on a dashboard. Within each JSON object there are several options: widgets (optional), which contains IDs for the widgets within the row. height (optional), which is the height setting for the row (small, medium, large, xlarge, or custom). customHeight (optional, which corresponds to the custom height setting. This number is the height in pixels (px) for the row. |
| name | Optional | The name of the dashboard. |
| private | Optional | Whether the dashboard is public or private. |
| properties | Optional | The properties for the dashboard. Propertiescontains several options: timeRangeDuration (optional) The timeframe setting. wrap (optional) Whether the dashboard rows wrap. |
| updated | Optional | The time the dashboard was last updated. This must be in ISO 8601 format. |
| userId | Optional | The ID of the user who created the dashboard. |
| widgets | Optional | A list of the widgets that are contained in the dashboard. |

### PUT to dashboards/{dashboardId}
Updates a dashboard.

| Parameters | Required/Optional | Description |
|------------|-------------------|----------------------------|
| dashboard | Required | Body parameter; see below. |

**Body Attributes**

| Attribute | Required/Optional | Description |
|--------------|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| created | Optional | The time the dashboard was created. This must be in ISO 8601 format. |
| creatorEmail | Optional | The email of the user who created the dashboard. |
| description | Optional | The description of the dashboard. |
| id | Optional | The ID of the dashboard. |
| layout | Optional | Specifies the layout of the dashboard’s row(s). Layout contains a single attribute: contents (optional) Array of JSON objects that correspond to each row on a dashboard. Within each JSON object there are several options: widgets (optional), which contains IDs for the widgets within the row. height (optional), which is the height setting for the row (small, medium, large, xlarge, or custom). customHeight (optional, which corresponds to the custom height setting. This number is the height in pixels (px) for the row. |
| name | Optional | The name of the dashboard. |
| private | Optional | Whether the dashboard is public or private. |
| properties | Optional | The properties for the dashboard. Propertiescontains several options: timeRangeDuration (optional) The timeframe setting. wrap (optional) Whether the dashboard rows wrap. |
| updated | Optional | The time the dashboard was last updated. This must be in ISO 8601 format. |
| userId | Optional | The ID of the user who created the dashboard. |
| widgets | Optional | A list of the widgets that are contained in the dashboard. |

### GET from /dashboards
Returns a list of dashboards associated with a tenant.

### GET from /dashboards/elementtype
Returns a list of element detail dashboards.

### GET from /dashboards/elementtype/{type}
Returns all element detail dashboards for a given type.

### DELETE from /dashboards/{id}
Deletes a given dashboard.

| Parameters | Required/Optional | Description |
|------------|-------------------|--------------------------------------------------|
| id | Required | URL (path) parameter. The ID of the integration. |

### GET from /dashboards/elementtype/{id}
Returns a dashboard for the given ID.

### POST a Copy from /dashboards/{id}/copy
Copies an existing dashboard.

| Parameters | Required/Optional | Description |
|------------|-------------------|--------------------------------------------------|
| id | Required | URL (path) parameter. The ID of the integration. |

**Body Attributes**

| Attribute | Required/Optional | Description |
|-----------|-------------------|----------------------------|
| name | Required | The name of the dashboard. |
