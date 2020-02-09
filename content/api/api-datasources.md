---
title: "Datasources API"
draft: false
categories:
tags: ["#api",]
author: Lawrence Lane
alwaysopen: false
pre: ""
---

## About the Datasources API


## GET from /datasources

{{< button href="https://app.metricly.com/swagger-ui.html#!/datasources/listUsingGET_1" theme="info" >}} GET {{< /button >}} Use this endpoint to  get a list of all datasources as well as their properties, elements, and collectors.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| includeElements | query | boolean | Includes or excludes elements in the response body. |


### Request URL

```
https://app.metricly.com/datasources?includeElements={boolean}

```

### CURL

In the following CURL example, datasources are requested without elements (**includeElements**).

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/datasources?includeElements=false'

```

### Response Body

The following response body returns datasources without elements. This example has been shortened. Notice that datasources include **collectors** and list **properties** that define what is and is not ingested into CloudWisdom.
```
{
  "dataSources": [
    {
      "id": 25186,
      "name": "ExampleRuby",
      "type": "RUBY",
      "properties": {
        "filterTagTypeOld": "include",
        "awsAuthentication": "role"
      },
      "enabled": true,
      "deleted": false,
      "apiId": "cb75111111d71a9b9f9d9ed22b119c84b",
      "collectors": [
        {
          "id": 3888,
          "name": "RUBY",
          "packageEnabled": false,
          "lastSeen": null,
          "properties": {},
          "datasource": 25186,
          "package": null,
          "elements": []
        }
      ]
    },
    {
      "id": 33884,
      "name": "EXAMPLEAZURE",
      "type": "AZURE",
      "properties": {
        "asgFilterTagValue": "",
        "ebsFilterTagValue": "",
        "sqsFilteringEnabled": "false",
        "sqsEnabled": "true",
        "albFilterTagName": "",
        "ebsFilterTagName": "",
        "avmFilterTagType": "include",
        "rdsFilterTagValue": "",
        "ctmEnabled": "false",
        "azureSecretKey": "******",
        "ec2FilteringEnabled": "false",
        "lamFilterTagType": "include",
        "albFilterTagValue": "",
        "elbFilterTagType": "include",
        "dynFilterTagName": "",
        "sqsFilterTagType": "include",
        "avmFilteringEnabled": "false",
        "azureSubscriptionId": "cc8cad9f-ce22-1111-be6c-f444c9b2ab77",
        "s3FilterTagType": "include",
        "emrFilteringEnabled": "false",
        "lamFilterTagName": "",
        "sqsFilterTagName": "",
        "collectionGranularity": "5",
        "vmcEnabled": "true",
        "elbFilterTagName": "",
        "vmcFilterTagValue": "",
        "azureDomain": "111a4746-2ac3-0000-a6c8-bc9cdf67f222",
        "emrFilterTagName": "",
        "echFilterTagName": "",
        "knsFilteringEnabled": "false",
        "agwFilterTagName": "",
        "vmcFilteringEnabled": "false",
        "albFilterTagType": "include",
        "ebsEnabled": "true",
        "azureClientId": "0aea2a0c-2807-4077-a4d5-406fb79b3bff",
        "elbEnabled": "true",
        "echFilterTagValue": "",
        "asgEnabled": "true",
        "awsAuthentication": "role",
        "ec2FilterTagValue": "",
        "redEnabled": "false",
        "albEnabled": "false",
        "ecsFilterTagValue": "",
        "ecsFilterTagName": "",
        "emrEnabled": "false",
        "avmFilterTagValue": "",
        "s3FilterTagValue": "",
        "elbFilterTagValue": "",
        "avmEnabled": "true",
        "urls": "[{\"type\":\"URL\",\"url\":\"\",\"elementName\":\"\",\"generateElementName\":false,\"enableErrorTracking\":true}]",
        "s3Enabled": "false",
        "collectionPeriod": "5",
        "dynFilterTagType": "include",
        "ec2Enabled": "true"
      },
      "enabled": false,
      "deleted": false,
      "apiId": null,
      "collectors": [
        {
          "id": 5868,
          "name": "Virtual Machine Example",
          "packageEnabled": false,
          "lastSeen": null,
          "properties": {},
          "datasource": 33884,
          "package": null,
          "elements": []
        },
        {
          "id": 2927,
          "name": "Virtual Machine",
          "packageEnabled": false,
          "lastSeen": null,
          "properties": {},
          "datasource": 33884,
          "package": null,
          "elements": []
        }
      ]
    }
  ]
}

```

{{% /expand %}}

---

## POST from /datasources

{{< button href="https://app.metricly.com/swagger-ui.html#!/datasources/createUsingPOST" theme="success" >}} POST {{< /button >}} Use this endpoint to

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| term | path | string | The element field you want to aggregate. |
| elasticsearchQuery | body | JSON | A JSON query. |

### Request URL

```
```

### CURL

In the following CURL example,

```

```

### Response Body

The following response body  

```


```

{{% /expand %}}

---

## DELETE from /datasources/{Id}

{{< button href="https://app.metricly.com/swagger-ui.html#!/datasources/deleteUsingDELETE_1" theme="danger" >}} DELETE {{< /button >}} Use this endpoint to  delete a datasource.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| User-Agent | header | string |  |
| id | path | JSON | Long. |

### Request URL

```
https://app.metricly.com/datasources/{datasourceId}

```

### CURL

In the following CURL example, a datasource with the **id** `12345` is deleted.

```
curl -X DELETE --header 'Accept: application/json' --header 'User-Agent: none' 'https://app.metricly.com/datasources/12345'

```


### Response Body

The following response body has no content. The success code is 204.  

```
No Content

```

{{% /expand %}}

---

## GET from /datasources/{Id}

{{< button href="https://app.metricly.com/swagger-ui.html#!/datasources/getSingleUsingGET_1" theme="info" >}} GET {{< /button >}} Use this endpoint to  

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| id | path | JSON | Long. |


### Request URL

```

```

### CURL

In the following CURL example

```

```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```

```

### Response Body

The following response body  
```

```

{{% /expand %}}

---

## PUT from /datasources/{Id}

{{< button href="https://app.metricly.com/swagger-ui.html#!/datasources/replaceDataSourceUsingPUT" theme="warning" >}} PUT {{< /button >}} Use this endpoint to  

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| term | path | string | The element field you want to aggregate. |
| elasticsearchQuery | body | JSON | A JSON query. |

### Request URL

```

```

### CURL

In the following CURL example

```

```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```

```

### Response Body

The following response body  
```

```

{{% /expand %}}

---
