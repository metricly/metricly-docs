---
title: "Linux Agent Metrics"
#date: 2018-11-30T16:08:13-05:00
draft: false
categories: ["integration", "admin guide", "getting started"]
tags: ["#agents", "#linux", "#metrics"]
author: Lawrence Lane
weight: 9
---

## Collected

### CPU

| Fully Qualified Name (FQN) | Description | Statistic | Units | Min | Max | Sparse Data Strategy (SDS) | BASE | CORR | UTIL |
|----------------------------|---------------------------------------------------------------------------------------------------|-----------|---------|-----|------|----------------------------|------|------|------|
| cpu.total.guest | Percentage of CPU spent running virtual CPUs for guest operatingsystems. | average | percent | 0 | none | none | yes | no | no |
| cpu.total.guest_nice | Percentage of CPU spent running low-priority virtual CPUs for guestoperating systems. | average | percent | 0 | none | none | yes | no | no |
| cpu.total.idle | Percentage of CPU not doing any work. | average | percent | 0 | none | none | yes | no | no |
| cpu.total.iowait | Percentage of CPU time spent waiting for I/O to complete. | average | percent | 0 | none | none | yes | no | no |
| cpu.total.irq | Percentage of CPU time spent processing hardware interrupts. | average | percent | 0 | none | none | yes | no | no |
| cpu.total.nice | Percentage of CPU spent running user processes at low priority. | average | percent | 0 | none | none | yes | no | no |
| cpu.total.softirq | Percentage of CPU time spent processing software interrupts. | average | percent | 0 | none | none | yes | no | no |
| cpu.total.steal | Percentage of CPU time spent in other operating systems when running ina virtualized environment. | average | percent | 0 | none | none | yes | no | no |
| cpu.total.system | Percentage of CPU spent running system processes. | average | percent | 0 | none | none | yes | no | no |
| cpu.total.user | Percentage of CPU spent running user processes. | average | percent | 0 | none | none | yes | no | no |


### Diskspace

| Fully Qualified Name (FQN) | Description | Statistic | Units | Min | Max | Sparse Data Strategy (SDS) | BASE | CORR | UTIL |
|----------------------------------------|-------------------------------------------------|-----------|---------|-----|-----|----------------------------|------|------|------|
| diskspace.<disk>.byte_percentfree | Percentage of bytes free. | average | percent | 0 | 100 | none | yes | no | no |
| diskspace.<disk>.byte_percentavailable | Percentage of bytes available to non-superuser. | average | percent | 0 | 100 | none | yes | no | no |

###  Disk Usage

| Fully Qualified Name (FQN) | Description | Statistic | Units | Min | Max | Sparse Data Strategy (SDS) | BASE | CORR | UTIL |
|------------------------------------|-----------------------------------------------------------------------------------|-----------|---------|-----|------|----------------------------|------|------|------|
| iostat.<disk>.average_queue_length | The average length of the disk queue for the disk. | average |  | 0 | none | none | yes | no | no |
| iostat.<disk>.await | Average completion in milliseconds. | average | ms | 0 | none | none | yes | no | no |
| iostat.<disk>.io | The total number of completed IO operations, including both reads andwrites. | sum |  | 0 | none | none | yes | no | no |
| iostat.<disk>.iops | Operations per second. | average | iops | 0 | none | none | yes | no | no |
| iostat.<disk>.read_await | Average read time completion in milliseconds. | average | ms | 0 | none | none | yes | no | no |
| iostat.<disk>.reads | Total number of read operations. | sum |  | 0 | none | none | yes | no | no |
| iostat.<disk>.util_percentage | Percentage of CPU time spent spent servicing all IO requests, both readand write. | average | percent | 0 | 100 | none | yes | no | no |
| iostat.<disk>.write_await | Average write time completion in milliseconds. | average | ms | 0 | none | none | yes | no | no |
| iostat.<disk>.writes | Total number of write operations. | sum |  | 0 | none | none | yes | no | no |

### Load Average

| Fully Qualified Name (FQN) | Description | Statistic | Units | Min | Max | Sparse Data Strategy (SDS) | BASE | CORR | UTIL |
|----------------------------|-------------------------------------------------------------|-----------|-------|-----|------|----------------------------|------|------|------|
| loadavg.01 | The is the average run queue size over the past minute. | average |  | 0 | none | none | yes | no | no |
| loadavg.05 | The is the average run queue size over the past 5 minutes. | average |  | 0 | none | none | yes | no | no |
| loadavg.15 | The is the average run queue size over the past 15 minutes. | average |  | 0 | none | none | yes | no | no |
| loadavg.processes_running | The total number of processes in a running state. | average |  | 0 | none | none | yes | no | no |
| loadavg.processes_total | The total number of processes. | average |  | 0 | none | none | yes | no | no |

### Memory

