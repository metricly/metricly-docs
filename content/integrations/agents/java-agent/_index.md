---
title: "Java Agent"
#date: 2018-12-11
draft: false
tags: ["#java", "#integrations","#agents"]
author: Lawrence Lane
---
Metricly’s Java agent is a java monitoring agent with a programmable bytecode instrumentation engine that’s enabled by adding a JVM integration in Metricly. The Metricly Java integration allows Metricly to collect JVM runtime system metrics like CPU, Memory, GC, Threads and Classes Count, and application components method performance statistics, such as number of calls and execution time.

## Prerequisites
Must have Java 6 Or greater.

## Configuration

### 1. Copy API key
1. From the top navigation menu, select Integrations.
2. Select the **Java** card. The name should be already populated, and Data Collection should be enabled. A unique API key for your account has already been generated.
3. Copy the **API key**.

### 2. Download the Netuitive Java agent

1. Download the [Netuitive Java agent](https://github.com/netuitive/zorka/releases/latest).
2. Unzip the `netuitive-zorka.zip` file to the desired location. We recommend that you unzip the `netuitive-zorka.zip` file near the app it is monitoring.

{{% notice tip %}}
You can also use the following command to obtain the most recent version of the Java Agent:   
`curl -s https://api.github.com/repos/Netuitive/zorka/releases/latest | jq -r ".assets[] | .browser_download_url"`
{{% /notice %}}

### Edit Config File

1. Navigate to the `zorka.properties` file that was included in the `netuitive-zorka-{version}.zip`.
2. Enable the `jvm.bsh` script and any other scripts as necessary at the top of the file.
3. Change **zorka.hostname** and **zorka.application** to the correct value. **zorka.hostname** should be the fully qualified domain name of the host and **zorka.application** should be the name of your Java application.
4. Optionally, if you’re setting up the Java agent on JBoss, you should change the **zorka.mbs.autoregister** setting to no.
5. Optionally, if you’d like the Zorka Log to be managed by the default syslog, change the **zorka.syslog** setting to yes. Read more about the **zorka.syslog** setting [here](http://zorka.io/install/logging.html).
6. Optionally, if you want Zorka to monitor clusters:
  - Uncomment **zorka.clusters** in the `zorka.properties` file and include the name of each element. The default setting (`cluster 1`, `cluster 2`) would create a JVM () element and two CLUSTER () elements with the names `cluster1` and `cluster2`.
    - `zorka.clusters = cluster1, cluster2`
  - If you want to specify the element type of the clusters, uncomment **zorka.clusters.type** and change the setting to the desired element type. If the type is not specified, the default is `CLUSTER`.
    - `zorka.clusters.type = CLUSTER`
7. Change the `netuitive.api.key` value to the unique API key generated for your account that you copied in step 1.
8. Ensure the **netuitive.api** value is set to yes to enable data push to Metricly.
9. Modify the **netuitive.api.interval** value to the desired data push interval (in seconds). The agent will collect data at the desired interval but aggregate the values each minute and send a single set of values to the API. Data is sent as statistics (_min_, _max_, _sum_, _avg_, and _count_) instead of raw values. Data in the Metrics pagefor your JVM metrics is displayed using gauges instead of a counter to capture any delta between data points.
10. **Restart** your app server with the following argument passed to the JVM (where the default path to the Netuitive Java agent unzipped directory is `/opt/netuitive-zorka/`):

```
 -javaagent:[path-to-netuitive-zorka-unzipped-dir]/netuitive.jar=[path-to-netuitive-zorka-unzipped-dir]
```

This integration’s package (computed metrics, dashboards, and policies that will give you important events and alerts) will be automatically enabled and provisioned to your account as soon as Metricly receives data from the integration. The PACKAGES button on the integration setup page will become active once data is received, so you’ll be able to disable and re-enable the package at will.

## Examples

We want to run the java application `zorka-core-test.jar` with our Java agent specified in the `-javaagent` JVM option.

```
 java -javaagent:/opt/netuitive-zorka/netuitive.jar=/opt/netuitive-zorka -jar zorka-core-test.jar
 ```
