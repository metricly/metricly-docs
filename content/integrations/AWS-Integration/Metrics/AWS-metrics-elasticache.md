---
title: "Elasticache Metrics"
date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started", "metrics"]
tags: ["aws", "metrics", "elasticache"]
author: Lawrence Lane
---
Elasticache instances can come in a few “flavors”, which means metrics are unique to each “flavor” of Elasticache.

 - Host-level metrics are present on both Memcached as well as Redis clusters
 - Memcached metrics are available only on Memcached clusters, Memcached 1.4.14 metrics are only available on Memcached clusters using at least version 1.4.14
 - Redis metrics are present only on Redis clusters.

## Collected

| Metric Type      | Fully Qualified Name (FQN)                   | AWS Metric                   | Statistic | Units   | Max  | BASE | CORR | UTIL |
|------------------|----------------------------------------------|------------------------------|-----------|---------|------|------|------|------|
| Host-level       | aws.elasticache.cpuutilization               | CPUUtilization               | average   | percent | 100  | yes  | yes  | yes  |
| Host-level       | aws.elasticache.freeablememory               | FreeableMemory               | average   | bytes   | none | yes  | no   | no   |
| Host-level       | aws.elasticache.networkbytesin               | NetworkBytesIn               | average   | bytes   | none | yes  | yes  | no   |
| Host-level       | aws.elasticache.networkbytesout              | NetworkBytesOut              | average   | bytes   | none | yes  | yes  | no   |
| Host-level       | aws.elasticache.swapusage                    | SwapUsage                    | average   | bytes   | none | yes  | no   | no   |
| Memcached        | aws.elasticache.bytesreadintomemcached       | BytesReadIntoMemcached       | average   | bytes   | none | yes  | no   | no   |
| Memcached        | aws.elasticache.bytesusedforacheitems        | BytesUsedForCacheItems       | average   | bytes   | none | yes  | no   | no   |
| Memcached        | aws.elasticache.byteswrittenoutfrommemcached | BytesWrittenOutFromMemcached | average   | bytes   | none | yes  | no   | no   |
| Memcached        | aws.elasticache.casbadval                    | CasBadVal                    | sum       | count   | none | yes  | no   | no   |
| Memcached        | aws.elasticache.cashits                      | CasHits                      | sum       | count   | none | yes  | no   | no   |
| Memcached        | aws.elasticache.casmisses                    | CasMisses                    | sum       | count   | none | yes  | no   | no   |
| Memcached        | aws.elasticache.cmdflush                     | CmdFlush                     | sum       | count   | none | yes  | no   | no   |
| Memcached        | aws.elasticache.cmdget                       | CmdGet                       | sum       | count   | none | yes  | no   | no   |
| Memcached        | aws.elasticache.cmdset                       | CmdSet                       | sum       | count   | none | yes  | no   | no   |
| Memcached        | aws.elasticache.currconnections              | CurrConnections              | sum       | count   | none | yes  | yes  | no   |
| Memcached        | aws.elasticache.curritems                    | CurrItems                    | sum       | count   | none | yes  | no   | no   |
| Memcached        | aws.elasticache.decrhits                     | DecrHits                     | sum       | count   | none | yes  | no   | no   |
| Memcached        | aws.elasticache.decrmisses                   | DecrMisses                   | sum       | count   | none | yes  | no   | no   |
| Memcached        | aws.elasticache.deletehits                   | DeleteHits                   | sum       | count   | none | yes  | no   | no   |
| Memcached        | aws.elasticache.deletemisses                 | DeleteMisses                 | sum       | count   | none | yes  | no   | no   |
| Memcached        | aws.elasticache.evictions                    | Evictions                    | sum       | count   | none | yes  | yes  | no   |
| Memcached        | aws.elasticache.gethits                      | GetHits                      | sum       | count   | none | yes  | no   | no   |
| Memcached        | aws.elasticache.getmisses                    | GetMisses                    | sum       | count   | none | yes  | no   | no   |
| Memcached        | aws.elasticache.incrhits                     | IncrHits                     | sum       | count   | none | yes  | no   | no   |
| Memcached        | aws.elasticache.incrmisses                   | IncrMisses                   | sum       | count   | none | yes  | no   | no   |
| Memcached        | aws.elasticache.reclaimed                    | Reclaimed                    | sum       | count   | none | yes  | no   | no   |
| Memcached 1.4.14 | aws.elasticache.bytesusedforhash             | BytesUsedForHash             | average   | bytes   | none | yes  | no   | no   |
| Memcached 1.4.14 | aws.elasticache.cmdconfigget                 | CmdConfigGet                 | sum       | count   | none | yes  | no   | no   |
| Memcached 1.4.14 | aws.elasticache.cmgconfigset                 | CmdConfigSet                 | sum       | count   | none | yes  | no   | no   |
| Memcached 1.4.14 | aws.elasticache.cmdtouch                     | CmdTouch                     | sum       | count   | none | yes  | no   | no   |
| Memcached 1.4.14 | aws.elasticache.currconfig                   | CurrConfig                   | average   | count   | none | yes  | no   | no   |
| Memcached 1.4.14 | aws.elasticache.evictedunfetched             | EvictedUnfetched             | sum       | count   | none | yes  | no   | no   |
| Memcached 1.4.14 | aws.elasticache.expiredunfetched             | ExpiredUnfetched             | sum       | count   | none | yes  | no   | no   |
| Memcached 1.4.14 | aws.elasticache.slabsmoved                   | SlabsMoved                   | sum       | count   | none | yes  | no   | no   |
| Memcached 1.4.14 | aws.elasticache.touchhits                    | TouchHits                    | sum       | count   | none | yes  | no   | no   |
| Memcached 1.4.14 | aws.elasticache.touchmisses                  | TouchMisses                  | sum       | count   | none | yes  | no   | no   |
| Redis            | aws.elasticache.bytesusedforcache            | BytesUsedForCache            | average   | bytes   | none | yes  | no   | no   |
| Redis            | aws.elasticache.cachehits                    | CacheHits                    | sum       | count   | none | yes  | yes  | no   |
| Redis            | aws.elasticache.cachemisses                  | CacheMisses                  | sum       | count   | none | yes  | yes  | no   |
| Redis            | aws.elasticache.currconnections              | CurrConnections              | sum       | count   | none | yes  | yes  | no   |
| Redis            | aws.elasticache.evictions                    | Evictions                    | sum       | count   | none | yes  | yes  | no   |
| Redis            | aws.elasticache.hyperloglogbasedcmds         | HyperLogLogBasedCmds         | sum       | count   | none | yes  | no   | no   |
| Redis            | aws.elasticache.ismaster                     | IsMaster                     | sum       | count   | none | yes  | no   | no   |
| Redis            | aws.elasticache.newconnections               | NewConnections               | sum       | count   | none | yes  | no   | no   |
| Redis            | aws.elasticache.reclaimed                    | Reclaimed                    | sum       | count   | none | yes  | no   | no   |
| Redis            | aws.elasticache.replicationbytes             | ReplicationBytes             | average   | bytes   | none | yes  | no   | no   |
| Redis            | aws.elasticache.replicationlag               | ReplicationLag               | average   | seconds | none | yes  | no   | no   |
| Redis            | aws.elasticache.saveinprogress               | SaveInProgress               | max       | count   | 1    | yes  | no   | no   |
| Redis            | aws.elasticache.curritems                    | CurrItems                    | sum       | count   | none | yes  | no   | no   |
| Redis            | aws.elasticache.gettypecmds                  | GetTypeCmds                  | sum       | count   | none | yes  | no   | no   |
| Redis            | aws.elasticache.hashbasedcmds                | HashBasedCmds                | sum       | count   | none | yes  | no   | no   |
| Redis            | aws.elasticache.keybasedcmds                 | KeyBasedCmds                 | sum       | count   | none | yes  | no   | no   |
| Redis            | aws.elasticache.listbasedcmds                | ListBasedCmds                | sum       | count   | none | yes  | no   | no   |
| Redis            | aws.elasticache.setbasedcmds                 | SetBasedCmds                 | sum       | count   | none | yes  | no   | no   |
| Redis            | aws.elasticache.settypecmds                  | SetTypeCmds                  | sum       | count   | none | yes  | no   | no   |
| Redis            | aws.elasticache.sortedsetbasedcmds           | SortedSetBasedCmds           | sum       | count   | none | yes  | no   | no   |
| Redis            | aws.elasticache.stringbasedcmds              | StringBasedCmds              | sum       | count   | none | yes  | no   | no   |

