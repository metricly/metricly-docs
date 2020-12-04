---
title: "ALB Metrics"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started", "metrics"]
tags: ["aws", "metrics", "alb" ]
author: Lawrence Lane
---
## Collected

| Friendly Name                      | Fully Qualified Name (FQN)                        | AWS Metric                     | Statistic | Sparse Data Strategy (SDS) | BASE |
|------------------------------------|---------------------------------------------------|--------------------------------|-----------|----------------------------|------|
| Active Connection Count            | aws.applicationelb.activeconnectioncount          | ActiveConnectionCount          | sum       | none                       | yes  |
| Client TLS Negotiation Error Count | aws.applicationelb.clienttlsnegotiationerrorcount | ClientTLSNegotiationErrorCount | sum       | none                       | yes  |
| Consumed LCUs                      | aws.applicationelb.consumedlcus                   | ConsumedLCUs                   | sum       | none                       | no   |
| Healthy Host Count                 | aws.applicationelb.healthyhostcount               | HealthyHostCount               | average   | none                       | yes  |
| HTTP Code ELB 4XX Count            | aws.applicationelb.httpcode_elb_4xx_count         | HTTPCode_ELB_4XX_Count         | sum       | ReplaceWithZero            | yes  |
| HTTP Code ELB 5XX Count            | aws.applicationelb.httpcode_elb_5xx_count         | HTTPCode_ELB_5XX_Count         | sum       | ReplaceWithZero            | yes  |
| HTTP Code Target 2XX Count         | aws.applicationelb.httpcode_target_2xx_count      | HTTPCode_Target_2XX_Count      | sum       | ReplaceWithZero            | yes  |
| HTTP Code Target 3XX Count         | aws.applicationelb.httpcode_target_3xx_count      | HTTPCode_Target_3XX_Count      | sum       | ReplaceWithZero            | yes  |
| HTTP Code Target 4XX Count         | aws.applicationelb.httpcode_target_4xx_count      | HTTPCode_Target_4XX_Count      | sum       | ReplaceWithZero            | yes  |
| HTTP Code Target 5XX Count         | aws.applicationelb.httpcode_target_5xx_count      | HTTPCode_Target_5XX_Count      | sum       | ReplaceWithZero            | yes  |
| New Connection Count               | aws.applicationelb.newconnectioncount             | NewConnectionCount             | sum       | none                       | yes  |
| Processed Bytes                    | aws.applicationelb.processedbytes                 | ProcessedBytes                 | sum       | none                       | yes  |
| RequestCount                       | aws.applicationelb.requestcount                   | RequestCount                   | sum       | ReplaceWithZero            | yes  |
| Request Count Per Target           | aws.applicationelb.requestcountpertarget          | RequestCountPerTarget          | average   | none                       | yes  |
| Rule Evaluations                   | aws.applicationelb.ruleevaluations                | RuleEvaluations                | average   | none                       | yes  |
| Target Connection Error Count      | aws.applicationelb.targetconnectionerrorcount     | TargetConnectionErrorCount     | sum       | ReplaceWithZero            | yes  |
| Target Response Time               | aws.applicationelb.targetresponsetime             | TargetResponseTime             | average   | ReplaceWithZero            | yes  |
| Unhealthy Host Count               | aws.applicationelb.unhealthyhostcount             | UnHealthyHostCount             | average   | none                       | yes  |

## Computed

| Fully Qualified Name (FQN)                   | Description                | Units      | BASE |
|----------------------------------------------|----------------------------|------------|------|
| netuitive.aws.alb.totaltargethttperrors      | Total Target HTTP Errors   | count      |   yes   |
| netuitive.aws.alb.totalelbhttperrors         | Total ALB HTTP Errors      | count      |   yes   |
| netuitive.aws.alb.httpcodeelberrorpercent    | ALB HTTP Error Percent     | percent    |   yes   |
| netuitive.aws.alb.unhealthyhostpercent       | Unhealthy Host Percent     | count      |  yes    |
| netuitive.aws.alb.requestspersecond          | Requests per Second        | operations |  yes    |
| netuitive.aws.alb.httpcodeelb4xxerrorpercent | ELB HTTP 4xx Error Percent | percent    |  yes    |
| netuitive.aws.alb.httpcodeelb5xxerrorpercent | ELB HTTP 5xx Error Percent | percent    |   yes   |
