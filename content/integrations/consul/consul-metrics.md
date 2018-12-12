---
title: "Metrics"
date: 2018-12-11
draft: false
tags: ["consul", "integrations", ]
author: Lawrence Lane
---
| Fully Qualified Name (FQN)                             | Statistic | Units                                   | BASE | CORR  | Type    | Computed |
|--------------------------------------------------------|-----------|-----------------------------------------|------|-------|---------|----------|
| consul.raft.commitTime.avg                             | max       |                                         | TRUE | TRUE  | counter | yes      |
| consul.raft.commitTime.max                             | max       |                                         | TRUE | TRUE  | counter | yes      |
| consul.proxy.web.inbound.rx_bytes                      | avg       | bytes                                   | TRUE | FALSE | gauge   | no       |
| consul.health.service.not-found.[service]              | avg       | queries                                 | TRUE | FALSE | gauge   | no       |
| consul.health.service.query-tags.[service].[tags]      | avg       | queries                                 | TRUE | FALSE | gauge   | no       |
| consul.health.service.query-tag.[service].[tag]        | avg       | queries                                 | TRUE | FALSE | gauge   | no       |
| consul.health.service.query.[service]                  | avg       | queries                                 | TRUE | FALSE | gauge   | no       |
| consul.catalog.service.not-found.[service]             | avg       | queries                                 | TRUE | FALSE | gauge   | no       |
| consul.catalog.service.query-tags.[service].[tags]     | avg       | queries                                 | TRUE | FALSE | gauge   | no       |
| consul.catalog.service.query-tag.[service].[tag]       | avg       | queries                                 | TRUE | FALSE | gauge   | no       |
| consul.catalog.service.query.[service]                 | avg       | queries                                 | TRUE | FALSE | gauge   | no       |
| consul.memberlist.pushPullNode                         | avg       | nodes / Interval                        | TRUE | FALSE | gauge   | no       |
| consul.memberlist.probeNode                            | avg       | nodes / Interval                        | TRUE | FALSE | gauge   | no       |
| consul.memberlist.msg_suspect                          | avg       | nodes / Interval                        | TRUE | FALSE | gauge   | no       |
| consul.memberlist.msg_dead                             | avg       | nodes / Interval                        | TRUE | FALSE | gauge   | no       |
| consul.memberlist.msg_alive                            | avg       | nodes / Interval                        | TRUE | FALSE | gauge   | no       |
| consul.memberlist.gossip                               | avg       | messages / Interval                     | TRUE | FALSE | gauge   | no       |
| consul.memberlist.tcp.sent                             | avg       | bytes sent / interval                   | TRUE | FALSE | gauge   | no       |
| consul.memberlist.tcp.connect                          | avg       | push/pull initiated / interval          | TRUE | FALSE | gauge   | no       |
| consul.memberlist.udp.sent/received                    | avg       | bytes sent or bytes received / interval | TRUE | FALSE | gauge   | no       |
| consul.memberlist.tcp.accept                           | avg       | connections accepted / interval         | TRUE | FALSE | gauge   | no       |
| onsul.memberlist.msg.suspect                           | avg       | suspect messages received / interval    | TRUE | FALSE | gauge   | no       |
| consul.memberlist.msg.dead                             | avg       | messages / interval                     | TRUE | FALSE | gauge   | no       |
| consul.memberlist.degraded.timeout                     | avg       | occurrence / interval                   | TRUE | FALSE | gauge   | no       |
| consul.memberlist.degraded.probe                       | avg       | probes / interval                       | TRUE | FALSE | gauge   | no       |
| consul.rpc.cross-dc                                    | avg       | queries                                 | TRUE | FALSE | gauge   | no       |
| consul.rpc.query                                       | avg       | queries                                 | TRUE | FALSE | gauge   | no       |
| consul.rpc.request                                     | avg       | requests                                | TRUE | FALSE | gauge   | no       |
| consul.rpc.request_error                               | avg       | errors                                  | TRUE | FALSE | gauge   | no       |
| consul.rpc.accept_conn                                 | avg       | connections                             | TRUE | FALSE | gauge   | no       |
| consul.dns.stale_queries                               | avg       | queries                                 | TRUE | FALSE | gauge   | no       |
| consul.acl.replication_hit                             | avg       | hits                                    | TRUE | FALSE | gauge   | no       |
| consul.acl.cache_miss                                  | avg       | misses                                  | TRUE | FALSE | gauge   | no       |
| consul.acl.cache_hit                                   | avg       | hits                                    | TRUE | FALSE | gauge   | no       |
| consul.client.rpc.error.catalog_node_services.[node]   | avg       | errors                                  | TRUE | FALSE | gauge   | no       |
| consul.client.api.success.catalog_node_services.[node] | avg       | requests                                | TRUE | FALSE | gauge   | no       |
| consul.client.api.catalog_node_services.[node]         | avg       | requests                                | TRUE | FALSE | gauge   | no       |
| consul.client.rpc.error.catalog_service_nodes.[node]   | avg       | errors                                  | TRUE | FALSE | gauge   | no       |
| consul.client.api.success.catalog_service_nodes.[node] | avg       | requests                                | TRUE | FALSE | gauge   | no       |
| consul.client.api.catalog_service_nodes.[node]         | avg       | requests                                | TRUE | FALSE | gauge   | no       |
| consul.client.rpc.error.catalog_services.[node]        | avg       | errors                                  | TRUE | FALSE | gauge   | no       |
| consul.client.api.success.catalog_services.[node]      | avg       | requests                                | TRUE | FALSE | gauge   | no       |
| consul.client.api.catalog_services.[node]              | avg       | requests                                | TRUE | FALSE | gauge   | no       |
| consul.client.rpc.error.catalog_nodes.[node]           | avg       | errors                                  | TRUE | FALSE | gauge   | no       |
| consul.client.api.success.catalog_nodes.[node]         | avg       | requests                                | TRUE | FALSE | gauge   | no       |
| consul.client.api.catalog_nodes.[node]                 | avg       | requests                                | TRUE | FALSE | gauge   | no       |
| consul.client.rpc.error.catalog_datacenters.[node]     | avg       | errors                                  | TRUE | FALSE | gauge   | no       |
| consul.client.api.success.catalog_datacenters.[node]   | avg       | requests                                | TRUE | FALSE | gauge   | no       |
| consul.client.api.catalog_datacenters.[node]           | avg       | requests                                | TRUE | FALSE | gauge   | no       |
| consul.client.rpc.error.catalog_deregister.[node]      | avg       | errors                                  | TRUE | FALSE | gauge   | no       |
| consul.client.api.success.catalog_deregister.[node]    | avg       | requests                                | TRUE | FALSE | gauge   | no       |
| consul.client.api.catalog_deregister.[node]            | avg       | requests                                | TRUE | FALSE | gauge   | no       |
| consul.client.rpc.error.catalog_register.[node]        | avg       | errors                                  | TRUE | FALSE | gauge   | no       |
| consul.client.api.success.catalog_register.[node]      | avg       | requests                                | TRUE | FALSE | gauge   | no       |
| consul.client.api.catalog_register.[node]              | avg       | requests                                | TRUE | FALSE | gauge   | no       |
| consul.client.rpc.failed                               | avg       | requests                                | TRUE | FALSE | gauge   | no       |
| consul.client.rpc.exceeded                             | avg       | rejected requests                       | TRUE | FALSE | gauge   | no       |
| consul.client.rpc                                      | avg       | requests                                | TRUE | FALSE | gauge   | no       |
| consul.acl.blocked.(check|node|service).registration   | avg       | requests                                | TRUE | FALSE | gauge   | no       |
| consul.acl.blocked.service.registration                | avg       | requests                                | TRUE | FALSE | gauge   | no       |
| consul.serf.events                                     | max       | events / interval                       | TRUE | TRUE  | counter | no       |
| consul.serf.member.flap                                | max       | flaps / interval                        | TRUE | TRUE  | counter | no       |
| consul.serf.snapshot.compact                           | max       | ms                                      | TRUE | TRUE  | timer   | no       |
| consul.serf.snapshot.appendLine                        | max       | ms                                      | TRUE | TRUE  | timer   | no       |
| consul.rpc.raft_handoff                                | avg       | connections                             | TRUE | FALSE | gauge   | no       |
| consul.raft.leader.lastContact                         | max       | ms                                      | TRUE | TRUE  | timer   | no       |
| consul.raft.replication.appendEntries.logs             | max       | logs appended/ interval                 | TRUE | TRUE  | counter | no       |
| consul.raft.replication.appendEntries.rpc              | max       | ms                                      | TRUE | TRUE  | timer   | no       |
| consul.raft.rpc.installSnapshot                        | max       | ms                                      | TRUE | TRUE  | timer   | no       |
| consul.raft.rpc.requestVote                            | max       | ms                                      | TRUE | TRUE  | timer   | no       |
| consul.raft.rpc.appendEntries.processLogs              | max       | ms                                      | TRUE | TRUE  | timer   | no       |
| consul.raft.rpc.appendEntries.storeLogs                | max       | ms                                      | TRUE | TRUE  | timer   | no       |
| consul.raft.rpc.appendEntries                          | max       | ms                                      | TRUE | TRUE  | timer   | no       |
| consul.raft.rpc.processHeartBeat                       | max       | ms                                      | TRUE | TRUE  | timer   | no       |
| consul.raft.restoreUserSnapshot                        | max       | ms                                      | TRUE | TRUE  | timer   | no       |
| consul.raft.transistion.heartbeat_timeout              | max       | timeouts / interval                     | TRUE | TRUE  | counter | no       |
| consul.raft.state.follower                             | max       | follower state entered / interval       | TRUE | TRUE  | counter | no       |
| consul.raft.replication.appendEntries                  | max       | ms                                      | TRUE | TRUE  | timer   | no       |
| consul.raft.leader.dispatchLog                         | max       | ms                                      | TRUE | TRUE  | timer   | no       |
| consul.raft.commitTime                                 | max       | ms                                      | TRUE | TRUE  | timer   | no       |
| consul.raft.restore                                    | max       | operation invoked / interval            | TRUE | TRUE  | counter | no       |
| consul.raft.verify_leader                              | max       | checks / interval                       | TRUE | TRUE  | counter | no       |
| consul.raft.barrier                                    | max       | blocks / interval                       | TRUE | TRUE  | counter | no       |
| consul.raft.apply                                      | max       | Raft Transactions / Interval            | TRUE | TRUE  | counter | no       |
| consul.raft.state.candidate                            | max       | Election Attempts / Interval            | TRUE | TRUE  | counter | no       |
| consul.raft.state.leader                               | max       | Leadership Transitions / Interval       | TRUE | TRUE  | counter | no       |
| consul.raft.replication.heartbeat                      | max       | MS                                      | TRUE | TRUE  | Timer   | no       |
| consul.raft.snapshot.takeSnapshot                      | max       | MS                                      | TRUE | TRUE  | Timer   | no       |
| consul.raft.snapshot.persist                           | max       | MS                                      | TRUE | TRUE  | Timer   | no       |
| consul.raft.snapshot.create                            | max       | MS                                      | TRUE | TRUE  | Timer   | no       |
| consul.raft.fsm.restore                                | max       | MS                                      | TRUE | TRUE  | Timer   | no       |
| consul.raft.fsm.apply                                  | max       | Commit Logs / Interval                  | TRUE | TRUE  | counter | no       |
| consul.raft.fsm.snapshot                               | max       | MS                                      | TRUE | TRUE  | Timer   | no       |
| consul.runtime.heap_objects                            | max       | number of objects                       | TRUE | TRUE  | gauge   | no       |
| consul.runtime.alloc_bytes                             | max       | bytes                                   | TRUE | TRUE  | gauge   | no       |
| consul.runtime.num_goroutines                          | max       | number of goroutines                    | TRUE | TRUE  | gauge   | no       |
