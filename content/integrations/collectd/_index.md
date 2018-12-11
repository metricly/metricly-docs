---
title: "Collectd"
date: 2018-12-11
draft: true
tags: ["collectd", "integrations" ]
author: Lawrence Lane
---

Collectd’s Write HTTP plugin can be used to configure collectd to send data to Metricly. If you need additional information about setting up Collectd, view [their wiki](https://collectd.org/wiki/index.php/First_steps).

## Configuration

### 1. Copy API Key in Metricly

1. From the top navigation menu, click **Integrations**.
2. Click the **collectd** card. Data collection should already be enabled, and a `unique API key` for your account has already been generated.
3. **Copy** the API key.

### 2. Install & Configure Collectd
Installation steps for collectd may vary widely between systems, so you’ll want to install collectd based on recommended steps for your distro and the version of collectd you downloaded. You can download the latest version of collectd [here](https://collectd.org/download.shtml).

1. After installing collectd, open your `collectd.conf` file. It can usually be found in `/etc/collectd.conf`.
2. Set the **Interval** to `60`. Setting the Interval to 60 will allow metrics to be collected and sent to Metricly every 60 seconds.
3. **Enable** the following plugins by uncommenting them:

```
LoadPlugin cpu
LoadPlugin disk
LoadPlugin interface
LoadPlugin load
LoadPlugin memory
LoadPlugin network
LoadPlugin processes
LoadPlugin write_http
```
4\.  In the `<Plugin write_http>` configuration section, replace **API_KEY** with the `unique API key` generated for your account that you copied in step 1.

```
<Plugin "write_http">
  <Node "example">
    URL "https://api.app.metricly.com/ingest/collectd/API_KEY";
    User "collectd"
    Password "weCh3ik0"
    Format JSON
    StoreRates true
  </Node>
</Plugin>
```
5\. **Save** the `collectd.conf` file.  
6. **Restart** collectd.  
7. Verify that collectd can determine its fully qualified hostname by checking the element name in your [Inventory Explorer][1]. The hostname should be unique. If collectd cannot correctly determine the hostname, set a unique hostname by replacing `unique_fqn_of_your_host` in the Hostname setting:

```
Hostname "unique_fqn_of_your_host"
```

This integration’s package (computed metrics, dashboards, and policies that will give you important events and alerts) will be automatically enabled and provisioned to your account as soon as Metricly receives data from the integration. The PACKAGES button on the integration setup page will become active once data is received, so you’ll be able to disable and re-enable the package at will.

[1]: /data-visualization/inventory
