---
title: "Interpret Exceptions"
#date: 2018-12-12
draft: false
tags: ["#ruby", "#integrations", "#agents" ]
author: Lawrence Lane
---

_IF_ **sendErrorEvents** is `enabled` in the netuitive_rails_agent config/agent.yaml file _AND_ **actionErrorsEnabled** and/or **sidekiqEnabled**  = `true`, exceptions are sent to CloudWisdom as external events.

An Exception External event has the following tags to help you dissect the exception:

| Tag        | Description                                                                                |
|------------|--------------------------------------------------------------------------------------------|
| Action     | The action the error originated from.                                                      |
| Controller | The name of the controller that the exception came from.                                   |
| Exception  | The type of exception.                                                                     |
| Sidekiq    | If true, this exception comes from sidekiq. If false, this exception comes from elsewhere. |
| URI        | The resource identifier that names the resource the exception came from.                   |

Because these tags are located within the message body, you can create a [policy][1] matching against the body of the message.

[1]: /capacity-monitoring/policies
