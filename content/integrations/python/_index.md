---
title: "Python"
#date: 2018-12-12
draft: false
tags: ["python", "integrations" ]
author: Lawrence Lane
---
You can monitor your Python applications using a Python web module, the Linux Agent, and the Metricly StatsD server.

## Prerequisites
- [Linux Agent][1]

## Configure

1. Navigate to the **netuitive-agent.conf** file.
2. Update the **StatsD** setting to `enabled = True`.

```
# local statsd server
[[[statsd]]]
enabled = True
```
3\. Download the **python web module** and extract the files.

```
>> wget http://webpy.org/static/web.py-0.37.tar.gz
>> tar xzvf web.py-0.37.tar.gz
```
4\. Move the web directory to the same folder as your application.

```
>> mv web.py-0.37/web /opt/python
```

5\. Download the **pystatsd** client from GitHub.

```
>> git clone https://github.com/jsocol/pystatsd.git
```

6\. Move the **statsd directory** to the same folder as your application.

```
>> cd pystatsd
>> mv statsd /opt/python/
```

7\. Import the **web** and **statsd** modules into your application’s code.

```
import web
import statsd
```

8\. Instrument your application code by calling the appropriate functions. Here's an example:

```
import web
import statsd

# Counter Increment
c.incr('example.data.counterup', 1)

# Counter Decrement
c.decr('example.data.counterdown', 1)

# Timer
c.timing('example.data.timer', 320)

# Gauge
c.gauge('example.data.gauge', 4)

urls = (
  '/', 'index'
)

class index:
  def GET(self):
    return "Hello, world!"

if __name__ == "__main__":
  app = web.application(urls, globals())
  app.run()
```
9\. **Save** and then **restart** your application and the Linux Agent.


[1]: /integrations/agents/linux-agent
