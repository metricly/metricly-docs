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

CloudWisdom's Packages API can be used to list, install, delete, and inspect packages in CloudWisdom. You can test these endpoints by visiting our [Swagger page](https://app.metricly.com/swagger-ui.html#/packages) and by clicking the interactive buttons below.

View the [official GitHub](https://github.com/netuitive-community-packages) for all Virtana (formerly Netuitive) packages.

## GET from /packages
{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/packages/listUsingGET_3" >}} GET {{< /button >}} Use this endpoint to list installed packages.

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| packageId | query | string | ID of the package e.g. netuitive.packages.linux. |
| version  | query  |  string | Semantic version of the package.  |

### Request URL

 `https://app.metricly.com/packages`

### CURL

The following example does not include the optional **packageId** or version. This enables you to list all packages.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/packages'
```

### Response Body

The following response body includes a shortened example of only one package. Typical responses include all packages installed. Notice package templates include default policy templates and default dashboards. The response body will not return widget details.

```
{
	"packages": [{
		"id": "d4c1a0d1-865d-38a3-8c0e-e8248e4ab0c5",
		"tenantId": "0fa5384a-3b36-4766-ad68-43e7c6af54f6",
		"packageId": "netuitive.packages.linux.nginx",
		"version": "1.1.1",
		"name": "Netuitive Packages Linux NGINX",
		"description": "A set of Netuitive analytics configurations, polices, dashboards, and reports that are used to monitor performance of the elements collected from the NGINX collector in the Netuitive Agent.",
		"authorName": "Netuitive Research",
		"authorEmail": "research@netuitive.com",
		"logo": "http://assets.app.netuitive.com/pkg/logo/netuitive/banner_logo.png",
		"downloadUrl": "https://github.com/netuitive-community-packages/netuitive-packages-linux-nginx/archive/master.zip",
		"userEmail": "null",
		"created": "2019-04-09T21:44:27Z",
		"updated": "2019-04-09T21:44:27Z",
		"tags": [],
		"policies": [],
		"analyticConfigurations": [{
				"type": null,
				"id": "7b349868-2c70-38ca-a0e7-7e5f17d81b5b",
				"name": null,
				"scope": null,
				"metrics": []
			},
			{
				"type": null,
				"id": "9e7814f8-bd3e-3f7a-ad92-17e3779b612e",
				"name": null,
				"scope": null,
				"metrics": []
			},
			{
				"type": null,
				"id": "c63afc28-2538-32a7-8ee1-b407128416f9",
				"name": null,
				"scope": null,
				"metrics": []
			}
		],
		"dashboards": [{
			"id": "2a0a9c59-a407-3f49-891e-bc791903b1a2",
			"name": null,
			"description": null,
			"layout": null,
			"properties": null,
			"widgets": null,
			"type": null,
			"private": true
		}]
	}]
}
```
{{% /expand %}}

---

## POST to /packages
{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/packages/provisionUsingPOST" >}} POST {{< /button >}} Use this endpoint to install packages via download URLs.

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| User-Agent | header | string | User-Agent |
| userEmail  | query  | string  |  User Email |
| request  | body  | JSON  | JSON with direct download URL of the package.  |

### Request URL

 `https://app.metricly.com/packages`

### CURL

The following example installs a package from the URL `https://github.com/netuitive-community-packages/netuitive-packages-linux/archive/master.zip`.

```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'User-Agent: none' -d '{ \
   "archives": [ \
     "https://github.com/netuitive-community-packages/netuitive-packages-linux/archive/master.zip" \
   ] \
 }' 'https://app.metricly.com/packages'
```

### Swagger Payload

Try installing the package for yourself in Swagger using the below template.

```
{
  "archives": [
    "https://github.com/netuitive-community-packages/netuitive-packages-linux/archive/master.zip"
  ]
}
```

### Response Body

The following response body returns the package's details and confirms installation.

```
{
  "packages": [
    {
      "id": "f4a226ea-510f-3f27-8ca2-4e7211128728",
      "tenantId": "0fa5384a-3b36-4766-ad68-43e7c6af54f6",
      "packageId": "netuitive.packages.linux",
      "version": "3.9.0",
      "name": "Netuitive Packages Linux",
      "description": "A set of Netuitive analytics configurations, polices, dashboards, and reports that are used to monitor performance of the default collectors in the Netuitive Agent (CPU, DiskSpace, DiskUsage, LoadAverage, Memory, Network, VMStat)",
      "authorName": "Netuitive Research",
      "authorEmail": "research@netuitive.com",
      "logo": "http://assets.app.netuitive.com/pkg/logo/netuitive/banner_logo.png",
      "downloadUrl": "https://github.com/netuitive-community-packages/netuitive-packages-linux/archive/master.zip",
      "userEmail": null,
      "created": "2020-02-27T22:37:04Z",
      "updated": "2020-02-27T22:37:04Z",
      "tags": [],
      "policies": [],
      "analyticConfigurations": [],
      "dashboards": []
    }
  ]
}
```
{{% /expand %}}

---

## POST to /packages/install
{{< button theme="success" href="https://app.metricly.com/swagger-ui.html#!/packages/installUsingPOST" >}} POST {{< /button >}} Use this endpoint to install custom packages using a local zip file.

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| User-Agent | header | string | User-Agent|
| userEmail  | query | string  | Email address registered in CloudWisdom account. |
| file  | formData  | file  |  A multipart/form data zip file. |

### Request URL

 `https://app.metricly.com/packages/install`

{{% notice tip %}}

CloudWisdom encourages that all custom packages be formatted, validated, and zipped using the metricly-cli: https://github.com/metricly/metricly-cli. Use these CLI commands in the following order: 1. `metricly package validate` 2. `metricly package format` 3. `metricly package create`.

{{% /notice %}}

### CURL

The following example requires **Content-Type: multipart/form-data** be specified.

```
curl -X POST --header 'Content-Type: multipart/form-data' --header 'Accept: application/json' --header 'User-Agent: none' {"type":"formData"} 'https://app.metricly.com/packages/install'
```

### Response Body

The following Response Body returns confirmation that the package has been created, complete with a unique **id**.

```
{
  "package": {
    "id": "f4a226ea-1111-2222-3333-4e7211128728",
    "tenantId": "0fa5384a-1111-0000-0000-43e7c6af54f6",
    "packageId": "netuitive.packages.linux",
    "version": "3.9.0",
    "name": "Netuitive Packages Linux",
    "description": "A set of Netuitive analytics configurations, polices, dashboards, and reports that are used to monitor performance of the default collectors in the Netuitive Agent (CPU, DiskSpace, DiskUsage, LoadAverage, Memory, Network, VMStat)",
    "authorName": "Netuitive Research",
    "authorEmail": "research@netuitive.com",
    "logo": "http://assets.app.netuitive.com/pkg/logo/netuitive/banner_logo.png",
    "downloadUrl": "https://github.com/netuitive-community-packages/netuitive-packages-linux/archive/master.zip",
    "userEmail": "null",
    "created": "2020-03-04T00:08:46Z",
    "updated": "2020-03-04T00:08:46Z",
    "tags": [],
    "policies": [],
    "analyticConfigurations": [],
    "dashboards": []
  }
}

```
{{% /expand %}}

---

## DELETE to /packages/{id}
{{< button theme="danger" href="https://app.metricly.com/swagger-ui.html#!/packages/uninstallUsingDELETE" >}} DELETE {{< /button >}} Use this endpoint to uninstall a package.

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| id | path | string | Unique ID of the package |
| User-Agent   | header  | string  | User-Agent  |

### Request URL

 `https://app.metricly.com/packages/{id}`

### CURL

The following example uninstalls the package belonging to the **id**  `f4a226ea-1111-2222-8ca2-4e7211128728`.

```
curl -X DELETE --header 'Accept: */*' --header 'User-Agent: none' 'https://app.metricly.com/packages/f4a226ea-1111-2222-8ca2-4e7211128728'
```

### Response Body

The following response body has no content with a 204 success code.

```
no content
```
{{% /expand %}}

---

## GET from /packages/{id}
{{< button theme="info" href="https://app.metricly.com/swagger-ui.html#!/packages/getUsingGET_2" >}} GET {{< /button >}} Use this endpoint to get an installed package.

{{% expand "View method details."%}}

### Parameters

| Parameter | Parameter Type | Data Type | Description |
|-------------|----------------|-----------|----------------------|
| id | path | string | Unique UUID of the installed package e.g. ``30dfa898-a49e-31e4-9e7f-fa07445752fc`` |

### Request URL

 `https://app.metricly.com/packages/{id}`

### CURL

The following example only requires the **id** (_not_ **packageId**) to be added to the Request URL.

```
curl -X GET --header 'Accept: application/json' 'https://app.metricly.com/packages/9b20b44c-aa37-39fa-b46b-9c17237337fe'

```

### Response Body

The following response body

```
{
  "package": {
    "id": "9b20b44c-aa37-39fa-b46b-9c17237337fe",
    "tenantId": "0fa5384a-3b36-4766-ad68-43e7c6af54f6",
    "packageId": "netuitive.packages.aws.cost",
    "version": "0.2.0",
    "name": "Netuitive Packages Total Cost",
    "description": "A set of assets to showcase total cost data captured by Metricly",
    "authorName": "Netuitive Research",
    "authorEmail": "research@netuitive.com",
    "logo": "http://assets.app.netuitive.com/pkg/logo/netuitive/banner_logo.png",
    "downloadUrl": "https://github.com/netuitive-community-packages/netuitive-packages-aws-cost/archive/master.zip",
    "userEmail": null,
    "created": "2018-07-27T01:26:00Z",
    "updated": "2018-07-27T01:26:00Z",
    "tags": [],
    "policies": [],
    "analyticConfigurations": [],
    "dashboards": [
      {
        "id": "54fc1a1b-d762-32b7-af4b-d6cd4e2dabd5",
        "name": null,
        "description": null,
        "layout": null,
        "properties": null,
        "widgets": null,
        "type": null,
        "private": true
      }
    ]
  }
}
```
{{% /expand %}}

---

## Modify an Existing Community Package

CloudWisdom has a [community GitHub for packages](https://github.com/netuitive-community-packages) available for download. You can install these via the API,  customize them to your liking, or even contribute with a completely new package. Let's simply modify an existing package to fit our needs.

{{% expand "View method details."%}}

**Prerequisite**: If you haven't already, install the [CLI](https://docs.metricly.com/api/api-cli/).

1\. Go to the [community GitHub for packages](https://github.com/netuitive-community-packages) and download the **netuitive-packages-linux** package as a .zip file.

2\. Unzip the contents.

3\. Navigate to the **policies** folder. Select **linux.-cpu.threshold.exceeded.json**.

```
{
  "policy": {
    "actions": [
      {
        "category": 3,
        "type": "event"
      }
    ],
    "conditions": [
      {
        "analytic": "actual",
        "level": 95,
        "metric": "netuitive.linux.cpu.total.utilization.percent",
        "operator": ">"
      }
    ],
    "deleted": false,
    "description": "The CPU on the SERVER instance has exceeded 95% for at least 15 minutes. The metric netuitive.linux.cpu.total.utilization.percent factors in cpu steal as part of its computation. Check cpu.total.steal for the instance. If the value is high, it could mean a neighboring virtual machine is hogging the physical cpu. For instances running in AWS, stopping and starting the EC2 should resolve the issue as the virtual machine is moved to a different hypervisor.",
    "duration": 900,
    "enabled": true,
    "name": "Linux - CPU Threshold Exceeded",
    "scope": {
      "elementTypes": [
        "SERVER"
      ]
    }
  }
}
```
4\. Notice the **level** of CPU total utilization is 95%. Let's lower that to 85% and update the description.


```
{
  "policy": {
    "actions": [
      {
        "category": 3,
        "type": "event"
      }
    ],
    "conditions": [
      {
        "analytic": "actual",
        "level": 85,
        "metric": "netuitive.linux.cpu.total.utilization.percent",
        "operator": ">"
      }
    ],
    "deleted": false,
    "description": "The CPU on the SERVER instance has exceeded 85% for at least 15 minutes. The metric netuitive.linux.cpu.total.utilization.percent factors in cpu steal as part of its computation. Check cpu.total.steal for the instance. If the value is high, it could mean a neighboring virtual machine is hogging the physical cpu. For instances running in AWS, stopping and starting the EC2 should resolve the issue as the virtual machine is moved to a different hypervisor.",
    "duration": 900,
    "enabled": true,
    "name": "Linux - CPU Threshold Exceeded",
    "scope": {
      "elementTypes": [
        "SERVER"
      ]
    }
  }
}
```

5\. Save the file & open the terminal/command prompt.

5\. Navigate to the root of the package folder.

6\. Enter `metricly package validate` to ensure the package is ready for formatting.

7\. Enter `metricly package format` to prepare the package.

9\. Enter `metricly package create` to create a pkg.zip (located in the folder).

10\. Install the package via a POST request to **/packages/install**. Successful package installations return a JSON template with a unique **id** for the package.

{{% notice tip %}}
You can build complete packages from scratch or add/remove content from available packages found in the GitHub library. Virtana recommends starting with an existing package as a template before creating a completely custom package.
{{% /notice %}}

{{% /expand %}}
