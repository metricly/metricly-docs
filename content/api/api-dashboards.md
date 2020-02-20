---
title: "Dashboard API"
draft: false
categories:
tags: ["#api",]
author: Lawrence Lane
alwaysopen: false
pre: ""
---

## About the Dashboards API

CloudWisdom's Dashboards API can be used to get a list of dashboards, create new ones, edit their settings, and remove them from CloudWisdom. You can test these endpoints by visiting our [Swagger page](https://app.metricly.com/swagger-ui.html#/dashboards) and by clicking the interactive buttons below.


## GET from /dashboards

{{< button href="https://app.metricly.com/swagger-ui.html#!/dashboards/listDashboardsUsingGET" theme="info" >}} GET {{< /button >}} Use this endpoint to get a list of all dashboards. Does not include widgets.

{{% expand "View Method Details." %}}


### Request URL

`https://app.metricly.com/dashboards`

### CURL

In the following CURL example, only sending a request to the endpoint is necessary to obtain a list of dashboards.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/dashboards'
```

### Response Body

The following response body returns all dashboards. This example has been shortened to one dashboard.

```
{
  "dashboards": [
    {
      "id": "df1b9000-1234-4d2a-b0a7-e74e4c5d00c6",
      "userId": 23456,
      "name": "ExampleDashboard",
      "description": null,
      "layout": null,
      "creatorEmail": "support-testing@netuitive.com",
      "created": "2018-05-24T12:59:34Z",
      "updated": "2019-09-19T14:24:49Z",
      "widgets": [],
      "properties": {
        "costOnly": "false",
        "timeRangeDuration": "3600",
        "gridstackContents": "[{\"id\":\"14b640c1-74fb-491a-83a9-e4dbf7cab27c\",\"x\":0,\"y\":0,\"width\":12,\"height\":6}]",
        "refreshIntervalSeconds": "300",
        "globalFilter": "false",
        "wrap": "true"
      },
      "type": "DEFAULT",
      "private": false
    }
  ]
}
```

{{% /expand %}}

---
## POST to /dashboards

{{< button href="https://app.metricly.com/swagger-ui.html#!/dashboards/createDashboardUsingPOST" theme="success" >}} POST {{< /button >}} Use this endpoint to create a dashboard.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| User-Agent | header | string | User agent. |
| dashboard | body | JSON | JSON payload that contains all dashboard instructions. |


### Request URL

`https://app.metricly.com/dashboards`

### CURL

In the following CURL example, a dashboard with the **name** `API created dashboard` is created. It includes two CPU widgets and defined **gridstackContents**.

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'User-Agent: none' -d '{ \
   "dashboard": { \
     "name": "API created dashboard", \
     "description": null, \
     "layout": null, \
     "widgets": [ \
       { \
         "name": "Windows EC2 CPU", \
         "description": null, \
         "widgetType": "multi-metric", \
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
           "metrics": "[{\"fqn\":\"aws.ec2.cpuutilization\",\"useRegex\":false,\"aggFns\":[\"avg\"],\"aggFn\":null,\"groupAggFn\":null,\"aggregationGroups\":[]}]", \
           "topNLimit": "5", \
           "elementScopeExcludedTags": "[]" \
         }, \
         "generated": false \
       }, \
       { \
         "name": "Linux EC2 CPU", \
         "description": null, \
         "widgetType": "multi-metric", \
         "properties": { \
           "visualization": "line", \
           "showElementTotal": "true", \
           "elementScopeTags": "[]", \
           "policies": "[]", \
           "useAllElementScopeTags": "true", \
           "metricLimit": "10", \
           "showBands": "true", \
           "elementScopeAttributes": "[]", \
           "elementScopeExcludedAttributes": "[{\"value\":\"windows\",\"key\":\"platform\"}]", \
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
           "metrics": "[{\"fqn\":\"aws.ec2.cpuutilization\",\"useRegex\":false,\"aggFns\":[\"avg\"],\"aggFn\":null,\"groupAggFn\":null,\"aggregationGroups\":[]}]", \
           "topNLimit": "5", \
           "elementScopeExcludedTags": "[]" \
         }, \
         "generated": false \
       } \
     ], \
     "properties": { \
       "timeRangeDuration": "3600", \
       "costOnly": "false", \
       "gridstackContents": "[{\"id\":\"5f85e632-5d09-4a9b-b9fc-ae4730cff055\",\"x\":0,\"y\":0,\"width\":12,\"height\":9},{\"id\":\"80ff3684-3b7d-4667-b81e-836dcf9ee1e7\",\"x\":0,\"y\":9,\"width\":12,\"height\":10}]", \
       "refreshIntervalSeconds": "300", \
       "globalFilter": "false", \
       "wrap": "true" \
     }, \
     "type": "DEFAULT", \
     "private": true \
   } \
 }' 'https://app.metricly.com/dashboards'
