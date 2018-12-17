---
title: "Metrics"
#date: 2018-12-12
draft: false
tags: ["ruby", "integrations", "agents", "metrics" ]
author: Lawrence Lane
---

## Collected

| Fully Qualified Name (FQN)                      | Statistic | Units        | Min | Max  | Sparse Data Strategy (SDS) |
|-------------------------------------------------|-----------|--------------|-----|------|----------------------------|
| action_controller.halted_callback               | sum       | count        | 0   | none | zero                       |
| action_controller.redirect                      | sum       | count        | 0   | none | zero                       |
| action_controller.total_requests                | sum       | count        | 0   | none | zero                       |
| action_controller.*.total_requests              | sum       | count        | 0   | none | zero                       |
| action_controller.*.*.request.query_time        | average   | milliseconds | 0   | none | zero                       |
| action_controller.*.*.request.total_duration    | average   | milliseconds | 0   | none | zero                       |
| action_controller.*.*.request.view_time         | average   | milliseconds | 0   | none | zero                       |
| action_controller.*.*.total_requests            | sum       | count        | 0   | none | zero                       |
| action_controller.*.request.queue_time          | average   | milliseconds | 0   | none |                            |
| action_controller.errors                        | average   | count        | 0   | none |                            |
| action_view.render_partial                      | sum       | count        | 0   | none | zero                       |
| action_view.render_template                     | sum       | count        | 0   | none | zero                       |
| action_record.instantiation                     | sum       | count        | 0   | none | zero                       |
| action_record.sql.statement                     | sum       | count        | 0   | none | zero                       |
| GC.profiler.total_time                          |           |              |     |      |                            |
| GC.stat.count                                   |           |              |     |      |                            |
| GC.stat.heap_allocatable_pages                  |           |              |     |      |                            |
| GC.stat.heap_allocated_pages                    |           |              |     |      |                            |
| GC.stat.heap_available_slots                    |           |              |     |      |                            |
| GC.stat.heap_eden_pages                         |           |              |     |      |                            |
| GC.stat.heap_final_slots                        |           |              |     |      |                            |
| GC.stat.heap_free_slots                         |           |              |     |      |                            |
| GC.stat.heap_live_slots                         |           |              |     |      |                            |
| GC.stat.heap_marked_slots                       |           |              |     |      |                            |
| GC..stat.heap_sorted_length                     |           |              |     |      |                            |
| GC.stat.heap_swept_slots                        |           |              |     |      |                            |
| GC.stat.heap_tomb_pages                         |           |              |     |      |                            |
| GC.stat.major_gc_count                          |           |              |     |      |                            |
| GC.stat.malloc_increase_bytes                   |           |              |     |      |                            |
| GC.stat.malloc_increase_bytes_limit             |           |              |     |      |                            |
| GC.stat.minor_gc_count                          |           |              |     |      |                            |
| GC.stat.old_objects                             |           |              |     |      |                            |
| GC.stat.old_objects_limit                       |           |              |     |      |                            |
| GC.stat.oldmalloc_increase_bytes                |           |              |     |      |                            |
| GC.stat.oldmalloc_increase_bytes_limit          |           |              |     |      |                            |
| GC.stat.remembered_wb_unprotected_objects       |           |              |     |      |                            |
| GC.stat.remembered_wb_unprotected_objects_limit |           |              |     |      |                            |
| GC.stat.total_allocated_objects                 |           |              |     |      |                            |
| GC.stat.total_allocated_pages                   |           |              |     |      |                            |
| GC.stat.total_freed_objects                     |           |              |     |      |                            |
| GC.stat.total_freed_pages                       |           |              |     |      |                            |
| ObjectSpace.count_objects.*                     | average   | count        | 0   | none | zero                       |
| sidekiq.*.job.count                             | average   | count        | 0   | none |                            |
| sidekiq.default.*.job.count                     | average   | count        | 0   | none |                            |
| sidekiq.default.job.count                       | average   | count        | 0   | none |                            |
| sidekiq.errors                                  | average   | count        | 0   | none |                            |

## Computed

| Fully Qualified Name (FQN)                        | Description                                                                                                                       | Statistic | Units | Min | Max  | BASE | CORR | UTIL |
|---------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|-----------|-------|-----|------|------|------|------|
| netuitive.ruby.action_controller.*.total_duration | The total time spent on requests to a specific controller.Computation:data.sum(‘action_controller.${1}.*.request.total_duration’) | average   | ms    | 0   | none | yes  | yes  | no   |
