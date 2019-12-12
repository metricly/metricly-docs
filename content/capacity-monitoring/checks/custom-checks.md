---
title: "Custom Checks"
#date: 2018-04-12
draft: false
categories:
tags: ["#alerts", "#notifications", "#checks", "#custom checks"]
author: Lawrence Lane
alwaysopen: false
---
CloudWisdom supports custom checks. These checks require scheduling mechanisms (such as Linux cron jobs or Windows task scheduler) to run.

**Using the Linux platform?**

When running on the Linux platform, our agent can also schedule your scripts via the Users Scripts Integration. You can then schedule a script that posts to our REST API as either a system check, a time-series metric value, even a text-based data. This removes the need for a separate scheduler or loop function. The agent executes the script on the small cycle as the data collection (ex. 60 seconds).


## The 4 parameters required to send custom checks

1. **apiId**: The API key found on the corresponding integration card in CloudWisdom.  (ex. Windows or Linux) on the integration page of our product once you are logged in. We suggest using the apiId associated with the element type (ex. Linux)
2. **checkName**:  Any name you want to give the check. It is the name that will show up in the user interface which you would also use to create an alerting policy.
3. **elementFqn**: This is the name of the element (ex. Linux hostname) that you want to associate with the system check. It is best practice to always associate a check with some monitored element.
4. **TTL**: The amount of time you expect to see a response back from your check. The value is in seconds. This time can exactly match the time you are running the scheduled job, but we suggest putting in a buffer to deal with any small latency (ex. network or DNS delay) and prevent check flapping.


### Endpoint URL Format
```
https://api.us.cloudwisdom.virtana.com/check/{apiId}/{checkName}/{elementFqn}/{ttl}
```

### CURL Example
If you had a daily backup running on host `db1234`, you could run the following at the end of your backup script:
```
curl -X POST https://api.us.cloudwisdom.virtana.com/check/00000000000000000000000000000000/dailybackup/db1234/90000
```
25 hours (90000 seconds) is used as the check TTL to provide a one hour buffer in case backup times fluctuate a bit, reducing false alarms.
