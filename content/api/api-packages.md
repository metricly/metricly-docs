---
title: "Packages API"
draft: false
categories:
tags: ["#api", "#packages"]
author: Lawrence Lane
alwaysopen: false
pre: ""
---

A package is an archive of assets compatible with CloudWisdom, which automatically provision to your account when you install a compatible integration to get ideal configurations for your environment. Packages typically include dashboards, default policies, and analytics configurations.

Packages are composed of at least three files: a package.json file, README.md, and at least one policy, analytics configuration, or dashboard. All available packages are available on our [community Github](https://github.com/netuitive-community-packages).

## GET

### GET from /packages
Get a list of installed packages

```
curl -X GET --header 'Accept: application/json' 'https://us.cloudwisdom.virtana.com/packages?packageId=netuitive.packages.kafka'
```

**Response**

This is just an example of the JSON format. When you make the call, you will see a list of all packages installed (custom and default). **Packages are automatically provisioned to your account when a datasource is turned on.** This means that if you connect an Elasticsearch datasource to CloudWisdom, the app automatically installs our Elasticsearch package.

```
{
  "packages": [
    {
      "analyticConfigurations": [
        {
          "id": "string",
          "metrics": [
            {
              "configurations": [
                {}
              ],
              "match": "string",
              "parentId": "string",
              "properties": {}
            }
          ],
          "name": "string",
          "packageId": "string",
          "scope": {
            "elementName": "string",
            "elementTags": [
              {
                "dataSourceId": 0,
                "id": "string",
                "name": "string",
                "value": "string"
              }
            ],
            "elementTagsAll": true,
            "elementType": "string",
            "metricMatches": "string"
          },
          "tenantId": "string",
          "type": "string"
        }
      ],
      "authorEmail": "string",
      "authorName": "string",
      "created": "2018-06-26T19:39:40.742Z",
      "dashboards": [
        {
          "created": "2018-06-26T19:39:40.742Z",
          "creatorEmail": "string",
          "description": "string",
          "id": "string",
          "layout": "string",
          "name": "string",
          "private": true,
          "properties": {},
          "tenantId": "string",
          "type": "string",
          "updated": "2018-06-26T19:39:40.742Z",
          "userId": 0,
          "widgets": [
            {
              "created": "2018-06-26T19:39:40.742Z",
              "dashboardId": "string",
              "description": "string",
              "id": "string",
              "name": "string",
              "properties": {},
              "updated": "2018-06-26T19:39:40.742Z",
              "userId": 0,
              "widgetType": "string"
            }
          ]
        }
      ],
      "description": "string",
      "downloadUrl": "string",
      "id": "string",
      "logo": "string",
      "name": "string",
      "packageId": "string",
      "policies": [
        {
          "actions": {},
          "checkCondition": {
            "checkName": "string"
          },
          "conditions": {},
          "creatorEmail": "string",
          "deleted": true,
          "description": "string",
          "duration": 0,
          "enabled": true,
          "eventConditions": {},
          "id": "string",
          "lastUpdated": "2018-06-26T19:39:40.742Z",
          "name": "string",
          "originPolicyId": "string",
          "originTenantId": "string",
          "scope": {
            "elementAttributes": [
              {
                "attributeType": "TEXT",
                "dataSourceId": 0,
                "id": "string",
                "name": "string",
                "value": "string"
              }
            ],
            "elementAttributesAll": true,
            "elementName": "string",
            "elementNameExclude": "string",
            "elementTags": [
              {
                "dataSourceId": 0,
                "id": "string",
                "name": "string",
                "value": "string"
              }
            ],
            "elementTagsAll": true,
            "elementType": "string",
            "elementTypes": [
              "string"
            ],
            "excludedElementAttributes": [
              {
                "attributeType": "TEXT",
                "dataSourceId": 0,
                "id": "string",
                "name": "string",
                "value": "string"
              }
            ],
            "excludedElementTags": [
              {
                "dataSourceId": 0,
                "id": "string",
                "name": "string",
                "value": "string"
              }
            ],
            "fqnExcludes": [
              "string"
            ],
            "fqnIncludes": [
              "string"
            ]
          }
        }
      ],
      "tags": [
        {
          "dataSourceId": 0,
          "id": "string",
          "name": "string",
          "value": "string"
        }
      ],
      "tenantId": "string",
      "updated": "2018-06-26T19:39:40.742Z",
      "userEmail": "string",
      "version": "string"
    }
  ]
}
```

## POST

### POST to /packages/install
Install packages via zip file (Content-Type: multipart/form-data).

```
curl -X POST -u username:password https://api.us.cloudwisdom.virtana.com/packages/install -H 'content-type: multipart/form-data' -F file=@package.zip
```

## DELETE

### DELETE from /packages/{id}
Deletes specified package.

```
curl -X DELETE --header 'Accept: */*' 'https://us.cloudwisdom.virtana.com/packages/123packageid123'
```