| Fully Qualified Name (FQN) | Description | Statistic | Units | Min | Max | Sparse Data Strategy (SDS) | BASE | CORR | UTIL |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|-------|-----|------|----------------------------|------|------|------|
| memory.Active | Memory currently in use. | average | bytes | 0 | none | none | yes | no | no |
| memory.Buffers | Cache for file buffers. | average | bytes | 0 | none | none | yes | no | no |
| memory.Cached | Cache for other things, such as disk cache. | average | bytes | 0 | none | none | yes | no | no |
| memory.Dirty | The total amount of memory waiting to be written back to the disk. | average | bytes | 0 | none | none | yes | no | no |
| memory.Inactive | Memory marked as not in use. | average | bytes | 0 | none | none | yes | no | no |
| memory.MemAvailable | Memory not being used for anything. Note that the amount of availablememory is computed by adding MemFree, Buffers, and Cache. This isbecause, while the memory used by Buffers and Cache is not “free”, itcan be freed and used by processes that need it, so it is thereforeconsidered “available”. | average | bytes | 0 | none | none | yes | no | no |
| memory.MemFree | The amount of physical memory left unused by the system. | average | bytes | 0 | none | none | yes | no | no |
| memory.MemTotal | The total amount of physical memory. | average | bytes | 0 | none | none | yes | no | no |
| memory.Shmem | Shared memory that can be simultaneously accessed by multiple processes. | average | bytes | 0 | none | none | yes | no | no |
| memory.SwapCached | Amount of swap used as cache memory. | average | bytes | 0 | none | none | yes | no | no |
| memory.SwapFree | Amount of swap memory which is free. | average | bytes | 0 | none | none | yes | no | no |
| memory.SwapTotal | Total amount of memory allocated for swapping. | average | bytes | 0 | none | none | yes | no | no |
| memory.VmallocChunk | The total amount of allocated virtual address space. | average | bytes | 0 | none | none | yes | no | no |
| memory.VmallocTotal | The total amount of used virtual address space. | average | bytes | 0 | none | none | yes | no | no |
| memory.VmallocUsed | The largest contiguous block of available virtual address space. | average | bytes | 0 | none | none | yes | no | no |

### Network

| Fully Qualified Name (FQN) | Description | Statistic | Units | Min | Max | Sparse Data Strategy (SDS) | BASE | CORR | UTIL |
|----------------------------|--------------------------------------------------------------------|-----------|-------|-----|------|----------------------------|------|------|------|
| network.<int>.rx_byte | The total number of bytes of data received by the interface. | sum | bytes | 0 | none | none | yes | no | no |
| network.<int>.rx_errors | The total number of receive errors detected by the device driver. | sum |  | 0 | none | none | yes | no | no |
| network.<int>.rx_packets | The total number of packets of data received by the interface. | sum |  | 0 | none | none | yes | no | no |
| network.<int>.tx_byte | The total number of bytes of data transmitted by the interface. | sum | bytes | 0 | none | none | yes | no | no |
| network.<int>.tx_errors | The total number of transmit errors detected by the device driver. | sum |  | 0 | none | none | yes | no | no |
| network.<int>.tx_packets | The total number of packets of data transmitted by the interface. | sum |  | 0 | none | none | yes | no | no |

### VMStat

| Fully Qualified Name (FQN) | Description | Statistic | Units | Min | Max | Sparse Data Strategy (SDS) | BASE | CORR | UTIL |
|----------------------------|---------------------|-----------|-------|-----|------|----------------------------|------|------|------|
| vmstat.pgpgin | Number of pageins. | average |  | 0 | none | none | yes | no | no |
| vmstat.pgpgout | Number of pageouts. | average |  | 0 | none | none | yes | no | no |
| vmstat.pswpin | Number of swapins. | average |  | 0 | none | none | yes | no | no |
| vmstat.pswpout | Number of swapouts. | average |  | 0 | none | none | yes | no | no |


## Computed

### CPU

| Fully Qualified Name (FQN) | Description | Units | Min | Max | BASE | CORR | UTIL | Related Default Policies |
|-----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|-----|-----|------|------|------|--------------------------------------------------------|
| netuitive.linux.cpu.total.utilization.percent | The overall average CPU Utilization across all CPUs. This is anormalized metric.Computation:(data[‘cpu.total.idle’] != null && data[‘cpu.total.idle’].actual!= null) ? ((data.sum(‘cpu.total.*’) – data[‘cpu.total.idle’].actual) /data.sum(‘cpu.total.*’)) * 100 : data[‘cpu.cpu0.idle’] != null ?((data.sum(‘cpu[.].*’) – data.sum(‘cpu[.].*.idle’)) /data.sum(‘cpu[.].*’)) * 100 : null | percent | 0 | 100 | yes | yes | yes | Linux – CPU Threshold Exceeded, Linux – Heavy CPU Load |
| netuitive.linux.cpu.total.normalized.user | Percentage of CPU spent running user processes. This is a normalizedmetric.Computation:attribute[‘cpus’] == null ? null : data[‘cpu.total.user’] /attribute[‘cpus’].value | percent | 0 | 100 | yes | no | no |  |
| netuitive.linux.cpu.total.normalized.system | Percentage of CPU spent running system processes. This is a normalizedmetric.Computation:attribute[‘cpus’] == null ? null : data[‘cpu.total.system’] /attribute[‘cpus’].value | percent | 0 | 100 | yes | no | no |  |

