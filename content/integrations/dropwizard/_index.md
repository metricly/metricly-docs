---
title: "Dropwizard"
#date: 2018-12-11
draft: false
tags: ["dropwizard", "integrations", "custom metrics"]
author: Lawrence Lane
---

Dropwizard is part Java framework and part Java library that assists in operating web services. Dropwizard will take your web application and run it locally, recording metrics on its performance. You can integrate with Dropwizard via our custom Dropwizard Metrics Library to send these metrics to a StatsD server, which you can then forward to Metricly.

## Configuration
1. Include the appropriate Ananke library dependency. You’ll also need a working StatsD (Metricly StatsD or Etsy StatsD) integration.
2. Include the appropriate dropwizard-metrics dependency for the build manager of your choice.

```
<dependency>
  <groupId>com.metriclyicly</groupId>
  <artifactId>dropwizard-metrics</artifactId>
  <version>1.0.0</version>
  <type>pom</type>
</dependency>
```
3\. Add the following to your Dropwizard config.yml file:

```
metrics:
  frequency: 1 minute
  reporters:
    - type: metriclyicly
      host: metriclyicly-agent
      port: 8125
```
