---
title: "Route 53 Metrics"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started", "metrics"]
tags: ["aws", "metrics", "route53" ]
author: Lawrence Lane
---
## Collected

| FULLY QUALIFIED NAME (FQN) | DESCRIPTION | STATISTIC | UNITS | BASE | CORR |
|------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|-----------|-------------------------------|------|------|
| aws.route53.healthcheckstatus | The status of the health check endpoint that CloudWatch is checking. 1 indicates healthy, and 0 indicates unhealthy. | min | none | no | no |
| aws.route53.healthcheckpercentagehealthy | The percentage of Route 53 health checkers that consider the selected endpoint to be healthy. | min | percent | yes | no |
| aws.route53.connectiontime | The average time it took Route 53 health checkers to establish a TCP connection with the endpoint. | avg | miliseconds | yes | yes |
| aws.route53.timetofirstbyte | The average time that it took Route 53 health checkers to receive the first byte of the response to an HTTP or HTTPS request. | avg | miliseconds | yes | yes |
| aws.route53..sslhandshaketime | The average time it took Route 53 health checkers to complete the SSL handshake. | avg | miliseconds | yes | no |
| aws.route53.childhealthcheckhealthycount | The number of health checks that are healthy . | avg | count (healthy health checks) | yes |  |
