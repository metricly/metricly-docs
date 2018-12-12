---
title: "ECS Metrics"
date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started", "metrics"]
tags: ["aws", "metrics", "ecs"]
author: Lawrence Lane
---

## Collected

| Cluster | Service | Fully Qualified Name (FQN)               | AWS Metric                           | Statistic | Units   | Max  | BASE | UTIL |
|---------|---------|------------------------------------------|--------------------------------------|-----------|---------|------|------|------|
| yes     | no      | aws.ecs.cpureservation                   | CPUReservation                       | average   | percent | 100  | yes  |      |
| yes     | no      | aws.ecs.memoryreservation                | MemoryReservation                    | average   | percent | 100  | yes  |      |
| yes     | yes     | aws.ecs.cpuutilization                   | CPUUtilization                       | average   | percent | 100  | yes  | yes  |
| yes     | yes     | aws.ecs.memoryutilization                | MemoryUtilization                    | average   | percent | 100  | yes  | yes  |
| yes     | no      | aws.ecs.activeservicecount               | Active Service Count                 | average   |         | none | yes  |      |
| yes     | no      | aws.ecs.pendingtaskcount                 | Pending Task Count                   | average   |         | none | yes  |      |
| yes     | no      | aws.ecs.registeredcontainerinstancecount | Registered Containers Instance Count | average   |         | none | yes  |      |
| yes     | no      | aws.ecs.runningtaskcount                 | Running Task Count                   | average   |         | none | yes  |      |
            
