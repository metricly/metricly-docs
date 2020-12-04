---
title: "Jenkins Metrics"
#date: 2018-12-11
draft: false
tags: [ "integrations", "metrics"]
author: Lawrence Lane
---

This plugin creates a single element---whose element name is determined by the configured hostname---with the following metrics:

| Fully Qualified Name(FQN) | Units | Statistic* | Description |
|------------------------------|-------|------------|------------------------------------------------------------|
| jenkins.[job-name].waiting | ms | timer | Time (in ms) the job was waiting before starting the build. |
| jenkins.[job-name].duration | ms | timer | Time (in ms) the job took to run. |
| jenkins.[job-name].completed | jobs | count | Count of completed jobs. |
| jenkins.[job-name].success | jobs | count | Count of successful jobs. |
| jenkins.[job-name].failure | jobs | count | Count of failed jobs. |
