---
title: "Etsy StatsD"
#date: 2018-12-11
draft: false
tags: ["statsd", "integrations" ]
author: Lawrence Lane
---
Etsy StatsD is one of the most popular StatsD libraries available. CloudWisdom offers a backend plugin for the Etsy StatsD library that allows you to send your StatsD metric data to CloudWisdom. We recommend using our Etsy StatsD integration if you currently have an Etsy StatsD server running and want to send your instrumented data to CloudWisdom. For more information about Etsy StatsD, see the following documentation.

## Configuration
### 1. Copy API key
1. From the left navigation menu, click **Integrations**.
2. Click the **Etsy | StatsD** card. Data collection should already be enabled, and a unique API key for your account has already been generated.
3. Copy the **API key**

### 2. Update Your StatsD Backends Directory
1. Clone the [Metricly StatsD Backend project](https://github.com/netuitive/statsd-netuitive-backend) to the desired location.
2. Copy the `metricly.js` file and the **entire metricly directory** to your StatsD backend directory. For more information about cloning existing repositories in Stash with Git, see the following [documentation](https://www.atlassian.com/git/tutorials/setting-up-a-repository).

### 3. Edit StatsD Config File
1. Open your local StatsD configuration file.
2. In your configuration file, add `./backends/metricly` to the backends section.

```
{
  backends:[
    "./backends/metricly"
  ]
}
```
3\. Add the following lines below the backends section:

```
{
  backends:[
    "./backends/metricly"
  ],
  metricly: {
    apiKey: "YOUR_API_KEY",
    apiHost: "api.us.cloudwisdom.virtana.com",
    apiPort: 443,
  }
}
```
4\. In order to associate StatsD metrics with an element in CloudWisdom, ensure that there is at least one mapping for CloudWisdom defined in the **mappings** section of your StatsD configuration file.

{{% notice tip %}}
Each mapping uses a pattern with a regular expression (`regex`) that corresponds with a set of keys in StatsD. The regex value can convert these keys to metrics that belong to an element in CloudWisdom. If the element or metric name is in the StatsD key, it can be represented by` $(regex-captured-group-number)`, demonstrated in the code below.
{{% /notice %}}

```
{
  backends:["./backends/metricly"],
  metricly: {
    apiKey: "YOUR_API_KEY",
    apiHost: "YOUR_METRICLY_API_HOST",
    apiPort: 443,
    mappings: [
      {
        pattern: "(.*?app.*?)\\.(.*?\\.mean)\\.gauge",
        element: {
          type: "APP Server",
          name: "$1",
          metric: {
            name: "$2"
          }
        }
      },
      {
        pattern: "(.*?app.*?)\\.(service.utilization)\\.gauge",
        element: {
          type: "APP Server",
          name: "$1",
          metric: {
            name: "$2",
            tags: [
              {"name": "utilization", "value":"true"}
            ]
          }
        }
      },
      {
        pattern: "\^(statsd\\..*)",
        element: {
          type: "StatsD",
          name: "StatsD",
          metric: {
            name: "$1"
          }
        }
      },
      {
        pattern: "\^(timestamp_lag.*)",
        element: {
          type: "StatsD",
          name: "StatsD",
          metric: {
            name: "statsd.$1"
          }
        }
      }
    ]
  }
}
```
5\. We recommend that you set the `flushInterval` in your StatsD configuration file to **60000 milliseconds**. This will ensure that your StatsD data is collected by CloudWisdom every 1 minute.
6. Sa**v**e the configuration file and **restart** StatsD.
