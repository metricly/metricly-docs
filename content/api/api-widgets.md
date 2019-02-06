---
title: "Widgets API"
draft: false
categories:
tags: ["#api",]
author: Lawrence Lane
alwaysopen: false
pre: ""
---

## Widget Types

### Multi-Metric

```
{
 "widget" : {
     "dashboardId" : "1d11111b-a111-11d1-adda-1aa1111cc1b1",
     "name" : "Total Disk Ops",
     "widgetType" : "multi-metric",
     "properties" : {
       "visualization" : "line",
       "tableColumns" : "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"}]",
       "showElementTotal" : "true",
       "elementScopeTags" : "[]",
       "useAllElementScopeTags" : "true",
       "elementScopeTypes" : "[\"EC2\"]",
       "metricLimit" : "10",
       "useAllMetricScopeTags" : "true",
       "metricAggs" : "[]",
       "elementScopeIds" : "[]",
       "elementScopeAttributes" : "[]",
       "showHighest" : "true",
       "metricScopeTags" : "[]",
       "useAllElementScopeAttributes" : "true",
       "metricAgg" : "avg",
       "metrics" : "[{\"fqn\":\"netuitive.aws.ec2.disktotalops\",\"useRegex\":false,\"aggFns\":[]}]"
     }
   }
}
```

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ \
   "widget" : { \
       "dashboardId" : "bf6e47b9-883e-4634-8bdf-f64c144fd7b2", \
       "name" : "Total Disk Ops", \
       "widgetType" : "multi-metric", \
       "properties" : { \
         "visualization" : "line", \
         "tableColumns" : "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"}]",  \
         "showElementTotal" : "true", \
         "elementScopeTags" : "[]", \
         "useAllElementScopeTags" : "true", \
         "elementScopeTypes" : "[\"EC2\"]", \
         "metricLimit" : "10", \
         "useAllMetricScopeTags" : "true", \
         "metricAggs" : "[]", \
         "elementScopeIds" : "[]", \
         "elementScopeAttributes" : "[]", \
         "showHighest" : "true", \
         "metricScopeTags" : "[]", \
         "useAllElementScopeAttributes" : "true", \
         "metricAgg" : "avg", \
         "metrics" : "[{\"fqn\":\"netuitive.aws.ec2.disktotalops\",\"useRegex\":false,\"aggFns\":[]}]" \
       } \
     } \
 }' 'https://app.metricly.com/widgets'
```

### Multi-Metric Table

```
{
  "widget" : {
        "dashboardId" : "1d11111b-a111-11d1-adda-1aa1111cc1b1",
        "name": "RDS Summary Data",
        "widgetType": "multi-metric-table",
        "properties": {
          "showElementTotal": "true",
          "selectedAttributes": "[{\"name\":\"region\"},{\"name\":\"dbName\"}]",
          "elementScopeTags": "[]",
          "useElementNameContains": "true",
          "elementScopeTypes": "[\"RDS\"]",
          "metricLimit": "10",
          "metricAggs": "[]",
          "elementScopeIds": "[]",
          "elementScopeAttributes": "[]",
          "showHighest": "true",
          "width": "auto",
          "metrics": "[{\"fqn\":\"netuitive.aws.rds.diskspacepercentused\",\"aggFn\":\"avg\",\"displayName\":\"Disk % Used\"},{\"fqn\":\"aws.rds.cpuutilization\",\"aggFn\":\"avg\",\"displayName\":\"CPU %\"},{\"fqn\":\"netuitive.aws.rds.iopsutilization\",\"aggFn\":\"avg\",\"displayName\":\"IOPS %\"},{\"fqn\":\"netuitive.aws.rds.totalthroughput\",\"aggFns\":[],\"aggFn\":\"avg\",\"displayName\":\"Throughput\"}]",
          "selectedTab": "table"
        }
      }
    }