```

### Swagger Payload

Use the following payload to test this POST method on Swagger.

```
{
  "dashboard": {
    "name": "API created dashboard 2",
    "description": null,
    "layout": null,
    "widgets": [
      {
        "name": "Windows EC2 CPU",
        "description": null,
        "widgetType": "multi-metric",
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
          "metrics": "[{\"fqn\":\"aws.ec2.cpuutilization\",\"useRegex\":false,\"aggFns\":[\"avg\"],\"aggFn\":null,\"groupAggFn\":null,\"aggregationGroups\":[]}]",
          "topNLimit": "5",
          "elementScopeExcludedTags": "[]"
        },
        "generated": false
      },
      {
        "name": "Linux EC2 CPU",
        "description": null,
        "widgetType": "multi-metric",
        "properties": {
          "visualization": "line",
          "showElementTotal": "true",
          "elementScopeTags": "[]",
          "policies": "[]",
          "useAllElementScopeTags": "true",
          "metricLimit": "10",
          "showBands": "true",
          "elementScopeAttributes": "[]",
          "elementScopeExcludedAttributes": "[{\"value\":\"windows\",\"key\":\"platform\"}]",
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
          "metrics": "[{\"fqn\":\"aws.ec2.cpuutilization\",\"useRegex\":false,\"aggFns\":[\"avg\"],\"aggFn\":null,\"groupAggFn\":null,\"aggregationGroups\":[]}]",
          "topNLimit": "5",
          "elementScopeExcludedTags": "[]"
        },
        "generated": false
      }
    ],
    "properties": {
      "timeRangeDuration": "3600",
      "costOnly": "false",
      "gridstackContents": "[{\"id\":\"5f85e632-5d09-4a9b-b9fc-ae4730cff055\",\"x\":0,\"y\":0,\"width\":12,\"height\":9},{\"id\":\"80ff3684-3b7d-4667-b81e-836dcf9ee1e7\",\"x\":0,\"y\":9,\"width\":12,\"height\":10}]",
      "refreshIntervalSeconds": "300",
      "globalFilter": "false",
      "wrap": "true"
    },
    "type": "DEFAULT",
    "private": true
  }
}
```

### Response Body

The following response body returns the created dashboard, complete with a unique **ids** for the dashboard and its widgets.

```
{
  "dashboard": {
    "id": "466a6920-9595-48e4-b791-53a20e1f8ceb",
    "userId": 76502,
    "name": "API created dashboard 2",
    "description": null,
    "layout": null,
    "creatorEmail": "mrlawrencelane+supportaccount@gmail.com",
    "created": "2020-02-16T01:54:20Z",
    "updated": "2020-02-16T01:54:20Z",
    "widgets": [
      {
        "id": "9dde7129-0e08-415f-bf5c-d0b67f7e3dd0",
        "dashboardId": "466a6920-9595-48e4-b791-53a20e1f8ceb",
        "userId": null,
        "name": "Windows EC2 CPU",
        "description": null,
        "widgetType": "multi-metric",
        "created": "2020-02-16T01:54:20Z",
        "updated": "2020-02-16T01:54:20Z",
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
          "metrics": "[{\"fqn\":\"aws.ec2.cpuutilization\",\"useRegex\":false,\"aggFns\":[\"avg\"],\"aggFn\":null,\"groupAggFn\":null,\"aggregationGroups\":[]}]",
          "topNLimit": "5",
          "elementScopeExcludedTags": "[]"
        },
        "generated": false
      },
      {
        "id": "844b8bec-80db-4133-83ad-b546cb978285",
        "dashboardId": "466a6920-9595-48e4-b791-53a20e1f8ceb",
        "userId": null,
        "name": "Linux EC2 CPU",
        "description": null,
        "widgetType": "multi-metric",
        "created": "2020-02-16T01:54:20Z",
        "updated": "2020-02-16T01:54:20Z",
        "properties": {
          "visualization": "line",
          "showElementTotal": "true",
          "elementScopeTags": "[]",
          "policies": "[]",
          "useAllElementScopeTags": "true",
          "metricLimit": "10",
          "showBands": "true",
          "elementScopeAttributes": "[]",
          "elementScopeExcludedAttributes": "[{\"value\":\"windows\",\"key\":\"platform\"}]",
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
          "metrics": "[{\"fqn\":\"aws.ec2.cpuutilization\",\"useRegex\":false,\"aggFns\":[\"avg\"],\"aggFn\":null,\"groupAggFn\":null,\"aggregationGroups\":[]}]",
          "topNLimit": "5",
          "elementScopeExcludedTags": "[]"
        },
        "generated": false
      }
    ],
    "properties": {
      "timeRangeDuration": "3600",
      "costOnly": "false",
      "gridstackContents": "[{\"id\":\"5f85e632-5d09-4a9b-b9fc-ae4730cff055\",\"x\":0,\"y\":0,\"width\":12,\"height\":9},{\"id\":\"80ff3684-3b7d-4667-b81e-836dcf9ee1e7\",\"x\":0,\"y\":9,\"width\":12,\"height\":10}]",
      "refreshIntervalSeconds": "300",
      "globalFilter": "false",
      "wrap": "true"
    },
    "type": "DEFAULT",
    "private": true
  }
}
```

{{% /expand %}}

---

## GET from /dashboards/dashboardtype/{type}

{{< button href="https://app.metricly.com/swagger-ui.html#!/dashboards/getByDashboardTypeUsingGET" theme="info" >}} GET {{< /button >}} Use this endpoint to get packaged dashboards specific to certain element types.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| type | path | string | Determines what element type. Can include optional **variant** using an - delimiter. |

{{% notice tip %}}
Variants are typically related to default package dashboards. For example, the SERVER element type has two dashboard variants: FULL and SIMPLE. FULL is provisioned when the default agent collectors are configured. SIMPLE is provisioned when the SimpleCollector is used instead of the default collectors. To see full dashboards, the type would be SERVER-FULL. To see simple, the type would be SERVER-SIMPLE. SERVER will show full only.
{{% /notice %}}


### Request URL

`https://app.metricly.com/dashboards/dashboardtype/{type}`

