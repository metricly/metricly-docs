---
title: "Netuitive StatsD"
#date: 2018-12-12
draft: false
tags: ["netuitive", "integrations", "netuitive statsd", "statsd", "custom metrics" ]
author: Lawrence Lane
---
The Netuitive StatsD integration interprets, aggregates, and forwards custom metrics generated from your application. Using the values instrumented from your application’s key actions and data (method calls, database queries, etc.), CloudWisdom aggregates the values, associates them with corresponding metrics, and analyzes them in our analytics cycles.

The Netuitive StatsD server comes pre-installed as part of the Linux Agent. We recommend setting up a Netuitive StatsD integration if you do not have a StatsD server already.

Metrics are taken into the server using the specified UDP format:

```
metric.name:floatvalue|metrictype|@samplerate|#tag1:value1, tag2,
tag3:value3
```

## Prerequisites
- [Linux Agent][1]

## Configure

1. Navigate to the Linux Agent configuration file, /`opt/netuitive-agent/conf/netuitive-agent.conf`.
2. Change the **enabled** setting to `True` in the [[[statsd]]] section of the file.
  - Optionally, adjust the listen (`listen_port and listen_ip`) and forward (`forward_ip`, `forward_port`, and `forward`) options. The listen settings tell the Linux Agent where to listen for metrics; typically the server that your application is located. The forward settings tell the Linux Agent where to send the information.
4. **Restart** the Linux Agent.

## Instrumentation
Netuitive StatsD will collect and organize your data as your application calls functions and methods. This data is flushed to the Metricly StatsD server every 60 seconds by default, and then aggregated in CloudWisdom’s five-minute batch analytics cycle. After CloudWisdom analyzes your data, it’s then graphed for you to see. The Metricly StatsD server will place all of your metrics under the StatsD namespace in the Metrics page. Metrics about the Netuitive StatsD server itself are organized under the netuitive-statsd namespace in the Metrics page.

Before you begin instrumenting custom metrics, you’ll need to find a language library to “talk” to the Netuitive StatsD server using certain metric types. Netuitive StatsD supports the following metric types:

### Counters
 Count how many times an event occurs.

```
example.counter:1|c
```

#### Example
Each time a different language is given in the function below, a metric’s value increments by one. If a language is not found, another metric is created to show how many times a language was not found.
```
//hello-translator.js

var Client = require('node-statsd-client').Client;

 var netuitiveStatsd =  new Client("localhost", 8125);

 function translateHello(language) {
     if (language == "German") {
        netuitiveStatsd.increment('myserver.data.german-counter')
         return "Hallo";
    }

     if (language == "Spanish") {
        netuitiveStatsd.increment('myserver.data.spanish-counter')
         return "Hola";
    }

     if (language == "French") {
        netuitiveStatsd.increment('myserver.data.french-counter')
         return "Bonjour";
    }

     else {
        netuitiveStatsd.increment('myserver.data.no-language-counter')
         return "Sorry, I don't recognize that language.";
    }
}

 var languageName = prompt("Please enter which language you want to translate 'Hello' to:");

alert(translateHello(languageName));
```
### Timers
Measure in milliseconds how long an action took.

```
example.timer:250|ms
```

#### example
We want to see how long it takes for our PHP server to count to 10000.


```
<?php

    $start = microtime(true);

    for ($x=0; $x<10000; $x++) {}

    $end = microtime(true);

    $finalTime = $end-$start;

    echo 'It took ' . $finalTime . ' seconds!';

    .timing('myserver.data.timer', $finalTime, 1);

?>
```

### Gauge
An arbitrary, persistent value (e.g., a fuel meter).

```
example.gauge:0.6|g
```
#### Example

Each time you order a pizza, you want to know what percentage of the pizza you ate.

```
#!/usr/bin/my ruby srv

    require 'rubygems' if RUBY_VERSION < '1.9.0'
    require './statsdclient.rb'

    Statsd.host = 'localhost'
    Statsd.port = 8125

    class Numeric
      def percent_of(n)
        self.to_f / n.to_f * 100.0
      end
    end

    def prompt(*args)
      print(*args)
      gets
    end

    #input variables
    total_pizza_slices = 0
    eaten = 0

    #user prompts
    total_pizza_slices = prompt "How many total slices made up the pizza? "

    eaten = prompt "How many slices did you eat? "

    #calculation
    percent_eaten = eaten.percent_of(total_pizza_slices)
    p "You ate #{percent_eaten} of the pizza!"
    Statsd.gauge('myserver.data.gauge', percent_eaten)
```

### Sets
A number of unique elements received over a set interval.

```
example.set:username|s
```
### Histograms
The statistical distribution of a set of values.

```
example.histogram:129|h
```

## Tagging
You can also pass in tags to any of your metrics like so:

```
netuitive_statsd.increment('login.errors', tags=['name', 'value'])
```

### Reserved Metric Tags
Netuitive StatsD already uses a few tags, so be mindful when passing in tags with StatsD metrics.

- **h**: Sets the hostname (element ID) of the element. The h tag should be replaced with caution, as replacing it with a custom value will create a separate, extra element.
- **un**: Sets the unit of the metric you’re creating. An exhaustive list of the units Netuitive StatsD supports can be found [here](https://github.com/Netuitive/kbn/blob/master/README.md).
- **sds**: Defines the strategy for replacing missing data. You can either replace missing data with a zero (ReplaceWithZero) or take no strategy at all (None). You should schedule a data push at least once in every five-minute cycle. If you cannot send data every five minutes, you should consider sending zeroes.
- **ty**: Sets the type of the element in Netuitive StatsD (e.g., SERVER).


## Optional Configuration

| Option       | Default   | Description                                                                                                        |
|--------------|-----------|--------------------------------------------------------------------------------------------------------------------|
| enabled      | TRUE      | Enable collecting Netuitive StatsD metrics.                                                                        |
| interval     | 60        | The interval (in seconds) at which to collect metrics.                                                             |
| listen_port  | 8125      | User Datagram Protocol (UDP) port to listen on.                                                                    |
| listen_ip    | 127.0.0.1 | IP address to listen on.                                                                                           |
| element_type | SERVER    | Element type applied to your netuitive-statsd server instance in CloudWisdom.                                         |
| prefix       | statsd    | Prefix applied to your netuitive-statsd metrics in CloudWisdom. Setting an empty prefix causes no prefix to be added. |
| forward_ip   | 127.0.0.1 | IP address to forward StatsD messages to.                                                                          |
| forward_port | 9125      | UDP port to forward StatsD messages to.                                                                            |
| forward      | FALSE     | Enable StatsD forwarding.                                                                                          |

[1]: /integrations/agents/linux-agent