```

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ \
   "widget" : { \
         "dashboardId" : "bf6e47b9-883e-4634-8bdf-f64c144fd7b2", \
         "name": "RDS Summary Data", \
         "widgetType": "multi-metric-table", \
         "properties": { \
           "showElementTotal": "true", \
           "selectedAttributes": "[{\"name\":\"region\"},{\"name\":\"dbName\"}]", \
           "elementScopeTags": "[]", \
           "useElementNameContains": "true", \
           "elementScopeTypes": "[\"RDS\"]", \
           "metricLimit": "10", \
           "metricAggs": "[]", \
           "elementScopeIds": "[]", \
           "elementScopeAttributes": "[]", \
           "showHighest": "true", \
           "width": "auto", \
           "metrics": "[{\"fqn\":\"netuitive.aws.rds.diskspacepercentused\",\"aggFn\":\"avg\",\"displayName\":\"Disk % Used\"},{\"fqn\":\"aws.rds.cpuutilization\",\"aggFn\":\"avg\",\"displayName\":\"CPU %\"},{\"fqn\":\"netuitive.aws.rds.iopsutilization\",\"aggFn\":\"avg\",\"displayName\":\"IOPS %\"},{\"fqn\":\"netuitive.aws.rds.totalthroughput\",\"aggFns\":[],\"aggFn\":\"avg\",\"displayName\":\"Throughput\"}]", \
           "selectedTab": "table" \
```

### Events

```
{
 "widget" : {
   "dashboardId" : "1d11111b-a111-11d1-adda-1aa1111cc1b1",
   "name" : "EC2 Events",
   "widgetType" : "events",
   "properties" : {
     "visualization" : "summary heat map",
     "tableColumns" : "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"}]",
     "showElementTotal" : "true",
     "elementScopeTags" : "[]",
     "useAllElementScopeTags" : "true",
     "elementScopeTypes" : "[\"EC2\"]",
     "metricLimit" : "10",
     "useAllMetricScopeTags" : "true",
     "metricAggs" : "[]",
     "elementScopeIds" : "[]",
     "elementScopeAttributes" : "[]",
     "showHighest" : "true",
     "metricScopeTags" : "[]",
     "useAllElementScopeAttributes" : "true",
     "metricAgg" : "avg"
   }
 }
}
```

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ \
   "widget" : { \
     "dashboardId" : "bf6e47b9-883e-4634-8bdf-f64c144fd7b2", \
     "name" : "EC2 Events", \
     "widgetType" : "events", \
     "properties" : { \
       "visualization" : "summary heat map", \
       "tableColumns" : "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"}]", \
       "showElementTotal" : "true", \
       "elementScopeTags" : "[]", \
       "useAllElementScopeTags" : "true", \
       "elementScopeTypes" : "[\"EC2\"]", \
       "metricLimit" : "10", \
       "useAllMetricScopeTags" : "true", \
       "metricAggs" : "[]", \
       "elementScopeIds" : "[]", \
       "elementScopeAttributes" : "[]", \
       "showHighest" : "true", \
       "metricScopeTags" : "[]", \
       "useAllElementScopeAttributes" : "true", \
       "metricAgg" : "avg" \
     } \
   } \
 }' 'https://app.metricly.com/widgets'
```

### Single-Metric

```
{
  "widget" : {
    "dashboardId" : "1d11111b-a111-11d1-adda-1aa1111cc1b1",
        "name": "My Single Metric",
        "widgetType": "single-metric",
        "properties": {
          "visualization": "time series",
          "showElementTotal": "true",
          "elementScopeTags": "[]",
          "policies": "[]",
          "useAllElementScopeTags": "true",
          "metricLimit": "10",
          "showBands": "true",
          "elementScopeAttributes": "[]",
          "showHighest": "true",
          "metric_fqn": "cpu.percent",
          "categories": "[]",
          "tableColumns": "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"}]",
          "colorByMetric": "false",
          "elementScopeTypes": "[]",
          "grouping": "attribute=SERVICE",
          "useAllMetricScopeTags": "true",
          "element_fqn": "clagettcentos",
          "metricAggs": "[]",
          "elementScopeIds": "[]",
          "metricScopeTags": "[]",
          "groupByPolicy": "false",
          "useAllElementScopeAttributes": "true",
          "metricAgg": "avg",
          "metrics": "[]",
          "topNLimit": "5",
          "elementScopeExcludedTags": "[]"
    }
  }
}
```

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ \
   "widget" : { \
     "dashboardId" : "bf6e47b9-883e-4634-8bdf-f64c144fd7b2", \
         "name": "My Single Metric", \
         "widgetType": "single-metric", \
         "properties": { \
           "visualization": "time series", \
           "showElementTotal": "true", \
           "elementScopeTags": "[]", \
           "policies": "[]", \
           "useAllElementScopeTags": "true", \
           "metricLimit": "10", \
           "showBands": "true", \
           "elementScopeAttributes": "[]", \
           "showHighest": "true", \
           "metric_fqn": "cpu.percent", \
           "categories": "[]", \
           "tableColumns": "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"}]", \
           "colorByMetric": "false", \
           "elementScopeTypes": "[]", \
           "grouping": "attribute=SERVICE", \
           "useAllMetricScopeTags": "true", \
           "element_fqn": "clagettcentos", \
           "metricAggs": "[]", \
           "elementScopeIds": "[]", \
           "metricScopeTags": "[]", \
           "groupByPolicy": "false", \
           "useAllElementScopeAttributes": "true", \
           "metricAgg": "avg", \
           "metrics": "[]", \
           "topNLimit": "5", \
           "elementScopeExcludedTags": "[]" \
     } \
   } \
 }' 'https://app.metricly.com/widgets'
```