### Diskspace

| Fully Qualified Name (FQN) | Description | Units | Min | Max | BASE | CORR | UTIL | Related Default Policies |
|-------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|-----|-----|------|------|------|---------------------------------------------|
| netuitive.linux.diskspace.*.byte_percentused | Percentage of disk space used.Computation:100 – data[‘diskspace.*.byte_percentfree’].actual | percent | 0 | 100 | no | no | no | Linux – Disk Utilization Threshold Exceeded |
| netuitive.linux.diskspace.avg_byte_percentused | Average disk space utilization across all disks.Computation:(data.count(‘diskspace\\..*\\..byte_percentfree’) == null) || (data.count(‘diskspace\\..*\\..byte_percentfree’) == 0) ? null : 100 – data.sum(‘diskspace\\..*\\..byte_percentfree’) / data.count(‘diskspace\\..*\\..byte_percentfree’) | percent | 0 | 100 | yes | yes | yes |  |
| netuitive.linux.diskspace.*.byte_percentused_nonsuperuser | Percentage of disk space used by non-superuser.Computation:100 – data[‘diskspace.*.byte_percentavailable’].actual | percent | 0 | 100 | no | no | no |  |
| netuitive.linux.diskspace.avg_byte_percentused_nonsuperuser | Average disk space utilization across all disks by non-superuser.Computation:(data.count(‘diskspace\\..*\\..byte_percentavailable’) == null) || (data.count(‘diskspace\\..*\\..byte_percentavailable’) == 0) ? null : 100 – data.sum(‘diskspace\\..*\\..byte_percentavailable’) / data.count(‘diskspace\\..*\\..byte_percentavailable’) | percent | 0 | 100 | yes | yes | yes |  |

### Disk Usage

| Fully Qualified Name (FQN) | Description | Units | Min | Max | BASE | CORR | UTIL | Related Default Policies |
|--------------------------------------------|------------------------------------------------------------------------------------------------|---------|-----|------|------|------|------|--------------------------|
| netuitive.linux.iostat.totalreads | Total reads across all disks.Computation:data.sum(‘iostat\\..*\\.reads) |  | 0 | none | yes | no | no |  |
| netuitive.linux.iostat.totalwrites | Total writes across all disks.Computation:data.sum(‘iostat\\..*\\.writes) |  | 0 | none | yes | no | no |  |
| netuitive.linux.iostat.max_util_percentage | Maximum disk utilization across all disks.Computation:data.max(‘iostat\\..*\\.util_percentage) | percent | 0 | 100 | yes | yes | yes |  |

### Load Average

| Fully Qualified Name (FQN) | Description | Units | Min | Max | BASE | CORR | UTIL | Related Default Policies |
|---------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------|-----|------|------|------|------|--------------------------|
| netuitive.linux.loadavg.01.normalized | The is the average run queue size over the past minute, normalizedacross CPUs.Computation:attribute[‘cpus’] == null ? null : (data[‘loadavg.01’].actual /attribute[‘cpus’].value) |  | 0 | none | yes | no | no |  |
| netuitive.linux.loadavg.05.normalized | The is the average run queue size over the past 5 minutes, normalizedacross CPUs.Computation:attribute[‘cpus’] == null ? null : (data[‘loadavg.05’].actual /attribute[‘cpus’].value) |  | 0 | none | yes | yes | no |  |
| netuitive.linux.loadavg.15.normalized | The is the average run queue size over the past 15 minutes, normalizedacross CPUs.Computation:attribute[‘cpus’] == null ? null : (data[‘loadavg.15’].actual /attribute[‘cpus’].value) |  | 0 | none | yes | no | no |  |

### Memory

| Fully Qualified Name (FQN) | Description | Units | Min | Max | BASE | CORR | UTIL | Related Default Policies |
|-------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|-----|-----|------|------|------|-----------------------------------------------------------------------------|
| netuitive.linux.memory.utilizationpercent | Under Linux, memory buffered and cached are part of memory which can beconsidered available. See the following explanation.Computation:100 – (memory.Buffers + memory.Cached + memory.MemFree) /memory.MemTotal * 100 | percent | 0 | 100 | yes | yes | yes | Linux – Memory Utilization Threshold Exceeded, Linux – Elevated MemoryUsage |

### Network

| Fully Qualified Name (FQN) | Description | Units | Min | Max | BASE | CORR | UTIL | Related Default Policies |
|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|---------|-----|------|------|------|------|--------------------------|
| netuitive.linux.network.*.errors | The total number of errors, both transmit and receive.Computation:network.*.rx_errors + network.*.tx_errors | errors | 0 | none | yes | no | no |  |
| netuitive.linux.network.*.packets | The total number of packets, both transmitted and received.Computation:network.*.rx_packets + network.*.tx_packets | packets | 0 | none | yes | yes | no |  |
| netuitive.linux.network.*.errors.percent | The percentage of errors, both transmit and receive.Computation:(netuitive.diamond.network.*.errors /netuitive.diamond.network.*.packets) * 100 | percent | 0 | 100 | yes | no | no |  |
