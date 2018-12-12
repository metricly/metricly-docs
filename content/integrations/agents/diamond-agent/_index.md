---
title: "Diamond Agent"
date: 2018-12-11
draft: false
tags: ["diamond", "integrations", "agents" ]
author: Lawrence Lane
---
Diamond’s default HTTP Post Handler can be used to send Diamond data to Metricly.

## Configuration
### 1. Copy the unique API key from the Diamond integration in your account
1. In Metricly, navigate to **Integrations**.
2. Click the **Diamond** card. Data collection should already be enabled, and a unique API key for your account has already been generated.
3. **Copy** the API key.

### 2. Install & Configure Diamond
1. **Download** and **install** Diamond using the instructions found [here](http://diamond.readthedocs.io/en/latest/).
2. **Open** your `diamond.conf` file. It can usually be found in `/etc/diamond/diamond.conf`.
3. Under `[[HttpPostHandler]]` in the `[handlers]`, change the url setting to the following:

```
[[HttpPostHandler]]
### Url to post the metrics
url = http://api.app.metricly.com/diamond/API_KEY
```
Substitute _API_KEY_ for your unique API key.
4\. Adjust the batch size to 256 for monitoring general server metrics.

```
### Metrics batch size
batch = 256
```
5\. **Save** the `diamond.conf` file and **restart** Diamond.

This integration’s package (computed metrics, dashboards, and policies that will give you important events and alerts) will be automatically enabled and provisioned to your account as soon as Metricly receives data from the integration. The PACKAGES button on the integration setup page will become active once data is received, so you’ll be able to disable and re-enable the package at will.