### Metricly Alerts

```
{
 "widget" : {
   "dashboardId" : "1d11111b-a111-11d1-adda-1aa1111cc1b1",
       "name": "My Alert Map",
       "widgetType": "metricly-alerts",
       "properties": {
         "visualization": "map",
         "showElementTotal": "true",
         "elementScopeTags": "[]",
         "policies": "[]",
         "useAllElementScopeTags": "true",
         "metricLimit": "10",
         "showBands": "true",
         "elementScopeAttributes": "[]",
         "showHighest": "true",
         "categories": "[]",
         "tableColumns": "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"}]",
         "colorByMetric": "false",
         "elementScopeTypes": "[]",
         "grouping": "attribute=SERVICE",
         "useAllMetricScopeTags": "true",
         "metricAggs": "[]",
         "elementScopeIds": "[]",
         "metricScopeTags": "[]",
         "groupByPolicy": "false",
         "useAllElementScopeAttributes": "true",
         "metricAgg": "avg",
         "metrics": "[]",
         "topNLimit": "5",
         "elementScopeExcludedTags": "[]"
   }
 }
}
```

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d ' { \
   "widget" : { \
     "dashboardId" : "bf6e47b9-883e-4634-8bdf-f64c144fd7b2", \
         "name": "My Alert Map", \
         "widgetType": "metricly-alerts", \
         "properties": { \
           "visualization": "map", \
           "showElementTotal": "true", \
           "elementScopeTags": "[]", \
           "policies": "[]", \
           "useAllElementScopeTags": "true", \
           "metricLimit": "10", \
           "showBands": "true", \
           "elementScopeAttributes": "[]", \
           "showHighest": "true", \
           "categories": "[]", \
           "tableColumns": "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"}]", \
           "colorByMetric": "false", \
           "elementScopeTypes": "[]", \
           "grouping": "attribute=SERVICE", \
           "useAllMetricScopeTags": "true", \
           "metricAggs": "[]", \
           "elementScopeIds": "[]", \
           "metricScopeTags": "[]", \
           "groupByPolicy": "false", \
           "useAllElementScopeAttributes": "true", \
           "metricAgg": "avg", \
           "metrics": "[]", \
           "topNLimit": "5", \
           "elementScopeExcludedTags": "[]" \
     } \
   } \
 }' 'https://app.metricly.com/widgets'
