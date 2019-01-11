---
title: "Metrics"
#date: 2018-12-11
draft: false
tags: ["#httpd", "#integrations", "#metrics" , "#collectors"]
author: Lawrence Lane
---

## Collected

| Fully Qualified Name (FQN)    | Type    | Units | Statistic | Min | Max  | Sparse Data Strategy (SDS) | BASE | CORR | UTIL |
|-------------------------------|---------|-------|-----------|-----|------|----------------------------|------|------|------|
| httpd.<host>.BusyWorkers      | GAUGE   | count | average   | 0   | none | none                       | yes  | no   | no   |
| httpd.<host>.BytesPerReq      | GAUGE   | bytes | average   | 0   | none | none                       | yes  | no   | no   |
| httpd.<host>.BytesPerSec      | GAUGE   | Bps   | average   | 0   | none | none                       | yes  | no   | no   |
| httpd.<host>.CleanupWorkers   | GAUGE   | count | average   | 0   | none | none                       | yes  | no   | no   |
| httpd.<host>.ClosingWorkers   | GAUGE   | count | average   | 0   | none | none                       | yes  | no   | no   |
| httpd.<host>.DnsWorkers       | GAUGE   | count | average   | 0   | none | none                       | yes  | no   | no   |
| httpd.<host>.FinishingWorkers | GAUGE   | count | average   | 0   | none | none                       | yes  | no   | no   |
| httpd.<host>.IdleWorkers      | GAUGE   | count | average   | 0   | none | none                       | yes  | no   | no   |
| httpd.<host>.KeepaliveWorkers | GAUGE   | count | average   | 0   | none | none                       | yes  | no   | no   |
| httpd.<host>.LoggingWorkers   | GAUGE   | count | average   | 0   | none | none                       | yes  | no   | no   |
| httpd.<host>.ReadingWorkers   | GAUGE   | count | average   | 0   | none | none                       | yes  | no   | no   |
| httpd.<host>.ReqPerSec        | GAUGE   | ops   | average   | 0   | none | none                       | yes  | no   | no   |
| httpd.<host>.TotalAccesses    | COUNTER | count |           | 0   | none | none                       | yes  | no   | no   |
| httpd.<host>.WritingWorkers   | GAUGE   | count | average   | 0   | none | none                       | yes  | no   | no   |
