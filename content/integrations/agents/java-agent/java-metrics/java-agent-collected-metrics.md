---
title: "Collected Metrics"
date: 2018-12-11
draft: true
tags: ["java", "integrations", "metrics", "agents"]
author: Lawrence Lane
---


## Collected

| Fully Qualified Name (FQN)             | Description                                                                        | Statistic | Units        | Min | Max    | Sparse Data Strategy (SDS) | BASE | CORR | UTIL |
|----------------------------------------|------------------------------------------------------------------------------------|-----------|--------------|-----|--------|----------------------------|------|------|------|
| *.calls                                | The number of calls made to the method.                                            | sum       | count        | 0   | none   | none                       | yes  | no   | no   |
| *.errors                               | The number of method calls that resulted in errors.                                | sum       | count        | 0   | none   | none                       | yes  | no   | no   |
| *.time                                 | The amount of time spent executing the method totaled across all calls.            | sum       | milliseconds | 0   | none   | none                       | yes  | no   | no   |
| *.avg_time                             | The amount of time spent executing the method, averaged across allcalls.           | average   | milliseconds | 0   | none   | none                       | yes  | no   | no   |
| cpu.used.percent                       | The percentage of CPU used by the JVM.                                             | average   | percent      | 0   | 100    | none                       | yes  | yes  | yes  |
| gc.psmarksweep.collectiontime          | The amount of time the JVM spent doing “PS MarkSweep” garbagecollection.           | average   | milliseconds | 0   | 300000 | none                       | yes  | no   | no   |
| gc.psscavenge.collectiontime           | The amount of time the JVM spent doing “PS Scavenge” garbage collection.           | average   | milliseconds | 0   | 300000 | none                       | yes  | no   | no   |
| gc.concurrentmarksweep.collectiontime  | The amount of time the JVM spent doing “Concurrent MarkSweep” garbagecollection.   | average   | milliseconds | 0   | 300000 | none                       | yes  | no   | no   |
| gc.parnew.collectiontime               | The amount of time the JVM spent doing “ParNew MarkSweep” garbagecollection.       | average   | milliseconds | 0   | 300000 | none                       | yes  | no   | no   |
| gc.g1oldgeneration.collectiontime      | The amount of time the JVM spent doing “G1 Old Generation” garbagecollection.      | average   | milliseconds | 0   | 300000 | none                       | yes  | no   | no   |
| gc.g1newgeneration.collectiontime      | The amount of time the JVM spent doing “G1 Old Generation” garbagecollection.      | average   | milliseconds | 0   | 300000 | none                       | yes  | no   | no   |
| heap.committed                         | The total amount of memory available for the heap.                                 | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| heap.used                              | The total amount of memroy currently being used by the heap.                       | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| mempool.codecache.committed            | The amount of memory currently allocated to the code cache.                        | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| mempool.codecache.max                  | The maximum amount of memory that could be allocated to the code cache.            | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| mempool.codecache.used                 | The amount of committed memory currently used by the code cache.                   | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| mempool.compressedclassspace.committed | The amount of memory currently allocated to the compressed class space.            | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| mempool.compressedclassspace.max       | The maximum amount of memory that could be allocated to the compressedclass space. | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| mempool.compressedclassspace.used      | The amount of committed memory currently used by the compressed class space.       | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| mempool.metaspace.committed            | The amount of memory currently allocated to the metaspace.                         | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| mempool.metaspace.max                  | The maximum amount of memory that could be allocated to the metaspace.             | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| mempool.metaspace.used                 | The amount of committed memory currently used by the metaspace.                    | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| mempool.psedenspace.committed          | The amount of memory currently allocated to the eden space.                        | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| mempool.psedenspace.max                | The maximum amount of memory that could be allocated to the eden space.            | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| mempool.psedenspace.used               | The amount of committed memory currently used by the eden space.                   | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| mempool.psoldgen.committed             | The amount of memory currently allocated to the old generation.                    | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| mempool.psoldgen.max                   | The maximum amount of memory that could be allocated to the oldgeneration.         | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| mempool.psoldgen.used                  | The amount of committed memory currently used by the old generaion.                | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| mempool.pspermgen.committed            | The amount of memory currently allocated to the permanent generation.              | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| mempool.pspermgen.max                  | The maximum amount of memory that could be allocated to the permanent generation.  | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| mempool.pspermgen.used                 | The amount of committed memory currently used by the permanent generation.         | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| mempool.pssurvivorspace.committed      | The amount of memory currently allocated to the survivor space.                    | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| mempool.pssurvivorspace.max            | The maximum amount of memory that could be allocated to the survivor space.        | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| mempool.pssurvivorspace.used           | The amount of committed memory currently used by the survivor space.               | average   | bytes        | 0   | none   | none                       | yes  | no   | no   |
| system.LoadedClasses                   | The number of classes loaded by the JVM.                                           | average   | count        | 0   | none   | none                       | yes  | yes  | no   |
| system.threads                         | The number of currently running threads.                                           | average   | count        | 0   | none   | none                       | yes  | yes  | no   |
| system.UnloadedClasses                 | The number of classes unloaded by the JVM.                                         | average   | count        | 0   | none   | none                       | yes  | no   | no   |
