---
title: "Optional Config"
#date: 2018-12-12
draft: false
tags: ["#ruby", "#integrations", "#agents" ]
author: Lawrence Lane
---

## Log Options

- **logLocation**: The absolute path of the log file. Leave this option blank to use the default location in the gem directory.
- **logAge**: Specify either the number of log files to keep or the frequency of rotation (daily, weekly, or monthly).
- **logSize**: Specify the maximum log file size (in bytes).
- **debugLevel**: Options include (in ascending order of severity) error, info, and debug.

## Active Support Notifications

The active support notifications are a pub-sub model that trigger active support notifications when certain actions are performed within your rails application(s). Each flag is toggling a certain set of active support notifications for a subset of metrics in Metricly.

- **actionControllerEnabled**: Set to `true` to enable `action_conroller` metric collection.
- **activeRecordEnabled**: Set to `true` to enable `active_record` metric collection.
- **actionViewEnabled**: Set to `true` to enable `action_view` metric collection.
- **actionMailerEnabled**: Set to `true` to enable `action_mailer` metric collection.
- **activeSupportEnabled**: Set to `true` to enable `active_support` metric collection.
- **activeJobEnabled**: Set to `true` to enable `active_job` metric collection.

## Injected Instrumentation

- **requestWrapperEnabled**: Set to `true` to enable the queue time metric, which is the time (in ms) taken after a request enters your system and before it reaches your application. Metricly takes either the `X-Queue-Start` or `X-Request-Start` headers to calculate the queue time, but time unit types won’t be automatically converted.
- **actionErrorsEnabled**: Set to `true` to inject code into the action controller which will silently track exceptions. Exceptions will be sent to CloudWisdom as an external event. An errors metric will also be available on the Metrics page under the action_controller branch for the element that tracks the number of exceptions seen.

## Interpreter Metrics

- **gcEnabled**: Set to `true` to enable garbage collection metric collection.
- **objectSpaceEnabled**: Set to `true` to enable object space metric collection.

## 3rd Party

- **sidekiqEnabled**: Set to `true` to enable sidekiq metric and error collection.
  - Sidekiq metrics include number of jobs per queue, number of jobs ran per queue, and number of jobs ran per job.
  - Errors will be sent to CloudWisdom as an external event. An errors metric will also be available on the Metrics page under the sidekiq branch for the element that tracks the number of exceptions seen.

## Error Tracking Features

**sendErrorEvents**: Set to `true` to send exceptions from `sidekiq` and `action_controller` as events to Metricly.
  - If this setting is set to `false`, but actionErrorsEnabled and sidekiqEnabled are set to `true`, errors will not be sent to CloudWisdom as events but all metrics will still be collected.

## Feature Configs
- **queueTimeUnits**: The divisor required to convert the queue time metric into seconds (e.g., seconds = 1, milliseconds = 1000, microseconds = 1000000).
- **ignoredErrors**: List of exceptions to ignore. List should be provided in one of the following formats:

**yaml**

```
ignoredErrors:
- Runtime Error
- Argument Error
```

**environment variable**

```
netuitive_RAILS_IGNORED_ERRORS=RuntimeError,ArgumentError
```

{{% notice tip %}}
You can ignore exceptions that match agains an ancestor using a `^`, so `netuitive_RAILS_IGNORED_ERRORS=RuntimeError^` would ignore all errors that inherit from `RuntimeError`.

{{% /notice %}}
