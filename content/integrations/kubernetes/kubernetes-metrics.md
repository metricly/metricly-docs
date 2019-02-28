---
title: "Kubernetes Metrics"
#date: 2018-12-11
draft: false
tags: ["#metrics", "#integrations", "#kubernetes" ]
author: Lawrence Lane
---
| Metric FQN                                               | Kubernetes Types                                            | Baseline | Correlated | Statistic                   |
|----------------------------------------------------------|-------------------------------------------------------------|----------|------------|-----------------------------|
| cpu.limit                                                | Cluster, Node, Namespace, Pod, Pod Container, Sys Container | No       | No         | Average                     |
| cpu.node.allocatable                                     | Node                                                        | No       | No         | Average                     |
| cpu.node.utilization                                     | Node                                                        | Yes      | Yes        | Average                     |
| cpu.node_capacity                                        | Node                                                        | No       | No         | Average                     |
| cpu.node_reservation                                     | Node                                                        | No       | No         | Average                     |
| cpu.request                                              | Cluster, Node, Namespace, Pod, Pod Container, Sys Container | No       | No         | Average                     |
| cpu.usage                                                | Cluster, Node, Namespace, Pod, Pod Container, Sys Container | No       | No         | Average                     |
| cpu.usage_rate                                           | Cluster, Node, Namespace, Pod, Pod Container, Sys Container | Yes      | No         | Average                     |
| disk.io.write_bytes:11:0                                 | Node                                                        | Yes      | No         | Average                     |
| disk.io_read_bytes:/dev/dm-0                             | Cluster, Namespace, Pod, Pod Container, Sys Container       | No       | No         | Average                     |
| disk.io_read_bytes:/dev/dm-1                             | Cluster, Namespace, Pod, Pod Container, Sys Container       | No       | No         | Average                     |
| disk.io_read_bytes:/dev/sda                              | Cluster, Namespace, Pod, Pod Container, Sys Container       | No       | No         | Average                     |
| disk.io_read_bytes:11:0                                  | Cluster, Node, Sys Container                                | Yes      | No         | Average                     |
| disk.io_read_bytes_rate:/dev/dm-0                        | Cluster, Namespace, Pod, Pod Container, Sys Container       | No       | No         | Average                     |
| disk.io_read_bytes_rate:/dev/dm-1                        | Cluster, Namespace, Pod, Pod Container, Sys Container       | No       | No         | Average                     |
| disk.io_read_bytes_rate:/dev/sda                         | Cluster, Namespace, Pod, Pod Container, Sys Container       | No       | No         | Average                     |
| disk.io_read_bytes_rate:11:0                             | Cluster, Node, Namespace, Sys Container                     | No       | No         | Average                     |
| disk.io_write_bytes:/dev/dm-0                            | Cluster, Node, Namespace, Sys Container                     | No       | No         | Average                     |
| disk.io_write_bytes:/dev/dm-1                            | Cluster, Namespace, Pod, Sys Container                      | No       | No         | Average                     |
| disk.io_write_bytes:/dev/sda                             | Cluster, Namespace, Pod, Sys Container                      | No       | No         | Average                     |
| disk.io_write_bytes:11:0                                 | Cluster, Namespace, Sys Container                           | Yes      | No         | Average                     |
| disk.io_write_bytes_rate:/dev/dm-0                       | Cluster, Namespace, Sys Container                           | No       | No         | Average                     |
| disk.io_write_bytes_rate:/dev/dm-1                       | Cluster, Namespace, Pod, Sys Container                      | No       | No         | Average                     |
| disk.io_write_bytes_rate:/dev/sda                        | Cluster, Namespace, Pod, Sys Container                      | No       | No         | Average                     |
| disk.io_write_bytes_rate:11:-                            | Node                                                        | No       | No         | Average                     |
| disk.io_write_bytes_rate:11:0                            | Cluster, Namespace, Sys Container                           | Yes      | No         | Average                     |
| filesystem.available:/dev/mapper/centos-root             | Node, Pod                                                   | No       | No         | Average                     |
| filesystem.available:/dev/mapper/centos-var_lib_docker   | Node, Pod, Pod Container                                    | No       | No         | Average                     |
| filesystem.available:/dev/sda1                           | Node                                                        | No       | No         | Average                     |
| filesystem.available:tmpfs                               | Node                                                        | No       | No         | Average                     |
| filesystem.inodes:/dev/mapper/centos-root                | Node                                                        | No       | No         | Average                     |
| filesystem.inodes:/dev/mapper/centos-var_lib_docker      | Node                                                        | No       | No         | Average                     |
| filesystem.inodes:/dev/sda1                              | Node                                                        | No       | No         | Average                     |
| filesystem.inodes:tmpfs                                  | Node                                                        | No       | No         | Average                     |
| filesystem.inodes_free:/dev/mapper/centos-root           | Node                                                        | No       | No         | Average                     |
| filesystem.inodes_free:/dev/mapper/centos-var_lib_docker | Node                                                        | No       | No         | Average                     |
| filesystem.inodes_free:/dev/sda1                         | Node                                                        | No       | No         | Average                     |
| filesystem.inodes_free:tmpfs                             | Node                                                        | No       | No         | Average                     |
| filesystem.limit:/dev/mapper/centos-root                 | Node                                                        | No       | No         | Average                     |
| filesystem.limit:/dev/mapper/centos-var_lib_docker       | Node, Pod, Pod Container                                    | No       | No         | Average                     |
| filesystem.limit:/dev/sda1                               | Node                                                        | No       | No         | Average                     |
| filesystem.limit:tmpfs                                   | Node                                                        | No       | No         | Average                     |
| filesystem.usage:/dev/mapper/centos-root                 | Node, Pod                                                   | No       | No         | Average                     |
| filesystem.usage:/dev/mapper/centos-var_lib_docker       | Node, Pod, Pod Container                                    | No       | No         | Average                     |
| filesystem.usage:/dev/sda1                               | Node                                                        | No       | No         | Average                     |
| filesystem.usage:tmpfs                                   | Node                                                        | No       | No         | Average                     |
| k8s.cluster.cpu.useage.percent                           | Cluster                                                     |          |            |                             |
| k8s.namespace.cpu.usage.percent                          | Namespace, Pod, Pod Container, Sys Container                |          |            |                             |
| k8s.namespace.memory.usage.percent                       | Namespace, Pod, Pod Container, Sys Container                | Yes      | Yes        | Percent (Expression Result) |
| memory.cache                                             | Namespace, Pod, Pod Container, Sys Container                | No       | No         | Average                     |
| memory.limit                                             | Cluster, Namespace, Pod, Pod Container                      | No       | No         | Average                     |
| memory.major_page_faults                                 | Cluster, Namespace, Pod, Pod Container, Sys Container       | No       | No         | Average                     |
| memory.major_page_faults_rate                            | Cluster, Namespace, Pod, Pod Container, Sys Container       | Yes      | No         | Average                     |
| memory.node_allocatable                                  | Cluster, Namespace                                          | No       | No         | Average                     |
| memory.node_capacity                                     | Cluster, Namespace                                          | No       | No         | Average                     |
| memory.node_reservation                                  | Cluster, Namespace                                          | No       | No         | Average                     |
| memory.node_utilization                                  | Cluster, Namespace                                          | Yes      | Yes        | Average                     |
| memory.page_faults                                       | Cluster, Namespace, Pod, Pod Container, Sys Container       | No       | No         | Average                     |
| memory.page_faults_rate                                  | Cluster, Namespace, Pod, Pod Container, Sys Container       | Yes      | No         | Average                     |
| memory.request                                           | Cluster, Namespace, Pod, Pod Container, Sys Container       | Yes      | Yes        | Average                     |
| memory.rss                                               | Cluster, Namespace, Pod, Pod Container, Sys Container       | No       | No         | Average                     |
| memory.usage                                             | Cluster, Namespace, Pod, Pod Container, Sys Container       | Yes      | Yes        | Average                     |
| memory.working_set                                       | Cluster, Namespace, Pod, Pod Container, Sys Container       | Yes      | No         | Average                     |
| network.rx                                               | Node, Pod, Pod Container                                    | No       | No         | Average                     |
| network.rx_errors                                        | Node, Pod, Pod Container                                    | No       | No         | Average                     |
| network.rx_errors_rate                                   | Node, Pod, Pod Container                                    | Yes      | No         | Average                     |
| network.rx_rate                                          | Node, Pod, Pod Container                                    | Yes      | Yes        | Average                     |
| network.tx                                               | Node, Pod, Pod Container                                    | No       | No         | Average                     |
| network.tx_errors                                        | Node, Pod, Pod Container                                    | No       | No         | Average                     |
| network.tx_errors_rate                                   | Node, Pod, Pod Container                                    | Yes      | No         | Average                     |
| network.tx_rate                                          | Node, Pod, Pod Container                                    | Yes      | Yes        | Average                     |
| restart_count                                            | Node, Pod, Pod Container                                    |          |            |                             |
| uptime                                                   | Cluster, Node, Namespace, Pod, Pod Container, Sys Container | No       | No         | Average                     |
