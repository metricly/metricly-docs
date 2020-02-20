---
title: "Widgets API"
draft: false
categories:
tags: ["#api",]
author: Lawrence Lane
alwaysopen: false
pre: ""
---


## About the Widgets API

CloudWisdom's Widgets API can be used to list, create, get, delete, and update widgets. You can test these endpoints by visiting our [Swagger page](https://app.metricly.com/swagger-ui.html#/widgets) and by clicking the interactive buttons below.

## GET from /widgets
{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/widgets/listWidgetsUsingGET" >}} GET {{< /button >}} Use this endpoint to view all widgets associated to a given dashboard.

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| dashboardId | query | string | Unique ID of the dashboard this widget is associated to. |

### Request URL

 `https://app.metricly.com/widgets?dashboardId={id}`

### CURL

The following example only requires the dashboard's **id** to return the widgets.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/widgets?dashboardId=7031cb3f-3160-400a-b279-707b28b2c8b7'

```

### Response Body

The following response body returns 4 widgets that belong to the chosen dashboard. This does not include **gridstackContents** found by interacting with the Dashboards API directly.

```
{
  "widgets": [
    {
      "id": "7b4690b2-fdcd-4bea-9741-15b57149667d",
      "dashboardId": "a1175567-f3e6-0000-1111-0b2a8d3aa504",
      "userId": 24765,
      "name": "Cost Period Comparison",
      "description": null,
      "widgetType": "multi-metric",
      "created": "2018-03-08T19:25:20Z",
      "updated": "2018-03-08T19:25:20Z",
      "properties": {
        "visualization": "line",
        "tableColumns": "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"},{\"columnType\":\"metric\",\"width\":\"10%\",\"metricDisplayName\":null,\"metricFqn\":null,\"metricAggFn\":null,\"metricAgg\":null,\"metricUnit\":null}]",
        "colorByMetric": "false",
        "showElementTotal": "true",
        "elementScopeTags": "[]",
        "useAllElementScopeTags": "true",
        "elementScopeTypes": "[]",
        "metricLimit": "10",
        "showBands": "true",
        "useAllMetricScopeTags": "true",
        "metricAggs": "[]",
        "elementScopeIds": "[]",
        "elementScopeAttributes": "[]",
        "showHighest": "true",
        "metricScopeTags": "[]",
        "useAllElementScopeAttributes": "true",
        "metricAgg": "avg",
        "metrics": "[{\"fqn\":null,\"useRegex\":false,\"aggFns\":[],\"metricAgg\":null}]",
        "elementScopeExcludedTags": "[]"
      },
      "generated": false
    },
    {
      "id": "eeb3c322-7b25-4169-b4a9-eaf4ee0319ba",
      "dashboardId": "a1175567-f3e6-0000-1111-0b2a8d3aa504",
      "userId": 24765,
      "name": "Top 5 Cost by Services",
      "description": null,
      "widgetType": "multi-metric",
      "created": "2018-03-08T19:26:37Z",
      "updated": "2018-03-08T19:27:06Z",
      "properties": {
        "visualization": "line",
        "tableColumns": "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"},{\"columnType\":\"metric\",\"width\":\"10%\",\"metricDisplayName\":null,\"metricFqn\":null,\"metricAggFn\":null,\"metricAgg\":null,\"metricUnit\":null}]",
        "colorByMetric": "false",
        "showElementTotal": "true",
        "elementScopeTags": "[]",
        "useAllElementScopeTags": "true",
        "elementScopeTypes": "[]",
        "metricLimit": "10",
        "showBands": "true",
        "useAllMetricScopeTags": "true",
        "metricAggs": "[]",
        "elementScopeIds": "[]",
        "elementScopeAttributes": "[]",
        "showHighest": "true",
        "metricScopeTags": "[]",
        "useAllElementScopeAttributes": "true",
        "metricAgg": "avg",
        "metrics": "[{\"fqn\":null,\"useRegex\":false,\"aggFns\":[],\"metricAgg\":null}]",
        "elementScopeExcludedTags": "[]"
      },
      "generated": false
    },
    {
      "id": "9ab10f03-2010-4f21-96dd-973ed33b5fb0",
      "dashboardId": "a1175567-f3e6-0000-1111-0b2a8d3aa504",
      "userId": 24765,
      "name": "Cost by Availability Zone",
      "description": null,
      "widgetType": "multi-metric",
      "created": "2018-03-09T17:47:02Z",
      "updated": "2018-03-09T17:47:02Z",
      "properties": {
        "visualization": "line",
        "tableColumns": "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"},{\"columnType\":\"metric\",\"width\":\"10%\",\"metricDisplayName\":null,\"metricFqn\":null,\"metricAggFn\":null,\"metricAgg\":null,\"metricUnit\":null}]",
        "colorByMetric": "false",
        "showElementTotal": "true",
        "elementScopeTags": "[]",
        "useAllElementScopeTags": "true",
        "elementScopeTypes": "[]",
        "metricLimit": "10",
        "showBands": "true",
        "useAllMetricScopeTags": "true",
        "metricAggs": "[]",
        "elementScopeIds": "[]",
        "elementScopeAttributes": "[]",
        "showHighest": "true",
        "metricScopeTags": "[]",
        "useAllElementScopeAttributes": "true",
        "metricAgg": "avg",
        "metrics": "[{\"fqn\":null,\"useRegex\":false,\"aggFns\":[],\"metricAgg\":null}]",
        "elementScopeExcludedTags": "[]"
      },
      "generated": false
    },
    {
      "id": "5027eeda-9c80-4c0a-b434-e2e4f27b499f",
      "dashboardId": "a1175567-f3e6-0000-1111-0b2a8d3aa504",
      "userId": 24765,
      "name": "Total Cost by Service",
      "description": null,
      "widgetType": "multi-metric",
      "created": "2018-03-08T19:26:04Z",
      "updated": "2018-03-08T19:26:04Z",
      "properties": {
        "visualization": "line",
        "tableColumns": "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"},{\"columnType\":\"metric\",\"width\":\"10%\",\"metricDisplayName\":null,\"metricFqn\":null,\"metricAggFn\":null,\"metricAgg\":null,\"metricUnit\":null}]",
        "colorByMetric": "false",
        "showElementTotal": "true",
        "elementScopeTags": "[]",
        "useAllElementScopeTags": "true",
        "elementScopeTypes": "[]",
        "metricLimit": "10",
        "showBands": "true",
        "useAllMetricScopeTags": "true",
        "metricAggs": "[]",
        "elementScopeIds": "[]",
        "elementScopeAttributes": "[]",
        "showHighest": "true",
        "metricScopeTags": "[]",
        "useAllElementScopeAttributes": "true",
        "metricAgg": "avg",
        "metrics": "[{\"fqn\":null,\"useRegex\":false,\"aggFns\":[],\"metricAgg\":null}]",
        "elementScopeExcludedTags": "[]"
      },
      "generated": false
    }
  ]
}
```
{{% /expand %}}

---

## POST to /widgets
{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/widgets/createWidgetUsingPOST" >}} POST {{< /button >}} Use this endpoint to create a widget on a dashboard.

{{% expand "View method details."%}}

{{% notice tip %}}
Creating a widget on a dashboard is a multi-step process. This endpoint is the first step. For the widget to _appear_ on the dashboard, it must also be assigned a gridstackContents value from the Dashboards API (PUT method).
{{% /notice %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| User-Agent | Header | String | User agent. |
|  widget | body  | JSON | Create a JSON payload that defines the widget's type, metrics, and other properties. |

### Request URL

`https://app.metricly.com/widgets`

### CURL

The following example creates a widget named "Windows EC2 Network Out" and associates it with the **dashboardId** `7031cb3f-3160-400a-b279-707b28b2c8b7`.

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'User-Agent: none' -d '{ \
   "widget": { \
     "created": "2020-02-11T18:06:49.886Z", \
     "dashboardId": "7031cb3f-3160-400a-b279-707b28b2c8b7", \
     "description": null, \
     "generated": true, \
     "id": null, \
     "name": "Windows EC2 Network Out", \
     "properties": { \
       "visualization": "line", \
       "showElementTotal": "true", \
       "elementScopeTags": "[]", \
       "policies": "[]", \
       "useAllElementScopeTags": "true", \
       "metricLimit": "10", \
       "showBands": "true", \
       "elementScopeAttributes": "[{\"value\":\"windows\",\"key\":\"platform\"}]", \
       "elementScopeExcludedAttributes": "[]", \
       "elementNameContains": "", \
       "showHighest": "true", \
       "categories": "[]", \
       "tableColumns": "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"},{\"columnType\":\"metric\",\"width\":\"10%\",\"metricDisplayName\":null,\"metricFqn\":null,\"metricAggFn\":null,\"metricAgg\":null,\"metricUnit\":null}]", \
       "period": "latest1", \
       "colorByMetric": "false", \
       "elementScopeTypes": "[\"EC2\"]", \
       "excludedElementScopeFqns": "[]", \
       "grouping": "attribute=SERVICE", \
       "useAllMetricScopeTags": "true", \
       "metricAggs": "[]", \
       "elementScopeIds": "[]", \
       "metricScopeTags": "[]", \
       "groupByPolicy": "false", \
       "useAllElementScopeAttributes": "true", \
       "metricAgg": "avg", \
       "metrics": "[{\"fqn\":\"aws.ec2.networkout\",\"useRegex\":false,\"aggFns\":[\"avg\"],\"aggFn\":null,\"groupAggFn\":null,\"aggregationGroups\":[]}]", \
       "topNLimit": "5", \
       "elementScopeExcludedTags": "[]" \
     }, \
     "updated": "2020-02-11T18:06:49.886Z", \
     "userId": null, \
     "widgetType": "multi-metric" \
   } \
 }' 'https://app.metricly.com/widgets'

```

## Swagger payload

Try creating this widget by swapping out the **dashboardId** and submitting it to Swagger.

```
{
  "widget": {
    "created": "2020-02-11T18:06:49.886Z",
    "dashboardId": "7031cb3f-3160-400a-b279-707b28b2c8b7",
    "description": null,
    "generated": true,
    "id": null,
    "name": "Windows EC2 Network Out",
    "properties": {
      "visualization": "line",
      "showElementTotal": "true",
      "elementScopeTags": "[]",
      "policies": "[]",
      "useAllElementScopeTags": "true",
      "metricLimit": "10",
      "showBands": "true",
      "elementScopeAttributes": "[{\"value\":\"windows\",\"key\":\"platform\"}]",
      "elementScopeExcludedAttributes": "[]",
      "elementNameContains": "",
      "showHighest": "true",
      "categories": "[]",
      "tableColumns": "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"},{\"columnType\":\"metric\",\"width\":\"10%\",\"metricDisplayName\":null,\"metricFqn\":null,\"metricAggFn\":null,\"metricAgg\":null,\"metricUnit\":null}]",
      "period": "latest1",
      "colorByMetric": "false",
      "elementScopeTypes": "[\"EC2\"]",
      "excludedElementScopeFqns": "[]",
      "grouping": "attribute=SERVICE",
      "useAllMetricScopeTags": "true",
      "metricAggs": "[]",
      "elementScopeIds": "[]",
      "metricScopeTags": "[]",
      "groupByPolicy": "false",
      "useAllElementScopeAttributes": "true",
      "metricAgg": "avg",
      "metrics": "[{\"fqn\":\"aws.ec2.networkout\",\"useRegex\":false,\"aggFns\":[\"avg\"],\"aggFn\":null,\"groupAggFn\":null,\"aggregationGroups\":[]}]",
      "topNLimit": "5",
      "elementScopeExcludedTags": "[]"
    },
    "updated": "2020-02-11T18:06:49.886Z",
    "userId": null,
    "widgetType": "multi-metric"
  }
}
```

### Response Body

The following response body returns confirmation that the widget has been created with the configuration specified. Notice that the **id** value is no longer null.

```
{
  "widget": {
    "id": "38250616-a1a7-4d2b-ab48-50ac2333ca95",
    "dashboardId": "7031cb3f-3160-400a-b279-707b28b2c8b7",
    "userId": 76502,
    "name": "Windows EC2 Network Out",
    "description": null,
    "widgetType": "multi-metric",
    "created": "2020-02-17T01:36:39Z",
    "updated": "2020-02-17T01:36:39Z",
    "properties": {
      "visualization": "line",
      "showElementTotal": "true",
      "elementScopeTags": "[]",
      "policies": "[]",
      "useAllElementScopeTags": "true",
      "metricLimit": "10",
      "showBands": "true",
      "elementScopeAttributes": "[{\"value\":\"windows\",\"key\":\"platform\"}]",
      "elementScopeExcludedAttributes": "[]",
      "elementNameContains": "",
      "showHighest": "true",
      "categories": "[]",
      "tableColumns": "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"},{\"columnType\":\"metric\",\"width\":\"10%\",\"metricDisplayName\":null,\"metricFqn\":null,\"metricAggFn\":null,\"metricAgg\":null,\"metricUnit\":null}]",
      "period": "latest1",
      "colorByMetric": "false",
      "elementScopeTypes": "[\"EC2\"]",
      "excludedElementScopeFqns": "[]",
      "grouping": "attribute=SERVICE",
      "useAllMetricScopeTags": "true",
      "metricAggs": "[]",
      "elementScopeIds": "[]",
      "metricScopeTags": "[]",
      "groupByPolicy": "false",
      "useAllElementScopeAttributes": "true",
      "metricAgg": "avg",
      "metrics": "[{\"fqn\":\"aws.ec2.networkout\",\"useRegex\":false,\"aggFns\":[\"avg\"],\"aggFn\":null,\"groupAggFn\":null,\"aggregationGroups\":[]}]",
      "topNLimit": "5",
      "elementScopeExcludedTags": "[]"
    },
    "generated": false
  }
}
```
{{% /expand %}}

---

## DELETE from /widgets/{id}
{{< button theme="danger" href="https://app.metricly.com/swagger-ui.html#!/widgets/deleteUsingDELETE_5" >}} DELETE {{< /button >}} Use this endpoint to delete a widget.

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| User-Agent | Header | String | User agent.  |
|  id | path  | string | Unique widget ID. |

### Request URL

 `https://app.metricly.com/widgets/{id}`

### CURL

The following example only requires the widget ID to perform the deletion.

```
curl -X DELETE --header 'Accept: */*' --header 'User-Agent: none' 'https://app.metricly.com/widgets/38250616-a1a7-4d2b-ab48-50ac2333ca95'

```

### Response Body

The following response body has no content and returns a 204 success code.

```
no content
```
{{% /expand %}}

---

## GET from /widgets/{id}
{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/widgets/getSingleUsingGET_4" >}} GET {{< /button >}} Use this endpoint to

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| id | path  | string | Unique widget ID. |

### Request URL

 `https://app.metricly.com/widgets/{id}`

### CURL

The following example only requires the widget ID.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/widgets/eeb3c322-7b25-4169-b4a9-eaf4ee0319ba'
```

### Response Body

The following response body returns details on the widget specified.

```
{
  "widget": {
    "id": "eeb3c322-7b25-4169-b4a9-eaf4ee0319ba",
    "dashboardId": "a1175567-f3e6-4e43-b283-0b2a8d3aa504",
    "userId": 24765,
    "name": "Top 5 Cost by Services",
    "description": null,
    "widgetType": "multi-metric",
    "created": "2018-03-08T19:26:37Z",
    "updated": "2018-03-08T19:27:06Z",
    "properties": {
      "visualization": "line",
      "tableColumns": "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"},{\"columnType\":\"metric\",\"width\":\"10%\",\"metricDisplayName\":null,\"metricFqn\":null,\"metricAggFn\":null,\"metricAgg\":null,\"metricUnit\":null}]",
      "colorByMetric": "false",
      "showElementTotal": "true",
      "elementScopeTags": "[]",
      "useAllElementScopeTags": "true",
      "elementScopeTypes": "[]",
      "metricLimit": "10",
      "showBands": "true",
      "useAllMetricScopeTags": "true",
      "metricAggs": "[]",
      "elementScopeIds": "[]",
      "elementScopeAttributes": "[]",
      "showHighest": "true",
      "metricScopeTags": "[]",
      "useAllElementScopeAttributes": "true",
      "metricAgg": "avg",
      "metrics": "[{\"fqn\":null,\"useRegex\":false,\"aggFns\":[],\"metricAgg\":null}]",
      "elementScopeExcludedTags": "[]"
    },
    "generated": false
  }
}
```
{{% /expand %}}

---

## PUT to /widgets/{id}
{{< button theme="warning" href="https://app.metricly.com/swagger-ui.html#!/widgets/replaceUsingPUT_1" >}} PUT {{< /button >}} Use this endpoint to edit widgets.

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| User-Agent | Header | String | User agent. |
|  widget | body  | JSON | Create a JSON payload that defines the widget's type, metrics, and other properties. |
| id  | path  | string  | Unique widget ID.  |

### Request URL

`https://app.metricly.com/widgets/{id}`

### CURL

The following example

```
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'User-Agent: none' -d '{ \
   "widget": { \
     "id": "e39b2b2a-e737-47ac-b5cf-364e324d077d", \
     "dashboardId": "7031cb3f-3160-400a-b279-707b28b2c8b7", \
     "userId": 24765, \
     "name": "Top 5 Cost by Services", \
     "description": null, \
     "widgetType": "multi-metric", \
     "created": "2018-03-08T19:26:37Z", \
     "updated": "2018-03-08T19:27:06Z", \
     "properties": { \
       "visualization": "line", \
       "tableColumns": "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"},{\"columnType\":\"metric\",\"width\":\"10%\",\"metricDisplayName\":null,\"metricFqn\":null,\"metricAggFn\":null,\"metricAgg\":null,\"metricUnit\":null}]", \
       "colorByMetric": "false", \
       "showElementTotal": "true", \
       "elementScopeTags": "[]", \
       "useAllElementScopeTags": "true", \
       "elementScopeTypes": "[]", \
       "metricLimit": "10", \
       "showBands": "true", \
       "useAllMetricScopeTags": "true", \
       "metricAggs": "[]", \
       "elementScopeIds": "[]", \
       "elementScopeAttributes": "[]", \
       "showHighest": "true", \
       "metricScopeTags": "[]", \
       "useAllElementScopeAttributes": "true", \
       "metricAgg": "avg", \
       "metrics": "[{\"fqn\":null,\"useRegex\":false,\"aggFns\":[],\"metricAgg\":null}]", \
       "elementScopeExcludedTags": "[]" \
     }, \
     "generated": false \
   } \
 }' 'https://app.metricly.com/widgets/e39b2b2a-e737-47ac-b5cf-364e324d077d'
```

### Response Body

```
{
  "widget": {
    "id": "e39b2b2a-e737-47ac-b5cf-364e324d077d",
    "dashboardId": "7031cb3f-3160-400a-b279-707b28b2c8b7",
    "userId": 76502,
    "name": "Top 5 Cost by Services",
    "description": null,
    "widgetType": "multi-metric",
    "created": "2018-03-08T19:26:37Z",
    "updated": "2020-02-17T02:35:24Z",
    "properties": {
      "visualization": "line",
      "tableColumns": "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"},{\"columnType\":\"metric\",\"width\":\"10%\",\"metricDisplayName\":null,\"metricFqn\":null,\"metricAggFn\":null,\"metricAgg\":null,\"metricUnit\":null}]",
      "colorByMetric": "false",
      "showElementTotal": "true",
      "elementScopeTags": "[]",
      "useAllElementScopeTags": "true",
      "elementScopeTypes": "[]",
      "metricLimit": "10",
      "showBands": "true",
      "useAllMetricScopeTags": "true",
      "metricAggs": "[]",
      "elementScopeIds": "[]",
      "elementScopeAttributes": "[]",
      "showHighest": "true",
      "metricScopeTags": "[]",
      "useAllElementScopeAttributes": "true",
      "metricAgg": "avg",
      "metrics": "[{\"fqn\":null,\"useRegex\":false,\"aggFns\":[],\"metricAgg\":null}]",
      "elementScopeExcludedTags": "[]"
    },
    "generated": false
  }
}
```
{{% /expand %}}

---
