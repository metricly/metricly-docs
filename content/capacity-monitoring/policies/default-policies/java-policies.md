---
title: "Java Policies"
#date: 2018-04-12
draft: false
categories:
tags: ["alerts", "notifications", "policies", "default policies", "java"]
author: Lawrence Lane
---

| Policy name                 | Duration | Conditions                                                                                                  | Category | Description                                                                                                                              |
|-----------------------------|----------|-------------------------------------------------------------------------------------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| Elevated JVM CPU Activity   | 15 min   | cpu.used.percent has an upper baseline deviation + an upper contextual deviation + a static threshold > 50% | WARNING  | This policy will generate a WARNING event when the JVM’s CPU activity is higher than expected. Additionally, the CPU usage is above 50%. |
| Elevated JVM Heap Usage     | 15 min   | netuitive.jvm.heap.utilizationpercent has an upper baseline deviation + an upper contextual deviation        | WARNING  | This policy will generate a WARNING event when the JVM’s heap usage is higher than expected.                                             |
| Elevated JVM System Threads | 15 min   | system.threads has an upper baseline deviation + an upper contextual deviation                              | WARNING  | This policy will generate a WARNING event when the number of system threads used by the JVM is higher than expected.                     |
