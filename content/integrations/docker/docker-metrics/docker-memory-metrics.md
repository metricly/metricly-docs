---
title: "Docker Memory Metrics"
#date: 2018-12-11
draft: false
tags: ["#docker", "#integrations", "#metrics", "#memory"]
author: Lawrence Lane
---

## Collected

| Fully Qualified Name(FQN) | Type | Units | Statistic* | BASE | CORR | Description |
|---------------------------------------|---------|-------|------------|------|------|----------------------------------------------------------------------------------------------------------------------------|
| memory.failcnt | GAUGE | count | average | no | no | A count of the number of times that the container requested memory and failed to obtain it. This value should always be 0. |
| memory.limit | GAUGE | bytes | average | no | no | The total amount of memory available to the container. |
| memory.max_usage | GAUGE | bytes | average | no | no | The maxiumum amount of memory the container has ever used. |
| memory.stats.active_anon | GAUGE | bytes | average | no | no | The amount of anonymous memory that has been identified as active and by the kernel. “Anonymous” memory is the memory that is not linked to disk pages. |
| memory.stats.active_file | GAUGE | bytes | average | no | no | Part of cache memory. Cache = active_file + inactive_file + tmpfs. |
| memory.stats.cache | GAUGE | bytes | average | no | no | The amount of memory used by the processes of this control group that can be associated with a block on a block device. Also accounts for memory used by tmpfs. |
| memory.stats.hierarchical_memory_lmit | GAUGE | bytes | average | no | no | The memory limit in place by the hierarchy cgroup.|
| memory.stats.hierarchical_memsw_limit | GAUGE | bytes | average | no | no | The memory+swap limit in place by the hierarchy cgroup.|
| memory.stats.inactive_anon | GAUGE | bytes | average | no | no | The amount of anonymous memory that has been identified as inactive and by the kernel. “Anonymous” memory is the memory that is not linked to disk pages.|
| memory,stats.inactive_file | GAUGE | bytes | average | no | no |Part of cache memory. Cache = active_file + inactive_file + tmpfs.|
| memory.stats.mapped_file | GAUGE | bytes | average | no | no |Indicates the amount of memory mapped by the processes in the control group. It doesn’t give you information about how much memory is used; it rather tells you how it is used.|
| memory.stats.pgpgin | COUNTER | bytes | count | yes | no | Total number of charging events. |
| memory.stats.pgpgout | COUNTER | bytes | count | yes | no | Total number of uncharging events. |
| memory.stats.rss | GAUGE | bytes | average | yes | no | The amount of memory that doesn’t correspond to anything on disk: stacks, heaps, and anonymous memory maps. |
| memory.stats.swap | GAUGE | bytes | average | no | no | Bytes of swap memory used by container. |
| memory.stats.total_active_anon | GAUGE | bytes | average | yes | no | Total amount of memory that has been identified as active by the kernel. Anonymous memory is memory that is not linked to disk pages. |
| memory.stats.total_active_file | GAUGE | bytes | average | no | no | Total amount of active file cache memory. Cache memory = active_file + inactive_file + tmpfs. |
| memory.stats_total_cache | GAUGE | bytes | average | no | no | Total amount of memory used by the processes of this control group that can be associated with a block on a block device. Also accounts for memory used by tmpfs. |
| memory.stats.total_inactive_anon | GAUGE | bytes | average | no | no | The total amount of memory that has been identified as inactive by the kernel. Anonymous memory is memory that is not linked to disk pages. |
| memory.stats.total_inactive_file | GAUGE | bytes | average | no | no | The total amount of inactive file cache memory. Cache memory = active_file + inactive_file + tmpfs. |
| memory.stats.total_mapped_file | GAUGE | bytes | average | no | no | The total amount of memory mapped by the processes in the control group.|
| memory.stats.total_pgpgin | COUNTER | bytes | count | yes | no | The total number of charging events. |
| memory.stats.total_pgpgout | COUNTER | bytes | count | yes | no | The total number of uncharging events. |
| memory.stats.total_rss | GAUGE | bytes | average | yes | no | The total amount of memory due to anonymous transparent hugepages.|
| memory.stats.total_swap | GAUGE | bytes | average | no | no | The total amount of swap memory available to this container. |
| memory.stats.total_unevictable | GAUGE | bytes | average | no | no | The total amount of memory that can not be reclaimed. |
| memory.stats.unevictable | GAUGE | bytes | average | no | no | The amount of memory that cannot be reclaimed.|
| memory.usage | GAUGE | bytes | average | yes | no | The amount of memory currently being used by the container. |