```

### Metric-Range

```
{
    "widget" : {
      "dashboardId" : "1d11111b-a111-11d1-adda-1aa1111cc1b1",
      "name" : "Highest CPU Utilization",
      "widgetType" : "metric-range",
      "properties" : {
        "visualization" : "bar",
        "tableColumns" : "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"}]",
        "showElementTotal" : "true",
        "elementScopeTags" : "[]",
        "useAllElementScopeTags" : "true",
        "elementScopeTypes" : "[\"EC2\"]",
        "metricLimit" : "5",
        "useAllMetricScopeTags" : "true",
        "metricAggs" : "[]",
        "elementScopeIds" : "[]",
        "elementScopeAttributes" : "[]",
        "showHighest" : "true",
        "metric_fqn" : "aws.ec2.cpuutilization",
        "metricScopeTags" : "[]",
        "useAllElementScopeAttributes" : "true",
        "metricAgg" : "avg",
        "metrics" : "[]"
    }
  }
}
```

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ \
     "widget" : { \
       "dashboardId" : "bf6e47b9-883e-4634-8bdf-f64c144fd7b2", \
       "name" : "Highest CPU Utilization", \
       "widgetType" : "metric-range", \
       "properties" : { \
         "visualization" : "bar", \
         "tableColumns" : "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"}]", \
         "showElementTotal" : "true", \
         "elementScopeTags" : "[]", \
         "useAllElementScopeTags" : "true", \
         "elementScopeTypes" : "[\"EC2\"]", \
         "metricLimit" : "5", \
         "useAllMetricScopeTags" : "true", \
         "metricAggs" : "[]", \
         "elementScopeIds" : "[]", \
         "elementScopeAttributes" : "[]", \
         "showHighest" : "true", \
         "metric_fqn" : "aws.ec2.cpuutilization", \
         "metricScopeTags" : "[]", \
         "useAllElementScopeAttributes" : "true", \
         "metricAgg" : "avg", \
         "metrics" : "[]" \
     } \
   } \
 }' 'https://app.metricly.com/widgets'
```
---

**Request Headers**

| Header Name | Header Value |
|----------------------|---------------------------------------|
| Content-Type | application/json |
| Authorization: Basic | (Base64 encoded authentication value) |

## GET

### GET list from /widgets
Returns a list of widgets associated with a dashboard.

**Parameters**

| Parameters | Required/Optional | Description |
|-------------|-------------------|--------------------------------------------------------------------------------|
| dashboardId | Required | Query parameter. The ID of the dashboard you’re trying to get the widgets for. |

### GET from /widgets/{id}
Returns a widget for the given ID.

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|----------------------------------------------------------------------------------|
| id | Required | URL (path) parameter. The ID for the widget.Input JSON Format for Request Header |

## DELETE

### DELETE from /widgets/{id}
This method deletes a given widget.
Replace {id} in the above URL with the ID from any of your integrations.

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|---------------------------------------------|
| id | Required | URL (path) parameter. The ID of the widget. |

## POST

### POST to /widgets
This method creates a widget. A **dashboardId** is required to create a widget. Obtain an Id from an existing dashboard or create a new dashboard for your widget.

**Parameters**

Parameters	Required/Optional	Description
widget	Required	Body parameter; see below.

**Body Attributes**

| Attribute | Required/Optional | Description |
|-------------|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| created | Optional | The time the widget was created. This must be in ISO 8601 format. |
| dashboardId | Optional | The ID of the dashboard you’re trying to put the widget in. |
| id | Optional | The ID for the widget. If you leave this field blank, Metricly will create an ID for you. |
| name | Optional | The name of the widget. |
| properties | Optional | The properties for the widget; this object will vary depending on the type of widget. You can read more about the widget types and their properties here. |
| updated | Optional | The time the widget was last updated. This must be in ISO 8601 format. |
| userId | Optional | The ID of the user who created the widget. If you leave this field blank, Metricly will use your user ID. |
| widgetType | Optional | See the Widget Types section for a full list. |

## PUT

### PUT to /widgets/{id}
This method will update a given widget.

**Parameters**

| Parameters | Required/Optional | Description |
|------------|-------------------|----------------------------------------------|
| id | Required | URL (path) parameter. The ID for the widget. |
| widget | Required | Body parameter; see below. |


**Body Attributes**

| Attribute | Required/Optional | Description |
|-------------|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| created | Optional | The time the widget was created. This must be in ISO 8601 format. |
| dashboardId | Optional | The ID of the dashboard you’re trying to put the widget in. |
| id | Optional | The ID for the widget. If you leave this field blank, Metricly will create an ID for you. |
| name | Optional | The name of the widget. |
| properties | Optional | The properties for the widget; this object will vary depending on the type of widget. You can read more about the widget types and their properties here. |
| updated | Optional | The time the widget was last updated. This must be in ISO 8601 format. |
| userId | Optional | The ID of the user who created the widget. If you leave this field blank, Metricly will use your user ID. |
| widgetType | Optional | See the Widget Types section for a full list. |
