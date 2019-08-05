---
title: "Riemann"
#date: 2018-12-12
draft: false
tags: ["#riemann", "#integrations" ]
author: Lawrence Lane
---
Riemann is a powerful network monitoring tool that aggregates events from your servers and applications using streams to process them in a format that makes them easy to manipulate or summarize. You can forward your events collected by Riemann streams to Metricly. The Riemann integration is very different from most of the other integrations: the integration is configured in Riemann to send data to Metricly using our API.


## Configure

1. Download the [Metricly Riemann library](https://github.com/riemann/riemann/tree/master/src/riemann/netuitive.clj).
2. Place the **metricly.clj** file in the `<riemann-directory>/etc` directory, where `<riemann-directory>` is the location of your Riemann files.
3. At the top of your **riemann.config** file (typically found at `<riemann-directory>/etc/riemann.config`), add:

```
(include "<riemann-directory>/etc/metricly.clj")
```
4\. At the bottom of the riemann.config file, add the following:

```
(def metricly-forwarder
  (batch 100 1/10
    (async-queue!
      :metricly-forwarder  ; A name for the forwarder
        {:queue-size     1e4  ; 10,000 events max
        :core-pool-size 5    ; Minimum 5 threads
        :max-pools-size 100} ; Maximum 100 threads
        (riemann.metricly/metricly {:api-key "metricly
-api-key" :type "Riemann"}))))
```

5\. Update the `:type` setting as necessary. This setting controls the element display name in Metricly.

{{% notice tip %}}
The `:type` setting will help provide a useful descriptor to your metrics. For example, if you’re using Riemann to pull in a group of metrics from your Elasticsearch instance, you could set the `:type` to `myElasticsearchInstance`.
{{% /notice %}}

6\. Replace the sample API key (`metricly-api-key`) with the API key from the Custom integration in your Metricly account.  

7\. Below the new **metricly-forwarder** code, add:

```
(streams
  metricly-forwarder
)
```
This will start pushing events using the `metricly-forwarder` definition.

## Optional Configure
### Printing Events and Sending to the Log file

In a new or existing stream, add the following to print all events to `STDOUT` and send events to the log.

```
(streams
  prn
  #(info %)
)
```

### Filtering Events
You can add additional qualifiers to the beginning of a stream to filter the events that are getting sent to Metricly.

Below is an example of filtering events that contain any of the listed tags for the service “web server”:

```
(streams
  (where (and (service "web server")
  (state "exception"))
    (tagged "controller"
      (email "5551234567@txt.att.net"))

    (tagged "view"
      (email "delacroix@trioptimum.com" "bronson@trioptimum.com"))

    (tagged "model"
      (email "staff@vonbraun.mil"))))
```

Below is an example of usgin a regex to find all metrics that start with “riemann server” and forwards only the matching metrics.

```
(streams
  (where (service #"riemann\sserver.*")
    metricly-forwarder
))
```
