---
title: "Windows Checks"
#date: 2018-04-12
draft: false
categories:
tags: ["alerts", "notifications", "checks", "windows"]
author: Lawrence Lane
alwaysopen: false
---

## Enable Windows Checks

1. Make sure the Windows agent is installed.
2. CloudWisdom checks can be enabled via the configuration files included with the agent.
3. All checks configuration files for the Windows agent can be found in `C:/Program Files (x86)/CollectdWin/conf/` or `C:/Program Files/CollectdWin/conf/` (depending on the version of windows).
4. Simply change the `enable` setting for the `ReadSystemChecks` from `false` to `true` in the `CollectdWin.config` file to enable the system checks.
5. To configure the checks, edit the `ReadSystemChecks.conf` file.

Currently, CloudWisdom comes with three pre-built checks: Heartbeat, Processes, and Ports. These are turnkey checks that do not require any scripting or coding, just simple configuration setting in the respective configuration files.

### Heartbeat Checks
This check **is enabled** by default. The Heartbeat check is to monitor the state of the agent. This check is enabled by default so no additional configuration is required once the Windows Checks have been enabled.

To disable this check, open the ``../CollectdWin/conf/ReadSystemChecks.config`` and change the `EnableAgentHeartbeat` setting to `false`.

Note that each check has a TTL (time to live) timer which is expressed as a multiple of the agent collection interval time. The default agent collection interval is 60 seconds so a TTLMultiplier of 2.0 would mean that the check timer would expire if no new post has been made to the API within 120 seconds. The minimum value allowed is 1.0 and decimal values are allowed. The intent is to have the TTL timer slightly be longer in duration than the posting frequency for the checks. This will allow some buffer and avoid potential “flapping” due to network latency or processing delays.

```
<readsystemchecks enableagentheartbeat="true" heartbeatttlmultiplier="2.0"> </readsystemchecks>
```
### HTTP Checks
Configure HTTP checks to send an `HTTP GET` request to a URL. If a successful response is returned a check is sent to CloudWisdom. By default, no HTTP checks are configured.

**Add something like:**
```
<HttpCheck Name="MyTestHTTPCheck" Url="http://www.google.com" StatusMatches="^(?!4|5)" />
```
**To your ReadSystemChecks.config file:**

```
<ReadSystemChecks EnableAgentHeartbeat="true" HeartbeatTTLMultiplier="2.5">

  <Checks>

  <HttpCheck Name="MyTestHTTPCheck" Url="http://www.google.com" StatusMatches="^(?!4|5)" />
 </Checks>
</ReadSystemChecks>
```

- **Name**: This is used as the name of the check in CloudWisdom if Alias is not set.
- **URL**: This is the URL to test. A check is sent if an `HTTP GET` request sent to the given URL returns a successful response. Redirects are automatically followed.
- **StatusMatches**: (optional) A regular expression to evaluate a successful response code. The default expression is ``^2`` which matches any `2xx` code.
Other examples:
   - ``^(?!4|5)`` : any code except `4xx` or `5xx`
   - ``^(2|3)`` : any `2xx` or `3xx` code
- **AuthHeader**:  (optional) An authorization header to send with the request. e.g., `Basic dXNlcm5hbWU6cGFzc3dvcmQ`
- **Alias**: (optional) An alias to use for the check name in CloudWisdom.
- **TTLMultiplier**: (optional) Sets the time-to-live of the check as a multiple of the agent execution interval. For example, if the agent is configured to collect data every 60 seconds (the default) and the check is configured with a TTLMultiplier of 2.5 (the default) then the next check must be received by CloudWisdom within 150 seconds in order to pass.

### Process and Service Checks

-  **Service checks**:  verify whether a Windows Service is in the running state
-  **Process checks**:  verify whether a process of the given name is in the list of processes running on the computer.

By default, no process or service checks are enabled.

**To add a new check:**

1. Edit the ``../CollectdWin/conf/ReadSystemChecks.config`` file
2. Insert a new entry between the … tags:
  - The check can be either Service or Process.
    - **Service Check**: the `Name` setting is the service name. This can be found by opening the service in the Service Control Manager (note that it is the Service Name, not the Display Name).
    - **Process Check**: the `Name` setting is is the process name as it appears in the performance monitor process list (this is typically the same as it appears in Task Manager but without the file extension).
3. (Optional) set the `TTLMultiplier` to configure the check time-to-live as a multiple of the agent collection interval.
    - For example, if the agent is configured to collect data every 60 seconds (the default) and the check is configured with a TTLMultiplier of 2.5 (the default) then the next check must be received by CloudWisdom within 150 seconds in order to pass.
    - The minimum allowed value is 1.0, but we recommended that it is set slightly higher to allow for processing time and network latency etc.
4. (Optional) You can add `Alias=”my check alias”` setting to provide an alias for the check received by CloudWisdom. If it is not supplied then the process name is used.
5. (Advanced) To capture multiple processes with a single check you can add `UseRegex=”true”` to the check configuration. With this set to true the `Name` field is used as a regular expression instead of an exact match and may match several processes.

```
<ServiceCheck Name="MSSQLSERVER" Alias="sqlservercheck" TTLMultiplier="2.5"/>
<ProcessCheck Name="Process123" Alias="process123" TTLMultiplier="2.5"/>
```
### Port Checks
**No port checks are configured** by default.To configure the port checks requires the same steps documented above for the Service and Process checks except that the Name is simply the check name and the Port must be specified.
```
 <PortCheck Name="ApplicationABC" Port="8081"/>
 ```