### CURL

In the following CURL example, all dashboards related to the EBS element type are requested.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/dashboards/dashboardtype/ebs'

```

### Response Body

The following response body returns the template for EBS element types, including all **widgets** and dashboard **properties**. This example has been reduced to two widgets. **gridstackContents** determines the overall layout design (size and placement of widgets).

```

{
  "elementTypeDashboard": {
    "id": "EBS",
    "userId": null,
    "name": "AWS EBS Element Detail",
    "description": null,
    "layout": null,
    "creatorEmail": "test@netuitive.com",
    "created": "2018-09-06T19:30:35Z",
    "updated": "2019-04-10T12:13:12Z",
    "widgets": [
      {
        "id": "5da2babc-4321-56789-1111-1c84e3e5ddac",
        "dashboardId": "a1abee12-1111-2222-3333-78c8b35e3b33",
        "userId": 0,
        "name": "Volume Queue Length",
        "description": null,
        "widgetType": "metric-time-series",
        "created": "2019-04-10T12:13:12Z",
        "updated": "2019-04-10T12:13:12Z",
        "properties": {
          "showHighest": "true",
          "metric_fqn": "aws.ebs.volumequeuelength",
          "showElementTotal": "true",
          "useElementNameContains": "true",
          "width": "medium",
          "metricLimit": "10",
          "selectedTab": "table"
        },
        "generated": false
      },
      {
        "id": "b4d37927-6666-7777-8888-8f7f83564038",
        "dashboardId": a1abee12-1111-2222-3333-78c8b35e3b33",
        "userId": 0,
        "name": "Queue Length Differential",
        "description": null,
        "widgetType": "metric-time-series",
        "created": "2019-04-10T12:13:12Z",
        "updated": "2019-04-10T12:13:12Z",
        "properties": {
          "showHighest": "true",
          "metric_fqn": "netuitive.aws.ebs.queuelengthdifferential",
          "showElementTotal": "true",
          "useElementNameContains": "true",
          "width": "auto",
          "metricLimit": "10",
          "selectedTab": "table"
        },
        "generated": false
      }
    ],
    "properties": {
      "refreshIntervalSeconds": "300",
      "timeRangeDuration": "3600",
      "wrap": "true",
      "gridstackContents": "[ {\n  \"id\" : \"91d41d43-571f-30a4-b511-500425f2cf71\",\n  \"x\" : 0,\n  \"y\" : 27,\n  \"width\" : 6,\n  \"height\" : 9\n}, {\n  \"id\" : \"7649fe4c-4a59-3c65-8576-937cc93171bd\",\n  \"x\" : 4,\n  \"y\" : 0,\n  \"width\" : 4,\n  \"height\" : 9\n}, {\n  \"id\" : \"d83824ba-df3f-3d6a-9f69-bd909f1811ae\",\n  \"x\" : 4,\n  \"y\" : 9,\n  \"width\" : 4,\n  \"height\" : 9\n}, {\n  \"id\" : \"b4d37927-1d2b-33f9-b82d-8f7f83564038\",\n  \"x\" : 8,\n  \"y\" : 9,\n  \"width\" : 4,\n  \"height\" : 9\n}, {\n  \"id\" : \"20be610a-43a7-33fd-9f9c-93a46e181a40\",\n  \"x\" : 0,\n  \"y\" : 36,\n  \"width\" : 12,\n  \"height\" : 9\n}, {\n  \"id\" : \"457dff70-5a97-3de5-aedd-b00a5e981c72\",\n  \"x\" : 8,\n  \"y\" : 0,\n  \"width\" : 4,\n  \"height\" : 9\n}, {\n  \"id\" : \"6e4c2b38-3bfa-3384-bf87-149efc4cefce\",\n  \"x\" : 6,\n  \"y\" : 18,\n  \"width\" : 6,\n  \"height\" : 9\n}, {\n  \"id\" : \"5da2babc-3ae8-38c3-99eb-1c84e3e5ddac\",\n  \"x\" : 0,\n  \"y\" : 18,\n  \"width\" : 6,\n  \"height\" : 9\n}, {\n  \"id\" : \"04a93da1-1038-3e8f-a2fe-59d34fcacd2a\",\n  \"x\" : 0,\n  \"y\" : 9,\n  \"width\" : 4,\n  \"height\" : 9\n}, {\n  \"id\" : \"bb5b336e-099e-356b-a98b-eae446d2cc68\",\n  \"x\" : 6,\n  \"y\" : 27,\n  \"width\" : 6,\n  \"height\" : 9\n}, {\n  \"id\" : \"bfe523cc-ac6a-3f29-868f-95eb2aead11d\",\n  \"x\" : 0,\n  \"y\" : 0,\n  \"width\" : 4,\n  \"height\" : 9\n} ]"
    },
    "type": "EBS",
    "private": false
  }
}

