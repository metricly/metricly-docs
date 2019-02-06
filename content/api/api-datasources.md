---
title: "Datasources API"
draft: false
categories:
tags: ["#api",]
author: Lawrence Lane
alwaysopen: false
pre: ""
---

## Request Header

| Header Name | Header Value |
|----------------------|---------------------------------------|
| Content-Type | application/json |
| Authorization: Basic | (Base64 encoded authentication value) |

## POST
### POST to /datasources
Creates a new integration for a tenant account.

This method can be used to create one or many integrations and **should only be used by an experienced power user**. Properties associated to datasources are mapped as strings and cannot be validated, meaning typos are not caught and returned as errors. Metricly recommends creating your datasources through the UI; updating an existing datasource via PUT is less complex than POSTing a new datasource.

**Request Body**

```
{
  "dataSource": {
    "name": "Metricly AWS",
    "type": "AWS",
    "properties": {
      "awsAuthentication": "role",
      "iamRole": "arn:aws:iam::120056789012:role/Metricly-Read-Only-Role-1200567890",
      "ec2Enabled": true
    }
  }
}
```

#### AWS Example

```
curl -X POST -k -H 'Authorization: Basic dGVzdDp0ZXN0' -i 'https://api.app.metricly.com/datasources' --data '[
{
  "dataSource": {
    "name": "Metricly AWS",
    "type": "AWS",
    "properties": {
      "awsAuthentication": "role",
      "iamRole": "arn:aws:iam::120056789012:role/Metricly-Read-Only-Role-1200567890",
      "ec2Enabled": true
    }
  }
}
]'
```

#### AWS Cost Example

```
curl -X POST -k -H 'Authorization: Basic dGVzdDp0ZXN0' -i 'https://api.app.metricly.com/datasources' --data '[
{
  "dataSource": {
    "id": 47470,
    "name": “ExampleName”,
    "type": "AWSCOST",
    "properties": {
      "bucketName": "a-bucket-name",
      "ec2FilterTagType": "include",
      "ec2FilterTagName": "",
      "ec2Enabled": "true",
      "awsAuthentication": "role",
      "iamRole": "arn:aws:iam::120056789012:role/Metricly-Read-Only-Role-1200567890",
      "ec2FilterTagValue": ""
    }
  }
}
]'
```

**Header**

| Header Name | Header Value |
|----------------------|---------------------------------------|
| Content-Type | application/json |
| Authorization: Basic | (Base64 encoded authentication value) |

**Body Attributes**

| Attribute | Required/Optional | Description |
|------------|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| apild | Optional | The API key associated with the integration. |
| collectors | Optional | The collectors associated with a particular integration. Collectors contains several attributes: datasource (optional) The datasource ID for the datasource the collector is associated with. elements (optional) A comma-delimited list of element IDs that are associated with this collector. id (optional) The ID for the collector. lastSeen (optional) When the collector last sent data. name (optional) The name for the collector. package (optional) The name of the package associated with the collector. packageEnabled (optional) Whether the listed package is enabled. properties (optional) The fields available for the collector (unique to each collector). |
| deleted | Optional | Whether the integration is deleted. |
| enabled | Optional | Whether the integration is enabled or not. |
| name | Optional | The name of the integration (displayed in the Inventory Explorer). |
| properties | Optional | The fields available for the integration (unique to each integration type). |
| type | Required | The type of integration. Can be one of the following: AWS, AWS COST, AZURE |

## GET
### GET from /datasources
Returns a list of all datasources associated with a tenant.

This method provides a list that includes datasources created upon account setup by Metricly; these datasources cannot be deleted by the DELETE method.

### GET from /datasources/{id}
Returns an integration for the given ID.
Replace {id} in the above URL with the ID from any of your integrations.

| Parameters | Required/Optional | Description |
|------------|-------------------|--------------------------------------------------|
| id | Required | URL (path) parameter. The ID of the integration. |

## DELETE
### DELETE  from /datasources/{id}
Deletes a given integration.

Replace {id} in the above URL with the ID of the integration you want deleted. Any integration you have created can be deleted. Metricly provisioned datasources cannot be deleted.

| Parameters | Required/Optional | Description |
|------------|-------------------|--------------------------------------------------|
| id | Required | URL (path) parameter. The ID of the integration. |

## PUT
### PUT to /datasources/{id}
Returns an integration for the given ID.
Replace {id} in the above URL with the ID from any of your integrations.

| Parameters | Required/Optional | Description |
|------------|-------------------|--------------------------------------------------|
| id | Required | URL (path) parameter. The ID of the integration. |
| wrapper | Optional | Body parameter; see below. |

**Body Attributes**

| Attribute | Required/Optional | Description |
|------------|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| apild | Optional | The API key associated with the integration. |
| collectors | Optional | The collectors associated with a particular integration. Collectors contains several attributes: datasource (optional) The datasource ID for the datasource the collector is associated with. elements (optional) A comma-delimited list of element IDs that are associated with this collector. id (optional) The ID for the collector. lastSeen (optional) When the collector last sent data. name (optional) The name for the collector. package (optional) The name of the package associated with the collector. packageEnabled (optional) Whether the listed package is enabled. properties (optional) The fields available for the collector (unique to each collector). |
| deleted | Optional | Whether the integration is deleted. |
| enabled | Optional | Whether the integration is enabled or not. |
| name | Optional | The name of the integration (displayed in the Inventory Explorer). |
| properties | Optional | The fields available for the integration (unique to each integration type). |
| type | Required | The type of integration. Can be one of the following: AWS, AWSCOST, AZURE |
|   |   |   |
