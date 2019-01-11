---
title: "Garbage Collection"
#date: 2018-12-12
draft: false
tags: ["#ruby", "#integrations", "#agents" ]
author: Lawrence Lane
---

 The garbage collector attempts to return memory consumed by objects no longer in use by your application. Metricly can be used to collect metrics on how much time is spent in garbage collection for your Ruby applications. You should have Matz’s Ruby Interpreter (MRI) version 1.9.2 or greater or Ruby Enterprise Edition installed before enabling garbage collection metrics.

## Configure
1. Navigate to your application’s initialization file.
2. Add the following call (depending on your Ruby version) to the file:
  - For MRI v1.9.2 or greater: ```GC::Profiler.enable```
  - For Ruby Enterprise Edition: ```GC.enable_stats```
3. **Save** the file and **restart** your application.

{{% notice tip %}}
If you have a Rails application, you can add one of the calls above to an initializer in `config/initializers` or directly to your `config/application.rb`.
{{% /notice %}}
