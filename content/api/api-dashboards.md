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

{{% notice tip %}}
The variant part is related to the dashboard variant and typically involves default package dashboards. For example, the SERVER element type has two dashboard variants: FULL and SIMPLE. FULL is provisioned when the default agent collectors are configured. SIMPLE is provisioned when the SimpleCollector is used instead of the default collectors. To see full dashboards, the type would be SERVER-FULL. To see simple, the type would be SERVER-SIMPLE. SERVER will show full only.
{{% /notice %}}

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
