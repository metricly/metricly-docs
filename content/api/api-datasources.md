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

This method can be used to create one or many integrations and **should only be used by an experienced power user**. Properties associated to datasources are mapped as strings and cannot be validated, meaning typos are not caught and returned as errors. Virtana recommends creating your datasources through the UI; updating an existing datasource via PUT is less complex than POSTing a new datasource.

**Request Body**

```
{
  "dataSource": {
    "name": "CloudWise AWS",
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
curl -X POST -k -H 'Authorization: Basic dGVzdDp0ZXN0' -i 'https://api.us.cloudwisdom.virtana.com/datasources' --data '[
{
  "dataSource": {
    "name": "CloudWise AWS",
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

## GET
### GET from /datasources
Returns a list of all datasources associated with a tenant.

This method provides a list that includes datasources created upon account setup by CloudWisdom; these datasources cannot be deleted by the DELETE method.

### GET from /datasources/{id}
Returns an integration for the given ID.
Replace {id} in the above URL with the ID from any of your integrations.

| Parameters | Required/Optional | Description |
|------------|-------------------|--------------------------------------------------|
| id | Required | URL (path) parameter. The ID of the integration. |

## DELETE
### DELETE  from /datasources/{id}
Deletes a given integration.

Replace {id} in the above URL with the ID of the integration you want deleted. Any integration you have created can be deleted. CloudWisdom provisioned datasources cannot be deleted.

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

## Datasource Template

Use the following JSON template as a guide when creating datasources through the Datasources API endpoint. Fields not listed here are not supported; they will be accepted by the endpoint, but not used in any way.

```
{
      "name": "DatasourceName",
      "type": "AWS",
      "properties": {
        "awsAuthentication": "ROLE or USER",
        "iamRole": "required if ROLE",
        "accessKey": "required if USER",
        "secretKey": "required if USER",
        "bucketName": "Optional field containing the S3 bucket name where your billing data is stored. required if you wish to use detailed billing reports.",
        "costExplorerEnabled": "Optional field. TRUE or FALSE. must still have cost explorer active in AWS Console.",
        "isGovCloud": "Optional field. TRUE or FALSE; is this datasource GovCloud?",
        "regions": "Optional field. List of regions that are INCLUDED -- by default, this populates after creation with all regions listed",

        "albEnabled": "TRUE or FALSE; turns collection on.",
        "albFilteringEnabled": "TRUE or FALSE; allows filtering.",
        "albFilterTagType": "INCLUDE or EXCLUDE; determines how filter operates.",
        "albFilterTagValue": "ONLY useable WHEN FilteringEnabled is TRUE.",
        "albFilterTagName": "ONLY useable WHEN FilteringENabled is TRUE.",

        "asgEnabled": "true",
        "asgFilteringEnabled": "true",
        "asgFilterTagType": "include",
        "asgFilterTagValue": "",
        "asgFilterTagName": "",

        "ctmEnabled": "true",
        "ctmFilteringEnabled": "false",
        "ctmFilterTagType": "include",
        "ctmFilterTagValue": "",
        "ctmFilterTagName": "not applicable. use FilterTagValue instead.",

        "dynEnabled": "false",
        "dynFilteringEnabled": "false",
        "dynFilterTagType": "include",
        "dynFilterTagValue": "",
        "dynFilterTagName": "not applicable. use FilterTagValue instead.",

        "ebsEnabled": "true",
        "ebsFilteringEnabled": "false",
        "ebsFilterTagType": "include",
        "ebsFilterTagValue": "",
        "ebsFilterTagName": "",

        "echEnabled": "false",
        "echFilteringEnabled": "false",
        "echFilterTagType": "include",
        "echFilterTagValue": "",
        "echFilterTagName": "",

        "ecsEnabled": "false",
        "ecsFilteringEnabled": "false",
        "ecsFilterTagType": "include",
        "ecsFilterTagValue": "",
        "ecsFilterTagName": "not applicable. use FilterTagValue instead.",

        "ec2Enabled": "true",
        "ec2FilteringEnabled": "false",
        "ec2FilterTagType": "include",
        "ec2FilterTagValue": "",
        "ec2FilterTagName": "",

        "elbEnabled": "true",
        "elbFilteringEnabled": "false",
        "elbFilterTagType": "include",
        "elbFilterTagValue": "",
        "elbFilterTagName": "",

        "emrEnabled": "false",
        "emrFilteringEnabled": "false",
        "emrFilterTagType": "include",
        "emrFilterTagValue": "",
        "emrFilterTagName": "",

        "knsEnabled": "false",
        "knsFilteringEnabled": "false",
        "knsFilterTagType": "include",
        "knsFilterTagValue": "",
        "knsFilterTagName": "not applicable. use FilterTagValue instead.",

        "lamEnabled": "false",
        "lamFilteringEnabled": "false",
        "lamFilterTagType": "include",
        "lamFilterTagValue": "",
        "lamFilterTagName": "",

        "mqEnabled": "false",
        "mqFilteringEnabled": "false",
        "mqFilterTagType": "include",
        "mqFilterTagValue": "",
        "mqFilterTagName": "not applicable. use FilterTagValue instead.",

        "rdsEnabled": "true",
        "rdsFilteringEnabled": "false",
        "rdsFilterTagType": "include",
        "rdsFilterTagValue": "",
        "rdsFilterTagName": "",

        "redEnabled": "false",
        "redFilteringEnabled": "false",
        "redFilterTagType": "include",
        "redFilterTagValue": "",
        "redFilterTagName": "",

        "sqsEnabled": "true",
        "sqsFilteringEnabled": "false",
        "sqsFilterTagType": "include",
        "sqsFilterTagValue": "",
        "sqsFilterTagName": "not applicable. use FilterTagValue instead.",

        "s3Enabled": "false",
        "s3FilteringEnabled": "false",
        "s3FilterTagType": "include",
        "s3FilterTagValue": "",
        "s3FilterTagName": "not applicable. use FilterTagValue instead.",

        "tagEnabled": "false; tag here stands for target groups.",
        "tagFilteringEnabled": "false",
        "tagFilterTagType":"include",
        "tagFilterTagValue": "",
        "tagFilterTagName": "not applicable. use FilterTagValue instead.",

      },

    }
```