```

{{% /expand %}}

---
## GET from /dashboards/elementtype

{{< button href="https://app.metricly.com/swagger-ui.html#!/dashboards/getAllElementDetailDashboardsUsingGET" theme="info" >}} GET {{< /button >}} Use this endpoint to get a list of all element detail dashboards. Does not include widgets.

{{% expand "View Method Details." %}}


### Request URL

`https://app.metricly.com/dashboards/elementtype`

### CURL

In the following CURL example, only sending a request to the endpoint is necessary to obtain a list of dashboards.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/dashboards/elementtype'
```

### Response Body

The following response body returns the element detail dashboard for each element type. This example has been shortened to just Lambda, EC2, and S3 bucket types.

```
{
  "elementTypeDashboards": [
    {
      "id": "LAMBDA",
      "userId": null,
      "name": "AWS Lambda Element Detail Page",
      "description": null,
      "layout": null,
      "creatorEmail": "research@netuitive.com",
      "created": "2018-09-20T21:49:08Z",
      "updated": "2019-02-20T20:33:56Z",
      "widgets": [],
      "properties": {
        "refreshIntervalSeconds": "300",
        "timeRangeDuration": "3600",
        "wrap": "true",
        "gridstackContents": "[ {\n  \"id\" : \"cdb3775a-7b25-32b2-83d3-84d616138fbe\",\n  \"x\" : 6,\n  \"y\" : 9,\n  \"width\" : 6,\n  \"height\" : 9\n}, {\n  \"id\" : \"47b8e5da-4c3e-3073-8943-4953dd6580f8\",\n  \"x\" : 0,\n  \"y\" : 18,\n  \"width\" : 6,\n  \"height\" : 9\n}, {\n  \"id\" : \"55fb0aef-2514-36fc-a37c-d3417da5a8fb\",\n  \"x\" : 6,\n  \"y\" : 0,\n  \"width\" : 6,\n  \"height\" : 9\n}, {\n  \"id\" : \"14652108-a819-3c67-876b-5f4c378643b1\",\n  \"x\" : 0,\n  \"y\" : 27,\n  \"width\" : 12,\n  \"height\" : 10\n}, {\n  \"id\" : \"3992a890-8493-3279-954a-378598bff128\",\n  \"x\" : 0,\n  \"y\" : 9,\n  \"width\" : 6,\n  \"height\" : 9\n}, {\n  \"id\" : \"1a9e4512-82e6-3383-af5c-93cbe6a5ea84\",\n  \"x\" : 0,\n  \"y\" : 0,\n  \"width\" : 6,\n  \"height\" : 9\n}, {\n  \"id\" : \"5563b4dd-35eb-34e9-a883-8c0ba1bf0275\",\n  \"x\" : 6,\n  \"y\" : 18,\n  \"width\" : 6,\n  \"height\" : 9\n} ]"
      },
      "type": "LAMBDA",
      "private": false
    },
    {
      "id": "EC2",
      "userId": null,
      "name": "AWS EC2 Element Detail",
      "description": null,
      "layout": null,
      "creatorEmail": "research@netuitive.com",
      "created": "2019-04-23T14:18:40Z",
      "updated": "2019-04-23T14:49:00Z",
      "widgets": [],
      "properties": {
        "refreshIntervalSeconds": "300",
        "density": "normal",
        "timeRangeDuration": "3600",
        "wrap": "true",
        "gridstackContents": "[ {\n  \"id\" : \"e00369f3-6e6b-3ffd-8aca-1cafae6c8a57\",\n  \"x\" : 0,\n  \"y\" : 9,\n  \"width\" : 6,\n  \"height\" : 9\n}, {\n  \"id\" : \"f2b3b136-14fe-3cb3-b5d3-a3fd862d0684\",\n  \"x\" : 0,\n  \"y\" : 0,\n  \"width\" : 4,\n  \"height\" : 9\n}, {\n  \"id\" : \"61473c32-5856-31ae-bd72-e4c59d0302f4\",\n  \"x\" : 0,\n  \"y\" : 26,\n  \"width\" : 12,\n  \"height\" : 9\n}, {\n  \"id\" : \"3d9b4836-3dcf-3a6d-9acf-8d0e448e870b\",\n  \"x\" : 6,\n  \"y\" : 9,\n  \"width\" : 6,\n  \"height\" : 9\n}, {\n  \"id\" : \"f868a8fc-1c91-3d74-893f-c1895a301b41\",\n  \"x\" : 4,\n  \"y\" : 0,\n  \"width\" : 4,\n  \"height\" : 9\n}, {\n  \"id\" : \"de2799a1-bf10-3038-8dc3-bc2b40893ef8\",\n  \"x\" : 8,\n  \"y\" : 0,\n  \"width\" : 4,\n  \"height\" : 9\n}, {\n  \"id\" : \"2ca6804d-bb92-3947-8a02-9180f42625ea\",\n  \"x\" : 0,\n  \"y\" : 18,\n  \"width\" : 3,\n  \"height\" : 8\n}, {\n  \"id\" : \"4b302753-83d4-3882-846f-e0e73650e98e\",\n  \"x\" : 3,\n  \"y\" : 18,\n  \"width\" : 3,\n  \"height\" : 8\n}, {\n  \"id\" : \"f975f948-3031-3937-a8bd-ebdda823e621\",\n  \"x\" : 6,\n  \"y\" : 18,\n  \"width\" : 3,\n  \"height\" : 8\n}, {\n  \"id\" : \"3a0ed68d-b1d6-3e9e-922c-0a9f5154d21e\",\n  \"x\" : 9,\n  \"y\" : 18,\n  \"width\" : 3,\n  \"height\" : 8\n} ]"
      },
      "type": "EC2",
      "private": false
    },
    {
      "id": "S3 BUCKET",
      "userId": null,
      "name": "AWS S3 Element Detail Page",
      "description": null,
      "layout": null,
      "creatorEmail": "research@netuitive.com",
      "created": "2018-09-20T21:49:28Z",
      "updated": "2018-09-20T21:49:28Z",
      "widgets": [],
      "properties": {
        "integrationType": null,
        "density": "normal",
        "timeRangeDuration": "3600",
        "gridstackContents": "[ {\n  \"id\" : \"9d1ad310-a2e2-3ddd-819d-4ef9ca1c85f7\",\n  \"x\" : 0,\n  \"y\" : 9,\n  \"width\" : 12,\n  \"height\" : 9\n}, {\n  \"id\" : \"44775f23-5589-3b16-a7c2-ace703563875\",\n  \"x\" : 0,\n  \"y\" : 0,\n  \"width\" : 12,\n  \"height\" : 9\n} ]",
        "refreshIntervalSeconds": "300",
        "wrap": "true"
      },
      "type": "S3 BUCKET",
      "private": false
    }
  ]
}
```

{{% /expand %}}

---
## DELETE from /dashboards/{id}

{{< button href="https://app.metricly.com/swagger-ui.html#!/dashboards/deleteDashboardUsingDELETE" theme="danger" >}} DELETE {{< /button >}} Use this endpoint to delete a dashboard.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| User-Agent  | header  | string  | User agent.   |
| id | path | string | Unique ID for the dashboard. |

### Request URL

`https://app.metricly.com/dashboards/{id}`

