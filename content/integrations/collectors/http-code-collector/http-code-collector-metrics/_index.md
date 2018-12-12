---
title: "Metrics"
date: 2018-12-11
draft: false
tags: ["http", "integrations", "metrics", "collectors"]
author: Lawrence Lane
---
This collector tracks per URL which response codes are received as well as the number of times each code was received as two separate metrics. The Response Code List metric’s value is the literal response code number at the time it was received. The Response Code count increments each time a response code is received; this means that you won’t have a metric for every response code until your web site serves up that response code.

## Collected

| Friendly Name       | Fully Qualified Name (FQN) | Description                                                                                             | Statistic | Units | Min | Max  | BASE | CORR | UTIL |
|---------------------|----------------------------|---------------------------------------------------------------------------------------------------------|-----------|-------|-----|------|------|------|------|
| Response Code List  | http.*.response_code       | The response code sent to the user.                                                                     | average   |       | 0   | none | none | yes  | no   |
| Response Code Count | http.*.response_code.#     | For each response code metric (as illustrated by the #), the number oftimes a response code was served. | average   |       | 0   | none | none | yes  | no   |
