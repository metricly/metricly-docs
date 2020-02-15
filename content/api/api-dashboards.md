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
| includeElements | query | boolean | Includes or excludes elements in the response body. |


### Request URL

`https://app.metricly.com/datasources?includeElements={boolean}`

### CURL

In the following CURL example,

```

```

### Response Body

The following response body returns

```

```

{{% /expand %}}

---

## GET from /dashboards/dashboardtype/{type}

{{< button href="https://app.metricly.com/swagger-ui.html#!/dashboards/getByDashboardTypeUsingGET" theme="info" >}} GET {{< /button >}} Use this endpoint to get dashboards specific to certain element types.

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

The following response body returns the template for EBS element types, including all **widgets** and dashboard **properties**. This example has been reduced to two widgets.

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

{{< button href="https://app.metricly.com/swagger-ui.html#!/dashboards/getAllElementDetailDashboardsUsingGET" theme="info" >}} GET {{< /button >}} Use this endpoint to get element detail dashboards. These are default dashboards in CloudWisdom determined by element type and provide a great template for building more complex dashboards.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| includeElements | query | boolean | Includes or excludes elements in the response body. |


### Request URL

`https://app.metricly.com/datasources?includeElements={boolean}`

### CURL

In the following CURL example,

```

```

### Response Body

The following response body returns

```

```

{{% /expand %}}

---
## DELETE from /dashboards/{id}

{{< button href="https://app.metricly.com/swagger-ui.html#!/dashboards/deleteDashboardUsingDELETE" theme="danger" >}} DELETE {{< /button >}} Use this endpoint to delete a dashboard.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| includeElements | query | boolean | Includes or excludes elements in the response body. |


### Request URL

`https://app.metricly.com/datasources?includeElements={boolean}`

### CURL

In the following CURL example,

```

```

### Response Body

The following response body returns

```

```

{{% /expand %}}

---
## GET from /dashboards/{id}

{{< button href="https://app.metricly.com/swagger-ui.html#!/dashboards/getSingleUsingGET" theme="info" >}} GET {{< /button >}} Use this endpoint to get a dashboard.  

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| includeElements | query | boolean | Includes or excludes elements in the response body. |


### Request URL

`https://app.metricly.com/datasources?includeElements={boolean}`

### CURL

In the following CURL example,

```

```

### Response Body

The following response body returns

```

```

{{% /expand %}}

---
## PUT to /dashboards/{id}

{{< button href="https://app.metricly.com/swagger-ui.html#!/dashboards/getSingleUsingGET" theme="warning" >}} PUT {{< /button >}} Use this endpoint to update a dashboard's settings.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| includeElements | query | boolean | Includes or excludes elements in the response body. |


### Request URL

`https://app.metricly.com/datasources?includeElements={boolean}`

### CURL

In the following CURL example,

```

```

### Response Body

The following response body returns

```

```

{{% /expand %}}

---

## POST to /dashboards/{id}/copy

{{< button href="https://app.metricly.com/swagger-ui.html#!/dashboards/copyDashboardUsingPOST" theme="success" >}} POST {{< /button >}} Use this endpoint to copy a dashboard.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| includeElements | query | boolean | Includes or excludes elements in the response body. |


### Request URL

`https://app.metricly.com/datasources?includeElements={boolean}`

### CURL

In the following CURL example,

```

```

### Response Body

The following response body returns

```

```

{{% /expand %}}

---

## Understanding gridstackContents