### CURL

In the following CURL example, a dashboard with the **id** `f54f391c-0790-4fe4-8b59-40dbe5cdfaf1` is deleted.

```
curl -X DELETE --header 'Accept: */*' --header 'User-Agent: none' 'https://app.metricly.com/dashboards/f54f391c-0790-4fe4-8b59-40dbe5cdfaf1'
```

### Response Body

The following response body returns no content with a 204 success code.

```
no content

```

{{% /expand %}}

---
## GET from /dashboards/{id}

{{< button href="https://app.metricly.com/swagger-ui.html#!/dashboards/getSingleUsingGET" theme="info" >}} GET {{< /button >}} Use this endpoint to get a dashboard.  

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| id | path | string | Unique ID for the dashboard. |


### Request URL

`https://app.metricly.com/dashboards/{id}`

### CURL

In the following CURL example, only the dashboard's **id** is needed.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/dashboards/23d3a5e6-8366-4242-9438-d5abe01ff59c'

```

### Response Body

The following response body returns basic details and properties of the dashboard.

```
{
  "dashboard": {
    "id": "23d3a5e6-0000-1111-9999-d5abe01ff59c",
    "userId": 87654,
    "name": "Example Name",
    "description": null,
    "layout": null,
    "creatorEmail": "support-testing@netuitive.com",
    "created": "2016-06-29T16:18:47Z",
    "updated": "2019-04-08T20:15:43Z",
    "widgets": [],
    "properties": {
      "integrationType": null,
      "timeRangeDuration": "28800",
      "costOnly": "false",
      "gridstackContents": "[]",
      "refreshIntervalSeconds": "300",
      "globalFilter": "false",
      "wrap": "true"
    },
    "type": "DEFAULT",
    "private": false
  }
}

```

{{% /expand %}}

---
## PUT to /dashboards/{id}

{{< button href="https://app.metricly.com/swagger-ui.html#!/dashboards/getSingleUsingGET" theme="warning" >}} PUT {{< /button >}} Use this endpoint to update a dashboard's settings.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| User-Agent  | header  | string  | User agent.  |
| id | path | string | Unique ID for the dashboard. |
|dashboard   | body  | JSON  | JSON template for the dashboard.  |


### Request URL

`https://app.metricly.com/dashboards/{id}`

### CURL

In the following CURL example, the **name** of the dashboard is updated.

{{% notice tip %}}
Use the GET method from /dashboards/{id} to obtain the full dashboard and resubmit an updated version to this endpoint.
{{% /notice %}}

