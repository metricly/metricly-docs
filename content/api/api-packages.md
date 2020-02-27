---
title: "Packages API"
draft: false
categories:
tags: ["#api", "#packages"]
author: Lawrence Lane
alwaysopen: false
pre: ""
---




## About the Packages API

CloudWisdom's Packages API can be used to  -- . You can test these endpoints by visiting our [Swagger page](https://app.metricly.com/swagger-ui.html#/packages) and by clicking the interactive buttons below.

## GET from /packages
{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/packages/listUsingGET_3" >}} GET {{< /button >}} Use this endpoint to list installed packages.

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| dashboardId | query | string | Unique ID of the dashboard this widget is associated to. |

### Request URL

 ` `

### CURL

The following example

```

```

### Response Body

The following response body

```
```
{{% /expand %}}

---

## POST to /packages
{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/packages/provisionUsingPOST" >}} POST {{< /button >}} Use this endpoint to install packages via download URLs.

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| dashboardId | query | string | Unique ID of the dashboard this widget is associated to. |

### Request URL

 ` `

### CURL

The following example

```

```

### Response Body

The following response body

```
```
{{% /expand %}}

---

## POST to /packages/install
{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/packages/installUsingPOST" >}} POST {{< /button >}} Use this endpoint to install packages as a multipart/form data zip file. 

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| dashboardId | query | string | Unique ID of the dashboard this widget is associated to. |

### Request URL

 ` `

### CURL

The following example

```

```

### Response Body

The following response body

```
```
{{% /expand %}}

---

## GET from /widgets
{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/widgets/listWidgetsUsingGET" >}} GET {{< /button >}} Use this endpoint to  

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| dashboardId | query | string | Unique ID of the dashboard this widget is associated to. |

### Request URL

 ` `

### CURL

The following example

```

```

### Response Body

The following response body

```
```
{{% /expand %}}

---

## GET from /widgets
{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/widgets/listWidgetsUsingGET" >}} GET {{< /button >}} Use this endpoint to  

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| dashboardId | query | string | Unique ID of the dashboard this widget is associated to. |

### Request URL

 ` `

### CURL

The following example

```

```

### Response Body

The following response body

```
```
{{% /expand %}}

---