## Computed

| Friendly Name      | Fully Qualified Name (FQN)                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                   | Units   | Max | BASE | CORR | Related Global Policies                    |
|--------------------|---------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|-----|------|------|--------------------------------------------|
| Cache Hit Rate     | netuitive.aws.elasticache.cachehitrate      | This metric provides the percentage of hits against the cacheComputation:(data[‘aws.elasticache.cachehits’].actual + data[‘aws.elasticache.cachemisses’].actual) == 0 ? 0 : 100 *(data[‘aws.elasticache.cachehits’].actual / (data[‘aws.elasticache.cachehits’].actual + data[‘aws.elasticache.cachemisses’].actual))                                                                                                         | percent | 100 | yes  | yes  | AWS Elasticache Redis – Low Cache Hit Rate |
| Memory Utilization | netuitive.aws.elasticache.memoryutilization | Computation:100 * ((data[‘aws.elasticache.bytesusedforcache’].actual != undefined ? data[‘aws.elasticache.bytesusedforcache’].actual : data[‘aws.elasticache.bytesusedforcacheitems’].actual) / ((data[‘aws.elasticache.bytesusedforcache’].actual != undefined ? data[‘aws.elasticache.bytesusedforcache’].actual : data[‘aws.elasticache.bytesusedforcacheitems’].actual) + data[‘aws.elasticache.freeablememory’].actual)) | percent | 100 | yes  | yes  | AWS Elasticache – Cache Memory Utilization |