```
{
  "dashboard": {
    "id": "6240d033-1111-2222-4444-a301d3b33aba",
    "userId": 76502,
    "name": "renamed-dashboard",
    "description": null,
    "layout": null,
    "creatorEmail": "supportaccount@gmail.com",
    "created": "2020-02-15T23:01:56Z",
    "updated": "2020-02-15T23:03:42Z",
    "widgets": [
      {
        "id": "c63f2aad-7167-45fd-97cf-149ffe29ba6a",
        "dashboardId": "6240d033-c887-4b70-8264-a301d3b33aba",
        "userId": 76502,
        "name": "satur",
        "description": null,
        "widgetType": "single-metric",
        "created": "2020-02-15T23:02:44Z",
        "updated": "2020-02-15T23:02:44Z",
        "properties": {
          "visualization": "chart",
          "showElementTotal": "true",
          "elementScopeTags": "[]",
          "policies": "[]",
          "useAllElementScopeTags": "true",
          "metricLimit": "10",
          "showBands": "true",
          "elementScopeAttributes": "[]",
          "elementScopeExcludedAttributes": "[]",
          "showHighest": "true",
          "metric_fqn": "netuitive.aws.ebs.iopsutilization",
          "categories": "[]",
          "tableColumns": "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"},{\"columnType\":\"metric\",\"width\":\"10%\",\"metricDisplayName\":null,\"metricFqn\":null,\"metricAggFn\":null,\"metricAgg\":null,\"metricUnit\":null}]",
          "period": "latest1",
          "colorByMetric": "false",
          "elementScopeTypes": "[\"EBS\"]",
          "excludedElementScopeFqns": "[]",
          "grouping": "attribute=SERVICE",
          "useAllMetricScopeTags": "true",
          "element_fqn": "502379301106:EBS:us-east-1:vol-b994f056",
          "metricAggs": "[]",
          "elementScopeIds": "[]",
          "metricScopeTags": "[]",
          "groupByPolicy": "false",
          "useAllElementScopeAttributes": "true",
          "metricAgg": "avg",
          "metrics": "[]",
          "topNLimit": "5",
          "elementScopeExcludedTags": "[]"
        },
        "generated": false
      }
    ],
    "properties": {
      "timeRangeDuration": "3600",
      "costOnly": "false",
      "gridstackContents": "[{\"id\":\"c63f2aad-7167-45fd-97cf-149ffe29ba6a\",\"width\":4,\"height\":7,\"x\":0,\"y\":0}]",
      "refreshIntervalSeconds": "300",
      "globalFilter": "false",
      "wrap": "true"
    },
    "type": "DEFAULT",
    "private": false
  }
}
```

### Response Body

The following response body returns no content and a 204 success code.

```
no content
```

{{% /expand %}}

---

## POST to /dashboards/{id}/copy

{{< button href="https://app.metricly.com/swagger-ui.html#!/dashboards/copyDashboardUsingPOST" theme="success" >}} POST {{< /button >}} Use this endpoint to copy a dashboard.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| User-Agent   | header  | string   | User agent.  |
| id | path | string | Unique ID of the dashboard. |
| request body   | body  | JSON  |  Used to provide a new name for the dashboard. |


### Request URL

`https://app.metricly.com/dashboards/{id}/copy`

### CURL

In the following CURL example, the a dashboard with the **id** `6240d033-c887-4b70-8264-a301d3b33aba` is copied and renamed "Cloned Dashboard."

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'User-Agent: none' -d '{ \
   "name": "Cloned Dashboard" \
 }' 'https://app.metricly.com/dashboards/6240d033-c887-4b70-8264-a301d3b33aba/copy'
```

### Response Body

The following response body returns all details of the copied dashboard.

```
{
  "dashboard": {
    "id": "cff676f5-1111-7777-0000-155698b864ac",
    "userId": 76502,
    "name": "Cloned Dashboard",
    "description": null,
    "layout": null,
    "creatorEmail": "supportaccount@gmail.com",
    "created": "2020-02-16T01:26:12Z",
    "updated": "2020-02-16T01:26:12Z",
    "widgets": [
      {
        "id": "ad3d1448-6666-3333-7777-7ce38cbbd38d",
        "dashboardId": ""cff676f5-1111-7777-0000-155698b864ac",
        "userId": 76502,
        "name": "satur",
        "description": null,
        "widgetType": "single-metric",
        "created": "2020-02-16T01:26:12Z",
        "updated": "2020-02-16T01:26:12Z",
        "properties": {
          "visualization": "chart",
          "showElementTotal": "true",
          "elementScopeTags": "[]",
          "policies": "[]",
          "useAllElementScopeTags": "true",
          "metricLimit": "10",
          "showBands": "true",
          "elementScopeAttributes": "[]",
          "elementScopeExcludedAttributes": "[]",
          "showHighest": "true",
          "metric_fqn": "netuitive.aws.ebs.iopsutilization",
          "categories": "[]",
          "tableColumns": "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"},{\"columnType\":\"metric\",\"width\":\"10%\",\"metricDisplayName\":null,\"metricFqn\":null,\"metricAggFn\":null,\"metricAgg\":null,\"metricUnit\":null}]",
          "period": "latest1",
          "colorByMetric": "false",
          "elementScopeTypes": "[\"EBS\"]",
          "excludedElementScopeFqns": "[]",
          "grouping": "attribute=SERVICE",
          "useAllMetricScopeTags": "true",
          "element_fqn": "502319302200:EBS:us-east-1:vol-b994f056",
          "metricAggs": "[]",
          "elementScopeIds": "[]",
          "metricScopeTags": "[]",
          "groupByPolicy": "false",
          "useAllElementScopeAttributes": "true",
          "metricAgg": "avg",
          "metrics": "[]",
          "topNLimit": "5",
          "elementScopeExcludedTags": "[]"
        },
        "generated": false
      }
    ],
    "properties": {
      "refreshIntervalSeconds": "300",
      "globalFilter": "false",
      "timeRangeDuration": "3600",
      "costOnly": "false",
      "wrap": "true",
      "gridstackContents": "[{\"id\":\"ad3d1448-84e0-45b0-af5f-7ce38cbbd38d\",\"x\":0,\"y\":0,\"width\":4,\"height\":7}]"
    },
    "type": null,
    "private": false
  }
}

