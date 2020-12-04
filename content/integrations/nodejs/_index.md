---
title: "Node.js"
#date: 2018-12-12
draft: false
tags: ["node.js", "integrations" ]
author: Lawrence Lane
---
 You can monitor your Node.js-based applications using the Linux Agent and Metricly StatsD server. All it takes is installing our agent and instrumenting your custom metrics, and then you’ll be visualizing the performance of your Node.js applications.

## Prerequisites
- [Linux Agent][1]

## Configure

1. Navigate to the **netuitive-agent.conf** file
2. Update **statsd** to `enabled = True`.

```
 # local statsd server
[[[statsd]]]
enabled = True
```

3\. Ensure Node.js is installed properly using the `node` command.  
4. StatsD requires a client library to push metrics, so you’ll need to install a Node.js library. For this example, we’ll be implementing the statsd-client. The open source community also has many Node.js libraries for StatsD that should all work with our agent.

```
npm install statsd-client
```

5\. Import the client into your application file and specify the location of the Metricly StatsD backend. By default, the Metricly StatsD runs on localhost port 8125 (as specified in the `/opt/netuitive-agent/conf/netuitive-agent.conf` file).  

```
var SDC = require('statsd-client'),
	client = new SDC({host: 'statsd.example.com', port: 8125});
```

6\. Instrument your application code by calling the appropriate functions.

```
// Counter Increment – Count occurrences of an event
client.increment('example.data.counterup');

//Counter Decrement - Subtract values from metrics
client.decrement('example.data.counterdown', -10);

// Timer – Measure the amount of time anaction took to complete
client.timing('example.data.timer', 250);

// Gauge – Set an static value andcompare against it to evaluate fluctuations
client.gauge('example.data.gauge', 5);

// Histogram - Create a histogram with tags
client.histogram('example.data.histogram', 10, {foo: 'bar'})
```

7\. **Save** and **restart** your application _and_ the Linux Agent.

[1]: /integrations/agents/linux-agent 
