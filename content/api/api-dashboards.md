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