```

{{% /expand %}}

---

## Understanding gridstackContents

**gridstackContents** is a dashboard property that defines the layout of its widgets. It requires widget IDs as well as definitions for width and height.

{{% expand "View More." %}}

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

{{% /expand %}}


## Create a New Dashboard Based on an Existing Dashboard

There are two ways you can quickly create a dashboard: clone (POST) and update (PUT), or GET and POST.

{{% expand "View More." %}}

1. Perform a GET query to /dashboards for a list of all existing dashboards. Find an existing dashboard to use as a template and grab its **id**.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/dashboards'
```

2. Build a CURL query to **GET /dashboards/{id}**, using the chosen **id**.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/dashboards/5d8355a2-1111-2222-bc6a-59f7689e0cf6'
```

3. Review the response body and update **name**, layout (**gridstackContents**), **widgets**, **widgetTypes**, and **metric_fqns**.

```
{
  "dashboard": {
    "id": "5d8355a2-1111-2222-bc6a-59f7689e0cf6",
    "userId": null,
    "name": "AWS ASG Summary",
    "description": null,
    "layout": null,
    "creatorEmail": "research@netuitive.com",
    "created": "2018-09-20T21:47:39Z",
    "updated": "2019-03-13T20:15:48Z",
    "widgets": [
      {
        "id": "b485aa21-515a-3522-9193-1e5c7e95f9bd",
        "dashboardId": "5d8355a2-1111-2222-bc6a-59f7689e0cf6",
        "userId": 0,
        "name": "Highest CPU Utilization",
        "description": null,
        "widgetType": "metric-range",
        "created": "2019-03-13T20:15:48Z",
        "updated": "2019-03-13T20:15:48Z",
        "properties": {
          "tableColumns": "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"},{\"columnType\":\"metric\",\"width\":\"10%\",\"metricDisplayName\":null,\"metricFqn\":null,\"metricAggFn\":null,\"metricUnit\":null}]",
          "visualization": "bar",
          "showElementTotal": "true",
          "useAllElementScopeTags": "true",
          "elementScopeTypes": "[\"ASG\"]",
          "metricLimit": "5",
          "useAllMetricScopeTags": "true",
          "metricUnit": "percent",
          "showHighest": "true",
          "metric_fqn": "aws.ec2.cpuutilization",
          "useAllElementScopeAttributes": "true",
          "metricAgg": "avg"
        },
        "generated": false
      },
      {
        "id": "f33caacd-6db5-3378-84c9-cd9f63551237",
        "dashboardId": "5d8355a2-1111-2222-bc6a-59f7689e0cf6",
        "userId": 0,
        "name": "ASG Network In",
        "description": null,
        "widgetType": "high-low-metric",
        "created": "2019-03-13T20:15:48Z",
        "updated": "2019-03-13T20:15:48Z",
        "properties": {
          "showHighest": "true",
          "metric_fqn": "aws.ec2.networkin",
          "showElementTotal": "true",
          "useElementNameContains": "true",
          "width": "auto",
          "elementScopeTypes": "[\"ASG\"]",
          "metricLimit": "5",
          "selectedTab": "graph"
        },
        "generated": false
      },
      {
        "id": "496494d8-acd8-34ce-b6b3-bcf185805969",
        "dashboardId": "5d8355a2-1111-2222-bc6a-59f7689e0cf6",
        "userId": 0,
        "name": "ASG Network Out",
        "description": null,
        "widgetType": "high-low-metric",
        "created": "2019-03-13T20:15:48Z",
        "updated": "2019-03-13T20:15:48Z",
        "properties": {
          "showHighest": "true",
          "metric_fqn": "aws.ec2.networkout",
          "showElementTotal": "true",
          "useElementNameContains": "true",
          "width": "auto",
          "elementScopeTypes": "[\"ASG\"]",
          "metricLimit": "5",
          "selectedTab": "graph"
        },
        "generated": false
      },
      {
        "id": "ea0a21a9-5638-3c36-be5b-f8f23b8c0438",
        "dashboardId": "5d8355a2-1111-2222-bc6a-59f7689e0cf6",
        "userId": 0,
        "name": "ASG Events",
        "description": null,
        "widgetType": "events",
        "created": "2019-03-13T20:15:48Z",
        "updated": "2019-03-13T20:15:48Z",
        "properties": {
          "tableColumns": "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"},{\"columnType\":\"metric\",\"width\":\"10%\",\"metricDisplayName\":null,\"metricFqn\":null,\"metricAggFn\":null,\"metricUnit\":null}]",
          "visualization": "summary heat map",
          "showHighest": "true",
          "showElementTotal": "true",
          "useAllElementScopeAttributes": "true",
          "useAllElementScopeTags": "true",
          "elementScopeTypes": "[\"ASG\"]",
          "metricAgg": "avg",
          "metricLimit": "10",
          "metrics": "[{\"fqn\":null,\"useRegex\":false,\"aggFns\":[]}]",
          "useAllMetricScopeTags": "true"
        },
        "generated": false
      }
    ],
    "properties": {
      "refreshIntervalSeconds": "300",
      "timeRangeDuration": "3600",
      "wrap": "true",
      "gridstackContents": "[ {\n  \"id\" : \"f33caacd-6db5-3378-84c9-cd9f63551237\",\n  \"x\" : 0,\n  \"y\" : 9,\n  \"width\" : 6,\n  \"height\" : 9\n}, {\n  \"id\" : \"b485aa21-515a-3522-9193-1e5c7e95f9bd\",\n  \"x\" : 0,\n  \"y\" : 0,\n  \"width\" : 6,\n  \"height\" : 9\n}, {\n  \"id\" : \"496494d8-acd8-34ce-b6b3-bcf185805969\",\n  \"x\" : 6,\n  \"y\" : 9,\n  \"width\" : 6,\n  \"height\" : 9\n}, {\n  \"id\" : \"ea0a21a9-5638-3c36-be5b-f8f23b8c0438\",\n  \"x\" : 6,\n  \"y\" : 0,\n  \"width\" : 6,\n  \"height\" : 9\n} ]"
    },
    "type": "DEFAULT",
    "private": false
  }
}
```

4. In this example, the dashboard is rebuilt to be a simple AWS EC2 dashboard.

```
{
	"dashboard": {
		"name": "AWS EC2 pretend",
		"description": null,
		"layout": null,
		"widgets": [{
				"name": "Top 10 Lowest CPU Credit Balance",
				"description": null,
				"widgetType": "metric-range",
				"properties": {
					"period": "latest1",
					"tableColumns": "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"},{\"columnType\":\"metric\",\"width\":\"10%\",\"metricDisplayName\":null,\"metricFqn\":null,\"metricAggFn\":null,\"metricAgg\":null,\"metricUnit\":null}]",
					"visualization": "bar",
					"colorByMetric": "false",
					"showElementTotal": "true",
					"useAllElementScopeTags": "true",
					"elementScopeTypes": "[\"EC2\"]",
					"metricLimit": "10",
					"grouping": "attribute=SERVICE",
					"showBands": "true",
					"useAllMetricScopeTags": "true",
					"showHighest": "false",
					"metric_fqn": "aws.ec2.cpucreditbalance",
					"groupByPolicy": "false",
					"notificationPeriod": "off",
					"useAllElementScopeAttributes": "true",
					"metricAgg": "avg",
					"topNLimit": "5"
				},
				"generated": false
			},
			{
				"name": "CPU Utilization",
				"description": null,
				"widgetType": "multi-metric",
				"properties": {
					"period": "latest1",
					"tableColumns": "[{\"columnType\":\"elementType\",\"width\":\"10%\"},{\"columnType\":\"elementName\",\"width\":\"80%\"},{\"columnType\":\"metric\",\"width\":\"10%\",\"metricDisplayName\":null,\"metricFqn\":null,\"metricAggFn\":null,\"metricAgg\":null,\"metricUnit\":null}]",
					"visualization": "line",
					"colorByMetric": "false",
					"showElementTotal": "true",
					"useAllElementScopeTags": "true",
					"elementScopeTypes": "[\"EC2\"]",
					"metricLimit": "10",
					"grouping": "attribute=SERVICE",
					"showBands": "true",
					"useAllMetricScopeTags": "true",
					"showHighest": "true",
					"groupByPolicy": "false",
					"notificationPeriod": "off",
					"useAllElementScopeAttributes": "true",
					"metricAgg": "avg",
					"metrics": "[{\"fqn\":\"aws.ec2.cpuutilization\",\"useRegex\":false,\"aggFns\":[\"avg\"],\"aggFn\":null,\"groupAggFn\":null,\"aggregationGroups\":[]}]",
					"topNLimit": "5"
				},
				"generated": false
			}
		],
		"properties": {
			"refreshIntervalSeconds": "300",
			"timeRangeDuration": "3600",
			"wrap": "true"
		},
		"type": "DEFAULT",
		"private": false
	}
}
```

{{% /expand %}}
