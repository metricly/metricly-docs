---
title: "MongoDB Metrics"
#date: 2018-12-11
draft: false
tags: ["#metrics", "#integrations", "#mongodb" ]
author: Lawrence Lane
---


| Fully Qualified Name (FQN)                          | Description                                                                                                                                                                                                | Units   | Min | Max  | BASE | CORR | UTIL |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|-----|------|------|------|------|
| metricly.linux.mongo.connections.utilizationpercent | The percentage of available connections currently being utilized. Computation: (mongo.connections.current / (mongo.connections.current +mongo.connections.available)) * 100                                | percent | 0   | 100  | yes  | no   | yes  |
| metricly.linux.mongo.opcounters.totalreads          | The total number of read operations currently taking place (reads include both query and getmore requests). Computation: mongo.opcounters.query + mongo.opcounters.germore                                 | count   | 0   | none | yes  | no   | no   |
| metricly.linux.mongo.opcounters.totalwrites         | The total number of write operations currently taking place (writes include insert, update, and delete requests). Computation: mongo.opcounters.insert + mongo.opcounters.update + mongo.opcounters.delete | count   | 0   | none | yes  | no   | no   |
