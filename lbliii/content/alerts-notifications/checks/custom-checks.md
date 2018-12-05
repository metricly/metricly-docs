---
title: "Custom Checks"
date: 2018-04-12
draft: true
categories:
tags: ["alerts", "notifications", "checks", "custom checks"]
author: Lawrence Lane
alwaysopen: false
---
Our platform is flexible to support any custom checks, but you will need a mechanism to schedule the scripts to run. Linux cron jobs or Window task scheduler will typically work for most cases. If you are running on the Linux platform our agent can also schedule the running of your scripts via the Users Scripts Integration. This option will allow you to schedule a script that may post to our REST API as output either a system check, or a time-series metric value, or even a text-based data. And it will remove the need for a separate scheduler or a loop function. The agent will execute the script on the small cycle as the data collection (ex. 60 seconds).

## The 4 parameters required to send custom checks

1. **apiId**: This is the API key that can be found by clicking on the corresponding integration (ex. Windows or Linux) on the integration page of our product once you are logged in. We suggest using the apiId associated with the element type (ex. Linux)
2. **checkName**: This is any name you want to give the check. It is the name that will show up in the user interface which you would also use to create an alerting policy.
3. **elementFqn**: This is the name of the element (ex. Linux hostname) that you want to associate with the system check. For example if you are checking if an application is running on `Server123`, you would set the `elementFqn` to `Server123`. If the element does not exist in the system, we will check an element with the type `check` and add it to the system. It is best practice to always associate a check with some monitored element.
4. **TTL**: The value is in seconds. It is the amount of time you would expect to see a response back from your check. This time can exactly match the time you are running the scheduled job, so for example the check could run every 60 seconds and have a 60 TTL. But we suggest putting in a buffer to deal with any small latency (ex. network or DNS delay) and prevent any “check flapping". A better example would be to set the check on a 60 second cycle and set the TTL for 90 seconds.

### Endpoint URL Format
```
https://api.app.metricly.com/check/{apiId}/{checkName}/{elementFqn}/{ttl}
```

### CURL Example
If you had a daily backup running on host `db1234`, you could run the following at the end of your backup script:
```
curl -X POST https://api.app.metricly.com/check/00000000000000000000000000000000/dailybackup/db1234/90000
```
25 hours (90000 seconds) is used as the check TTL to provide a one hour buffer in case backup times fluctuate a bit, reducing false alarms.
