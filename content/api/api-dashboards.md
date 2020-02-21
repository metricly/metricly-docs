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
| User-Agent | header | string | User-Agent |
| dashboard | body | JSON | JSON payload that contains all dashboard instructions. |


### Request URL

`https://app.metricly.com/dashboards`

### CURL

In the following CURL example, a dashboard with the **name** `API created dashboard` is created from scratch. It includes two CPU widgets and a defined **gridstackContents** layout, with placeholder values (1,2) standing in for widget IDs. Using these placeholders allows the API to link widgets with corresponding layout dimensions defined in the gridstackContents

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'User-Agent: none' -d '{ \
   "dashboard": { \
     "name": "API created dashboard", \
     "description": null, \
     "layout": null, \
     "widgets": [ \
       { \
         "id": "1",\
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
         "id": "2",\
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
       "gridstackContents": "[{\"id\":\"1\",\"x\":0,\"y\":0,\"width\":12,\"height\":9},{\"id\":\"2\",\"x\":0,\"y\":9,\"width\":12,\"height\":10}]", \
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

Use the following payload to test this POST method in Swagger.

```
{
  "dashboard": {
    "name": "API created dashboard",
    "description": null,
    "layout": null,
    "widgets": [
      {
        "id": "1",
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
        "id": "2",
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
      "gridstackContents": "[{\"id\":\"1\",\"x\":0,\"y\":0,\"width\":12,\"height\":9},{\"id\":\"2\",\"x\":0,\"y\":9,\"width\":12,\"height\":10}]",
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

The following response body returns the created dashboard, complete with unique **ids** for the dashboard and its widgets. Notice that the placeholder values (1,2) have been replaced in the gridstackContents with the newly generated widget IDs.

```
{
  "dashboard": {
    "id": "ff6d185e-3f40-4872-a13e-ae0b8bb7e599",
    "userId": 76502,
    "name": "API created dashboard",
    "description": null,
    "layout": null,
    "creatorEmail": "mrlawrencelane+supportaccount@gmail.com",
    "created": "2020-02-21T03:45:51Z",
    "updated": "2020-02-21T03:45:51Z",
    "widgets": [
      {
        "id": "8c7e11c0-b88c-4393-91a6-20ca053935ec",
        "dashboardId": "ff6d185e-3f40-4872-a13e-ae0b8bb7e599",
        "userId": null,
        "name": "Windows EC2 CPU",
        "description": null,
        "widgetType": "multi-metric",
        "created": "2020-02-21T03:45:51Z",
        "updated": "2020-02-21T03:45:51Z",
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
        "id": "eb98c261-a3dd-4961-9628-fccc191fb846",
        "dashboardId": "ff6d185e-3f40-4872-a13e-ae0b8bb7e599",
        "userId": null,
        "name": "Linux EC2 CPU",
        "description": null,
        "widgetType": "multi-metric",
        "created": "2020-02-21T03:45:51Z",
        "updated": "2020-02-21T03:45:51Z",
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
      "gridstackContents": "[ {\n  \"id\" : \"8c7e11c0-b88c-4393-91a6-20ca053935ec\",\n  \"x\" : 0,\n  \"y\" : 0,\n  \"width\" : 12,\n  \"height\" : 9\n}, {\n  \"id\" : \"eb98c261-a3dd-4961-9628-fccc191fb846\",\n  \"x\" : 0,\n  \"y\" : 9,\n  \"width\" : 12,\n  \"height\" : 10\n} ]",
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
## DELETE to /dashboards/{id}

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

In the following CURL example, a dashboard with the **id** `6240d033-c887-4b70-8264-a301d3b33aba` is copied and renamed "Cloned Dashboard."

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

There are two ways you can quickly create a dashboard: clone (POST) and update (PUT), or GET and POST. This example uses the GET and POST endpoints.

{{% expand "View More." %}}

1. Build a CURL query to **GET  /dashboards** for a list of all existing dashboards. Use this list to find an existing dashboard to use as a template and grab its **id**.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/dashboards'
```

2\. Build a CURL query to **GET /dashboards/{id}**, using the chosen **id**.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/dashboards/e7f72f9b-54c3-48e4-89d8-9e247ead3b12'
```

3\. Review the response body and make changes as needed. Note that you do not have to remove or update the IDs, as they will get converted to new unque IDs for both the dashboard and its widgets. You only need to change the dashboard name and widget details such as **widgetType**, **metrics**, etc.

```
{
  "dashboard": {
    "id": "e7f72f9b-54c3-48e4-89d8-9e247ead3b12",
    "userId": 24765,
    "name": "Page Views",
    "description": null,
    "layout": null,
    "creatorEmail": "support-testing@netuitive.com",
    "created": "2017-02-02T04:23:27Z",
    "updated": "2017-05-25T00:46:12Z",
    "widgets": [
      {
        "id": "2c9afda3-3ee8-4dbd-8ffe-a23710a72520",
        "dashboardId": "e7f72f9b-54c3-48e4-89d8-9e247ead3b12",
        "userId": 24765,
        "name": "All Page Views Avg",
        "description": null,
        "widgetType": "multi-metric-time-series",
        "created": "2017-02-02T05:10:18Z",
        "updated": "2017-02-02T05:10:18Z",
        "properties": {
          "showElementTotal": "true",
          "selectedAttributes": "[]",
          "elementScopeTags": "[]",
          "useElementNameContains": "true",
          "useAllElementScopeTags": "true",
          "elementScopeTypes": "[]",
          "metricLimit": "10",
          "useAllMetricScopeTags": "true",
          "showArea": "false",
          "metricAggs": "[]",
          "elementScopeIds": "[]",
          "elementScopeAttributes": "[]",
          "showHighest": "true",
          "metricScopeTags": "[]",
          "width": "auto",
          "metrics": "[{\"fqn\":\"customwinmetrics.pageviews.page1.count\",\"aggFns\":[\"avg\"]},{\"fqn\":\"pageviews.page1.count\",\"aggFns\":[\"avg\"]}]",
          "selectedTab": "table"
        },
        "generated": false
      },
      {
        "id": "08d332f3-a036-4506-8329-1bf8c4b6180e",
        "dashboardId": "e7f72f9b-54c3-48e4-89d8-9e247ead3b12",
        "userId": 24765,
        "name": "Page Views",
        "description": null,
        "widgetType": "metric-time-series",
        "created": "2017-02-02T04:24:22Z",
        "updated": "2017-02-02T05:16:58Z",
        "properties": {
          "showElementTotal": "true",
          "selectedAttributes": "[]",
          "elementScopeTags": "[]",
          "useElementNameContains": "true",
          "useAllElementScopeTags": "true",
          "element_id": "f736c76f-a7ab-3d9c-b88c-55591e1decea",
          "elementScopeTypes": "[]",
          "metricLimit": "10",
          "useAllMetricScopeTags": "true",
          "element_fqn": "customwinmetrics",
          "showArea": "false",
          "metricAggs": "[\"sum\"]",
          "elementScopeIds": "[]",
          "elementScopeAttributes": "[]",
          "showHighest": "true",
          "metric_fqn": "customwinmetrics.pageviews.page1.count",
          "metricScopeTags": "[]",
          "width": "medium",
          "metrics": "[]",
          "selectedTab": "table"
        },
        "generated": false
      },
      {
        "id": "711b47e7-0de7-4e8e-a755-9ff718eab486",
        "dashboardId": "e7f72f9b-54c3-48e4-89d8-9e247ead3b12",
        "userId": 24765,
        "name": "Total Page Views",
        "description": null,
        "widgetType": "metric-agg",
        "created": "2017-02-02T04:25:16Z",
        "updated": "2017-02-02T05:14:20Z",
        "properties": {
          "showElementTotal": "true",
          "selectedAttributes": "[]",
          "elementScopeTags": "[]",
          "useElementNameContains": "true",
          "useAllElementScopeTags": "true",
          "element_id": "f736c76f-a7ab-3d9c-b88c-55591e1decea",
          "elementScopeTypes": "[]",
          "metricLimit": "10",
          "useAllMetricScopeTags": "true",
          "element_fqn": "customwinmetrics",
          "showArea": "false",
          "metricAggs": "[\"sum\"]",
          "elementScopeIds": "[]",
          "elementScopeAttributes": "[]",
          "showHighest": "true",
          "metric_fqn": "customwinmetrics.pageviews.page1.count",
          "metricScopeTags": "[]",
          "width": "medium",
          "metrics": "[]",
          "selectedTab": "table"
        },
        "generated": false
      },
      {
        "id": "78eaeefc-e487-40cd-bc71-9f1eb594beaa",
        "dashboardId": "e7f72f9b-54c3-48e4-89d8-9e247ead3b12",
        "userId": 24765,
        "name": "Avg Page Views",
        "description": null,
        "widgetType": "stacked-area",
        "created": "2017-02-02T05:02:20Z",
        "updated": "2017-02-02T05:12:32Z",
        "properties": {
          "showElementTotal": "true",
          "selectedAttributes": "[]",
          "elementScopeTags": "[]",
          "useElementNameContains": "true",
          "useAllElementScopeTags": "true",
          "elementScopeTypes": "[]",
          "metricLimit": "10",
          "useAllMetricScopeTags": "true",
          "showArea": "false",
          "metricAggs": "[]",
          "elementScopeIds": "[]",
          "elementScopeAttributes": "[]",
          "showHighest": "true",
          "metricScopeTags": "[]",
          "width": "auto",
          "metrics": "[{\"fqn\":\"customwinmetrics.pageviews.page1.count\",\"aggFns\":[]}]",
          "selectedTab": "table"
        },
        "generated": false
      }
    ],
    "properties": {
      "refreshIntervalSeconds": "300",
      "timeRangeDuration": "86400",
      "wrap": "true",
      "gridstackContents": "[{\"id\":\"08d332f3-a036-4506-8329-1bf8c4b6180e\",\"width\":4,\"height\":9,\"x\":0,\"y\":0},{\"id\":\"711b47e7-0de7-4e8e-a755-9ff718eab486\",\"width\":4,\"height\":9,\"x\":4,\"y\":0},{\"id\":\"78eaeefc-e487-40cd-bc71-9f1eb594beaa\",\"width\":4,\"height\":9,\"x\":8,\"y\":0},{\"id\":\"2c9afda3-3ee8-4dbd-8ffe-a23710a72520\",\"width\":12,\"height\":9,\"x\":0,\"y\":9}]"
    },
    "type": "DEFAULT",
    "private": false
  }
}
```

4\. In this example, we're going to rename the dashboard and use only the first two widgets to create a simplified dashboard. Build a CURL query to submit to **POST /dashboards**.

```curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'User-Agent: none' -d '{ \
   "dashboard": { \
     "id": "e7f72f9b-54c3-48e4-89d8-9e247ead3b12", \
     "userId": 24765, \
     "name": "Page Views Simplified", \
     "description": null, \
     "layout": null, \
     "creatorEmail": "support-testing%40netuitive.com", \
     "created": "2017-02-02T04:23:27Z", \
     "updated": "2017-05-25T00:46:12Z", \
     "widgets": [ \
       { \
         "id": "2c9afda3-3ee8-4dbd-8ffe-a23710a72520", \
         "dashboardId": "e7f72f9b-54c3-48e4-89d8-9e247ead3b12", \
         "userId": 24765, \
         "name": "All Page Views Avg", \
         "description": null, \
         "widgetType": "multi-metric-time-series", \
         "created": "2017-02-02T05:10:18Z", \
         "updated": "2017-02-02T05:10:18Z", \
         "properties": { \
           "showElementTotal": "true", \
           "selectedAttributes": "[]", \
           "elementScopeTags": "[]", \
           "useElementNameContains": "true", \
           "useAllElementScopeTags": "true", \
           "elementScopeTypes": "[]", \
           "metricLimit": "10", \
           "useAllMetricScopeTags": "true", \
           "showArea": "false", \
           "metricAggs": "[]", \
           "elementScopeIds": "[]", \
           "elementScopeAttributes": "[]", \
           "showHighest": "true", \
           "metricScopeTags": "[]", \
           "width": "auto", \
           "metrics": "[{\"fqn\":\"customwinmetrics.pageviews.page1.count\",\"aggFns\":[\"avg\"]},{\"fqn\":\"pageviews.page1.count\",\"aggFns\":[\"avg\"]}]", \
           "selectedTab": "table" \
         }, \
         "generated": false \
       }, \
       { \
         "id": "08d332f3-a036-4506-8329-1bf8c4b6180e", \
         "dashboardId": "e7f72f9b-54c3-48e4-89d8-9e247ead3b12", \
         "userId": 24765, \
         "name": "Page Views", \
         "description": null, \
         "widgetType": "metric-time-series", \
         "created": "2017-02-02T04:24:22Z", \
         "updated": "2017-02-02T05:16:58Z", \
         "properties": { \
           "showElementTotal": "true", \
           "selectedAttributes": "[]", \
           "elementScopeTags": "[]", \
           "useElementNameContains": "true", \
           "useAllElementScopeTags": "true", \
           "element_id": "f736c76f-a7ab-3d9c-b88c-55591e1decea", \
           "elementScopeTypes": "[]", \
           "metricLimit": "10", \
           "useAllMetricScopeTags": "true", \
           "element_fqn": "customwinmetrics", \
           "showArea": "false", \
           "metricAggs": "[\"sum\"]", \
           "elementScopeIds": "[]", \
           "elementScopeAttributes": "[]", \
           "showHighest": "true", \
           "metric_fqn": "customwinmetrics.pageviews.page1.count", \
           "metricScopeTags": "[]", \
           "width": "medium", \
           "metrics": "[]", \
           "selectedTab": "table" \
         }, \
         "generated": false \
       } \
     ], \
     "properties": { \
       "refreshIntervalSeconds": "300", \
       "timeRangeDuration": "86400", \
       "wrap": "true", \
       "gridstackContents": "[{\"id\":\"08d332f3-a036-4506-8329-1bf8c4b6180e\",\"width\":4,\"height\":9,\"x\":0,\"y\":0},{\"id\":\"711b47e7-0de7-4e8e-a755-9ff718eab486\",\"width\":4,\"height\":9,\"x\":4,\"y\":0}]" \
     }, \
     "type": "DEFAULT", \
     "private": false \
   } \
 }' 'https://app.metricly.com/dashboards'

```
5\. Review the response body to see that your new dashboard has been created.

```
{
  "dashboard": {
    "id": "5b04470b-bd8f-4235-82da-9926dbf3c50b",
    "userId": 76502,
    "name": "Page Views Simplified",
    "description": null,
    "layout": null,
    "creatorEmail": "mrlawrencelane+supportaccount@gmail.com",
    "created": "2020-02-21T04:01:13Z",
    "updated": "2020-02-21T04:01:13Z",
    "widgets": [
      {
        "id": "5577c252-9bb3-44cb-8e38-6325a115c388",
        "dashboardId": "5b04470b-bd8f-4235-82da-9926dbf3c50b",
        "userId": 24765,
        "name": "All Page Views Avg",
        "description": null,
        "widgetType": "multi-metric-time-series",
        "created": "2020-02-21T04:01:13Z",
        "updated": "2020-02-21T04:01:13Z",
        "properties": {
          "showElementTotal": "true",
          "selectedAttributes": "[]",
          "elementScopeTags": "[]",
          "useElementNameContains": "true",
          "useAllElementScopeTags": "true",
          "elementScopeTypes": "[]",
          "metricLimit": "10",
          "useAllMetricScopeTags": "true",
          "showArea": "false",
          "metricAggs": "[]",
          "elementScopeIds": "[]",
          "elementScopeAttributes": "[]",
          "showHighest": "true",
          "metricScopeTags": "[]",
          "width": "auto",
          "metrics": "[{\"fqn\":\"customwinmetrics.pageviews.page1.count\",\"aggFns\":[\"avg\"]},{\"fqn\":\"pageviews.page1.count\",\"aggFns\":[\"avg\"]}]",
          "selectedTab": "table"
        },
        "generated": false
      },
      {
        "id": "19525b84-8a5f-4c90-9007-457bce6c25d3",
        "dashboardId": "5b04470b-bd8f-4235-82da-9926dbf3c50b",
        "userId": 24765,
        "name": "Page Views",
        "description": null,
        "widgetType": "metric-time-series",
        "created": "2020-02-21T04:01:13Z",
        "updated": "2020-02-21T04:01:13Z",
        "properties": {
          "showElementTotal": "true",
          "selectedAttributes": "[]",
          "elementScopeTags": "[]",
          "useElementNameContains": "true",
          "useAllElementScopeTags": "true",
          "element_id": "f736c76f-a7ab-3d9c-b88c-55591e1decea",
          "elementScopeTypes": "[]",
          "metricLimit": "10",
          "useAllMetricScopeTags": "true",
          "element_fqn": "customwinmetrics",
          "showArea": "false",
          "metricAggs": "[\"sum\"]",
          "elementScopeIds": "[]",
          "elementScopeAttributes": "[]",
          "showHighest": "true",
          "metric_fqn": "customwinmetrics.pageviews.page1.count",
          "metricScopeTags": "[]",
          "width": "medium",
          "metrics": "[]",
          "selectedTab": "table"
        },
        "generated": false
      }
    ],
    "properties": {
      "refreshIntervalSeconds": "300",
      "timeRangeDuration": "86400",
      "wrap": "true",
      "gridstackContents": "[ {\n  \"id\" : \"19525b84-8a5f-4c90-9007-457bce6c25d3\",\n  \"x\" : 0,\n  \"y\" : 0,\n  \"width\" : 4,\n  \"height\" : 9\n}, {\n  \"id\" : null,\n  \"x\" : 4,\n  \"y\" : 0,\n  \"width\" : 4,\n  \"height\" : 9\n} ]"
    },
    "type": "DEFAULT",
    "private": false
  }
}
```

The dashboard and its widgets now populate in the UI.

{{% /expand %}}
