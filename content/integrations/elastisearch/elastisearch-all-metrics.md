---
title: "All Elastisearch Metrics"
#date: 2018-12-11
draft: false
tags: ["elastisearch", "integrations", "metrics", "cluster", "disk", "threadpool", "indices" ]
author: Lawrence Lane
---
## Collected
For the table below, all metrics that begin with `elasticsearch.indices.*` are duplicated for each index being monitored, with the * replaced by the index name (your indices will vary based on your implementation). All metrics that start with `elasticsearch.thread_pool.*` are duplicated for each thread pool, with the * replaced by the thread pool name. The various thread pools are:

- bench
- bulk
- fetch_shard_started
- fetch_shard_store
- flush
- generic
- get
- index
- listener
- management
- merge
- optimize
- percolate
- refresh
- search
- snapshot
- suggest
- warmer

| Fully Qualified Name (FQN)                                     | Statistic | Units   | Min | Max  | Sparse Data Strategy(SDS) | BASE | CORR | UTIL |
|----------------------------------------------------------------|-----------|---------|-----|------|---------------------------|------|------|------|
| elasticsearch.cache.filter.evictions                           | max       | count   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.cache.filter.size                                | average   | bytes   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.cluster_health.nodes.data                        | average   | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.cluster_health.nodes.total                       | average   | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.cluster_health.shards.active                     | average   | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.cluster_health.shards.active_primary             | average   | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.cluster_health.shards.initializing               | average   | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.cluster_health.shards.relocating                 | average   | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.cluster_health.status                            | average   | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.cluster_health.unassigned                        | average   | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.disk.reads.count                                 | max       | count   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.disk.reads.size                                  | max       | bytes   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.disk.writes.count                                | max       | count   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.disk.writes.size                                 | max       | bytes   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.fielddata.evictions                              | average   | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.fielddata.size                                   | average   | bytes   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.http.current                                     | average   | count   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.datastore.size                         | max       | bytes   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.docs.count                             | max       | count   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.docs.deleted                           | max       | count   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.flush.total                            | max       | count   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.flush.total_time_in_milliseconds       | max       | ms      | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.get.exists_time_in_milliseconds        | max       | ms      | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.get.exists_total                       | max       | count   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.get.missing_time_in_milliseconds       | max       | ms      | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.get.missing_total                      | max       | count   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.get.time_in_milliseconds               | max       | ms      | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.get.total                              | max       | count   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.indexing.delete_time_in_milliseconds   | max       | ms      | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.indexing.delete_total                  | max       | count   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.indexing.index_time_in_milliseconds    | max       | ms      | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.indexing.index_total                   | max       | count   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.indexing.noop_update_total             | max       | count   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.indexing.throttle_time_in_milliseconds | max       | ms      | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.merges.total                           | max       | count   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.merges.total_time_in_milliseconds      | max       | ms      | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.percolate.time_in_milliseconds         | max       | ms      | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.percolate.total                        | max       | count   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.recover.throttle_time_in_milliseconds  | max       | ms      | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.refresh.total                          | max       | count   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.refresh.total_time_in_milliseconds     | max       | ms      | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.search.fetch_time_in_milliseconds      | max       | ms      | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.search.fetch_total                     | max       | count   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.search.query_time_in_milliseconds      | max       | ms      | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.search.query_total                     | max       | count   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.store.throttle_time_in_milliseconds    | max       | ms      | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.suggest.time_in_milliseconds           | max       | ms      | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.suggest.total                          | max       | count   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.warmer.total                           | max       | count   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.warmer.total_time_in_milliseconds      | max       | ms      | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.datastore.size                         | max       | bytes   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.docs.count                             | max       | count   | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.indices.*.docs.deleted                           | max       | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.jvm.gc.collection.count                          | max       | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.jvm.gc.collection.old.count                      | max       | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.jvm.gc.collection.old.time                       | max       | ms      | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.jvm.gc.collection.young.count                    | max       | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.jvm.gc.collection.young.time                     | max       | ms      | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.jvm.mem.heap_committed                           | average   | bytes   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.jvm.mem.heap_used                                | average   | bytes   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.jvm.mem.heap_used_percent                        | average   | percent | 0   | none | none                      | yes  | yes  | no   |
| elasticsearch.jvm.mem.non_heap_committed                       | average   | bytes   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.jvm.mem.non_heap_used                            | average   | bytes   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.jvm.mem.pools.old.max                            | average   | bytes   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.jvm.mem.pools.old.used                           | average   | bytes   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.jvm.mem.pools.survivor.max                       | average   | bytes   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.jvm.mem.pools.survivor.used                      | average   | bytes   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.jvm.mem.young.max                                | average   | bytes   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.jvm.mem.young.used                               | average   | bytes   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.jvm.threads.count                                | average   | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.network.tcp.active_opens                         | max       | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.network.tcp.attempt_fails                        | max       | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.network.tcp.curr_estab                           | max       | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.network.tcp.estab_resets                         | max       | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.network.tcp.in_errs                              | max       | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.network.tcp.in_segs                              | max       | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.network.tcp.out_rate                             | max       | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.network.tcp.out_segs                             | max       | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.network.tcp.passive_opens                        | max       | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.network.tcp.retrans_segs                         | max       | count   | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.process.cpu.percent                              | average   | percent | 0   | none | none                      | yes  | no   | no   |
| elasticsearch.process.mem.resident                             | average   | bytes   | 0   | 100  | none                      | yes  | no   | no   |
| elasticsearch.process.share                                    | average   | bytes   | 0   | 100  | none                      | yes  | no   | no   |
| elasticsearch.process.virtual                                  | average   | bytes   | 0   | 100  | none                      | yes  | no   | no   |
| elasticsearch.thread_pool.*.active                             | average   | count   | 0   | 100  | none                      | yes  | no   | no   |
| elasticsearch.thread_pool.*.completed                          | max       | count   | 0   | 100  | none                      | yes  | no   | no   |
| elasticsearch.thread_pool.*.largest                            | average   | count   | 0   | 100  | none                      | yes  | no   | no   |
| elasticsearch.thread_pool.*.queue                              | average   | count   | 0   | 100  | none                      | yes  | no   | no   |
| elasticsearch.thread_pool.*.rejected                           | max       | count   | 0   | 100  | none                      | yes  | no   | no   |
| elasticsearch.thread_pool.*.threads                            | average   | count   | 0   | 100  | none                      | yes  | no   | no   |
| elasticsearch.transport.rx.count                               | max       | count   | 0   | 100  | none                      | yes  | no   | no   |
| elasticsearch.transport.rx.size                                | max       | count   | 0   | 100  | none                      | yes  | no   | no   |
| elasticsearch.transport.tx.count                               | max       | count   | 0   | 100  | none                      | yes  | no   | no   |
| elasticsearch.transport.tx.size                                | max       | count   | 0   | 100  | none                      | yes  | no   | no   |
