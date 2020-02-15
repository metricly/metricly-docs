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

CloudWisdom's Datasources API can be used to get a list of datasources, create new ones, edit their settings, and remove them from CloudWisdom. You can test these endpoints by visiting our [Swagger page](https://app.metricly.com/swagger-ui.html#/datasources) and by clicking the interactive buttons below.


## GET from /datasources

{{< button href="https://app.metricly.com/swagger-ui.html#!/datasources/listUsingGET_1" theme="info" >}} GET {{< /button >}} Use this endpoint to  get a list of all datasources as well as their properties, elements, and collectors.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| includeElements | query | boolean | Includes or excludes elements in the response body. |


### Request URL

`https://app.metricly.com/datasources?includeElements={boolean}`

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

{{< button href="https://app.metricly.com/swagger-ui.html#!/datasources/createUsingPOST" theme="success" >}} POST {{< /button >}} Use this endpoint to create a new datasource.

{{% expand "View Method Details." %}}

{{% notice tip %}}

This method can be used to create one or many integrations and should only be used by an experienced power user. Properties associated to datasources are mapped as strings and cannot be validated, meaning typos are not caught and returned as errors. Virtana recommends creating your datasources through the UI; updating an existing datasource via PUT is less complex than POSTing a new datasource.

{{% /notice %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| term | path | string | The element field you want to aggregate. |
| elasticsearchQuery | body | JSON | A JSON query. |

### Request URL

`https://app.metricly.com/datasources`


### CURL

In the following CURL example, a new datasource is created with the **name** `CloudWisdom AWS`. Datasource requirements may vary per datasource type. For example, it is recommended you at least include the following properties to set up an AWS datasource:

- awsAuthentication
- awsAccountNumber
- iamRole
- bucketName

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'User-Agent: none' -d '{ \
   "dataSource": { \
     "name": "CloudWisdom AWS", \
     "type": "AWS", \
     "properties": { \
       "awsAuthentication": "role", \
       "awsAccountNumber": "600000000083", \
       "iamRole": "arn:aws:iam::600000000083:role/Netuitive", \
       "ec2Enabled": true, \
       "bucketName": "support-aws-cost" \
     } \
   } \
 }' 'https://app.metricly.com/datasources'

```

## Swagger Sample

```
{
  "dataSource": {
    "name": "CloudWisdom AWS",
    "type": "AWS",
    "properties": {
      "awsAuthentication": "role",
      "awsAccountNumber": "602205202783",
      "iamRole": "arn:aws:iam::602205202783:role/Netuitive",
      "ec2Enabled": true,
      "bucketName": "rcg-netuitive-support-aws-cost"
    }
  }
}
```

### Response Body

The following response body returns a basic AWS datasource with minimal properties. You can add more via the UI or the PUT method.

```
{
  "dataSource": {
    "id": 25796,
    "name": "CloudWisdom AWS",
    "type": "AWS",
    "properties": {
      "awsAuthentication": "role",
      "awsAccountNumber": "600000000083",
      "iamRole": "arn:aws:iam::600000000083:role/Netuitive",
      "ec2Enabled": "true",
      "bucketName": "support-aws-cost",
      "regions": "us-east-1,us-east-2,us-west-1,us-west-2,ca-central-1,ap-south-1,ap-northeast-2,ap-southeast-1,ap-southeast-2,ap-northeast-1,eu-central-1,eu-west-1,eu-west-2,sa-east-1",
      "collectionGranularity": "5",
      "collectionOffset": "5",
      "collectionPeriod": "5",
      "threadPoolSize": "10"
    },
    "enabled": true,
    "deleted": false,
    "apiId": null,
    "collectors": []
  }
}

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

`https://app.metricly.com/datasources/{datasourceId}`


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

{{< button href="https://app.metricly.com/swagger-ui.html#!/datasources/getSingleUsingGET_1" theme="info" >}} GET {{< /button >}} Use this endpoint to get information about one datasource.

{{% expand "View Method Details." %}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|--------------------|----------------|-----------|----------------------------------------------|
| id | path | JSON | Long. |


### Request URL

`https://app.metricly.com/datasources/{dataSourceId}`


### CURL

In the following CURL example, the a datasource with the **id** `12345` is retrieved.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/datasources/12345'

```

### Response Body

The following response body  returns all **properties** and **collectors** associated to the dataSource.

```
{
  "dataSource": {
    "id": 12345,
    "name": "NETUITIVE",
    "type": "AZURE",
    "properties": {
      "asgFilterTagValue": "",
      "mqFilteringEnabled": "false",
      "ebsFilterTagValue": "",
      "sqsFilteringEnabled": "false",
      "sqsEnabled": "true",
      "albFilterTagName": "",
      "efsCollectionFrequency": "5",
      "ebsFilterTagName": "",
      "avmFilterTagType": "include",
      "rdsFilterTagValue": "",
      "ctmEnabled": "false",
      "nlbFilteringEnabled": "false",
      "azureSecretKey": "******",
      "elbCollectionFrequency": "5",
      "ec2FilteringEnabled": "false",
      "lamFilterTagType": "include",
      "albFilterTagValue": "",
      "tagFilterTagName": "",
      "tagCollectionFrequency": "5",
      "elbFilterTagType": "include",
      "dynFilterTagName": "",
      "costExplorerEnabled": "true",
      "knsCollectionFrequency": "5",
      "sqsFilterTagType": "include",
      "avmFilteringEnabled": "false",
      "ctmCollectionFrequency": "5",
      "mqEnabled": "false",
      "azureSubscriptionId": "f9e8197a-1111-9999-3333-f571f5251411",
      "ctmFilterTagName": "",
      "s3FilteringEnabled": "false",
      "agwFilteringEnabled": "false",
      "tagFilterTagType": "include",
      "dynFilterTagType": "include",
      "r53FilterTagValue": "",
      "ec2Enabled": "true"
    },
    "enabled": false,
    "deleted": false,
    "apiId": null,
    "collectors": [
      {
        "id": 4321,
        "name": "Virtual Machine",
        "packageEnabled": false,
        "lastSeen": null,
        "properties": {},
        "datasource": 45243,
        "package": null,
        "elements": []
      },
      {
        "id": 7654,
        "name": "Virtual Machine (Classic)",
        "packageEnabled": false,
        "lastSeen": null,
        "properties": {},
        "datasource": 12345,
        "package": null,
        "elements": []
      }
    ]

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

`https://app.metricly.com/datasources/{id}`


### CURL

In the following CURL example, the datasource with the **id** `12345` is disabled by hanging **enabled** to `false`.

```
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'User-Agent: none' -d '{ \
   "dataSource": { \
     "id": 12345, \
     "name": "ruby", \
     "type": "RUBY", \
     "properties": { \
       "filterTagTypeOld": "include", \
       "awsAuthentication": "role" \
     }, \
     "enabled": false, \
     "deleted": false, \
     "apiId": "cb7515557d71a9b9f9d9ed77b119c84b", \
     "collectors": [ \
     ] \
   } \
 }' 'https://app.metricly.com/datasources/25186'

```

### Swagger Payload

You can use the following template to test this endpoint with Swagger. Select the method icon to open this specific endpoint.

```
{
  "dataSource": {
    "id": 12345,
    "name": "Ruby",
    "type": "RUBY",
    "properties": {
      "filterTagTypeOld": "include",
      "awsAuthentication": "role"
    },
    "enabled": false,
    "deleted": false,
    "apiId": "cb7515557d71a9b9f9d9ed77b119c84b",
    "collectors": [
    ]
  }
}
```

### Response Body

The following response body returns more details about the datasource and allows the user to verity the values have been updated.
```
{
  "dataSource": {
    "id": 12345,
    "name": "Ruby",
    "type": "RUBY",
    "properties": {
      "filterTagTypeOld": "include",
      "awsAuthentication": "role"
    },
    "enabled": false,
    "deleted": false,
    "apiId": "cb7515557d71a9b9f9d9ed77b119c84b",
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
  }
}
```

{{% /expand %}}

---


## How to Update Data Collection for a Datasource

Every datasource has **properties** that can be updated to enable or disable collection for different types of data. In this example we are going to disable collection for a particular AWS region.

{{% expand "View More." %}}

1. Build a CURL query to GET from **/datasources**. This allows us to see a full list of datasources and find the right **id**.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/datasources?includeElements=false'
```

2\. Select a datasource form the response body. Copy its **id** and build another GET query for **/datasources/{id}**

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/datasources/12345'
```

3\. Review the response body. In particular, we are interested in the **properties** options. The properties in this example have been greatly reduced. Find the **regions** key.

```
{
  "dataSource": {
    "id": 12345,
    "name": "AWS1-new",
    "type": "AWS",
    "properties": {
      "bucketName": "rcg-netuitive-support-aws-cost",
      "regions": "us-east-1,us-east-2,us-west-1,us-west-2,ca-central-1,ap-south-1,ap-northeast-2,ap-southeast-1,ap-southeast-2,ap-northeast-1,eu-central-1,eu-west-1,eu-west-2,sa-east-1",
      "lamFilterTagName": "",
      "sqsFilterTagName": "",
      "lamCollectionFrequency": "5",
      "collectionGranularity": "5",
      "efsFilteringEnabled": "false",
      "asgFilterTagType": "include",
      "rdsFilteringEnabled": "false",
      "rdsFilterTagName": "",
      "ec2CollectionFrequency": "5",
      "ebsFilterTagType": "exclude",
      "vmcEnabled": "true",
      "elbFilterTagName": "",
      "vmcFilterTagValue": "",
      "tagEnabled": "false",
      "nlbFilterTagName": "",
      "knsFilterTagValue": "",
      "ebsEnabled": "true",
      "iamRole": "arn:aws:iam::600000000003:role/Netuitive",
      "tagFilterTagValue": "",
      "elbEnabled": "false",
      "mqFilterTagValue": "",
      "echFilterTagValue": "",
      "asgEnabled": "true",
      "awsAuthentication": "role",
      "ec2FilterTagValue": "",
      "redEnabled": "false",
      "agwCollectionFrequency": "5",
      "r53FilterTagType": "include",
      "efsFilterTagType": "include",
      "knsFilterTagType": "exclude",
      "asgCollectionFrequency": "5",
      "redCollectionFrequency": "5",
      "dynFilteringEnabled": "false",
      "ecsFilterTagValue": "",
      "ecsFilterTagName": "",
      "emrCollectionFrequency": "5",
      "emrEnabled": "false",
      "avmFilterTagValue": "",
      "s3FilterTagValue": "",
      "ctmFilteringEnabled": "false",
      "elbFilterTagValue": "",
      "tagFilteringEnabled": "false",
      "avmEnabled": "true",
      "filterTagTypeOld": "exclude",
      "urls": "[{\"type\":\"URL\",\"url\":\"\",\"elementName\":\"\",\"generateElementName\":false,\"enableErrorTracking\":true}]",
      "nlbEnabled": "false",
      "r53FilterTagName": "",
      "avmCollectionFrequency": "5",
      "nlbCollectionFrequency": "5",
      "s3Enabled": "false",
      "collectionPeriod": "5",
      "awsAccountNumber": "600005000003"
    },
    "enabled": false,
    "deleted": false,
    "apiId": null,
    "collectors": [
    ]
  }
}
```

4\. Build a CURL query for the PUT method for the endpoint **/datasources/{id}**. You'll need to use the datasources's **id** as a parameter. Remove the region `us-east-1` from the list.

```
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'User-Agent: none' -d '{ \
   "dataSource": { \
     "name": "AWS1-new", \
     "properties": { \
       "regions": "us-east-2,us-west-1,us-west-2,ca-central-1,ap-south-1,ap-northeast-2,ap-southeast-1,ap-southeast-2,ap-northeast-1,eu-central-1,eu-west-1,eu-west-2,sa-east-1} \
 } \
 }' 'https://app.metricly.com/datasources/12345
```

5\. The response body returns the whole datasource definition. Verify that the **regions** have updated.

{{% /expand %}}
