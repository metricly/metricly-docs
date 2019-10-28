---
title: "API"
#date: 2018-04-12
draft: false
categories:
tags: ["#api",]
author: Lawrence Lane
alwaysopen: false
pre:
weight: 15
---
CloudWisdom’s RESTful API allows you read and write data programmatically. This means that you can perform a wide variety of tasks, including adding a new integration, returning a filtered list of Events, removing elements from your account, and more.

To view and try out the available API endpoints, visit the [CloudWisdom Swagger UI](https://us.cloudwisdom.virtana.com/swagger-ui.html). This web based user interface allows users to view all the APIs, see additional documentation, and test the calls from your browser.

## Did you know we have a Metricly CLI?

Virtana strongly encourages you to use the Metricly CLI when interacting with our API. The CLI has built-in commands and help information, offering a guided experience when interacting with endpoints. You can create, delete, list, or get several of the features inside CloudWisdom through the CLI without having to worry about structuring the JSON payload exactly right. You can install the CLI from GitHub.

## Authentication
CloudWisdom requires users to authenticate their requests with HTTP basic auth. Basic authentication uses a standard HTTP header that includes encoded versions of your username and password. Basic authentication is required for all endpoints except ingest and ingest events, which require API keys.

## Data Formats
Dates and Times – All request parameters associated with date and time (duration, startTime, endTime) must be written in ISO 8601 format, see examples below.

| Unit     | ISO 8601   |
|------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Time (hours, minutes, and seconds) | hh:mm:ss or hhmmss (24-hour clock) |
| Time (hours and minutes)           | hh:mm or hhmm  |
| Duration                           | P<date>T<time> For duration, an upper case letter indicating a unit of date or time follows its corresponding numerical value. So, where n equals the value of each date or time, duration is written as follows: PnYnMnDnTnHnMnS. A duration of 1 year, 4 months, 6 days, 12 hours, 35 minutes, and 20 seconds, for example, is represented as P1Y4M6DT12H35M20S. Also, a duration of 1 month is represented as P1M, while a duration of 1 minute is represented as PT1. |
| Date (Year, Month, and Day)        | YYYY-MM-DD or YYYYMMDD |
| Date (Year and Month)              | YYYY-MM not YYYYMM   |
| Combined date and time             | <date>T<time> A combination of the date January 13, 2015 and the time 11:30 PM is written as 2015-01-13T23:30.  |


## Conditions

All request parameters associated with conditions (used in the Policy API) must follow a particular format. An example is below to show the syntax and ordering; a table follows to demonstrate the values and valid options.

| Attribute | Description and Examples   |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| metric    | The name of the metric(s) being used in the condition. Any full metric FQN. This attribute is left blank (e.g., “”) if using the wildcard method to define multiple metrics. Example(s) system.threads, emailgenerator.generateemail.calls, aws.elb.requestcount, metricly.metrics.collected.percent     |
| wildcard  | The wildcard-friendly metric name being used in the condition. Any metric-wildcard hybrid FQNs. Example(s) metricly.*.backend, aws.elb.httpcode*, aws.rds.*utilization  |
| analytic  | What type of analytic is being used in the condition. baselineDeviation, contextualDeviation, or actual (static threshold).  |
| operator  | "The operator to help define the analytic used in the condition. If baselineDeviation or contextualDeviation is the listed analytic: < (Lower Deviation) > (Upper Deviation) defined (Is Deviating) undefined (Is Not Deviating)If actual is the listed analytic: > (More Than) >= (More Than or Equal To) < (Less Than) <= (Less Than or Equal To) == (Equal To) != (Not Equal To) >= and <= (Between)  To use the Between operator for a Static Threshold analytic, you’ll have to create two “separate” conditions: one for the lower value and one for the upper value. | | "         |    |
| level     | The value to measure against for the Static Threshold analytic. Any rational number (integer, whole, or decimal number). Example(s) 123, -50, 111.476  |
