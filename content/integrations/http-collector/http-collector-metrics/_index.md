---
title: "HTTP Collector Metrics"
#date: 2018-12-11
draft: false
tags: ["http", "integrations", "metrics", "collectors"]
author: Lawrence Lane
---

## Collected

| Friendly Name     | Fully Qualified Name (FQN)         | Description                                | Statistic |
|-------------------|------------------------------------|--------------------------------------------|-----------|
| Servers Http Time | servers.[hostname].http.[url].time | Time to download the page in microseconds. | average   |
| Servers Http Size | servers.[hostname].http.[url].size | Size of the page received in bytes.        | bytes     |
