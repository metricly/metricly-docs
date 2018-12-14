---
title: "metrics"
#date: 2018-12-12
draft: false
tags: ["postresql", "integrations", "metrics" ]
author: Lawrence Lane
---
## Collected

| Friendly Name            | Fully Qualified Name (FQN)        | Description                                                                                                   | Statistic | Units | Min | Max  | Sparse Data Strategy (SDS) | BASE | CORR | UTIL |
|--------------------------|-----------------------------------|---------------------------------------------------------------------------------------------------------------|-----------|-------|-----|------|----------------------------|------|------|------|
| Blocks Hit               | postgres.database.*.blks_hit      | The number of times disk blocks were found already in the PostgreSQLbuffer cache so a read was not necessary. | average   |       | 0   | none | none                       | yes  | no   | no   |
| Blocks Read              | postgres.database.*.blks_read     | The number of disk blocks read in the database.                                                               | average   |       | 0   | none | none                       | yes  | no   | no   |
| Connections              | postgres.database.*.connections   | The number of connections to the database.                                                                    | average   |       | 0   | none | none                       | yes  | no   | no   |
| Backend Connections      | postgres.database.*.numbackends   | The number of backends currently connected to the database.                                                   | average   |       | 0   | none | none                       | yes  | no   | no   |
| Database Size            | postgres.database.*.size          | The size of the database.                                                                                     | average   |       | 0   | none | none                       | yes  | no   | no   |
| Deleted Rows             | postgres.database.*.tup_deleted   | Number of rows deleted by queries in the database.                                                            | average   |       | 0   | none | none                       | yes  | no   | no   |
| Fetched Rows             | postgres.database.*.tup_fetched   | Number of rows fetched by queries in the database.                                                            | average   |       | 0   | none | none                       | yes  | no   | no   |
| Inserted Rows            | postgres.database.*.tup_inserted  | Number of rows inserted by queries in the database.                                                           | average   |       | 0   | none | none                       | yes  | no   | no   |
| Returned Rows            | postgres.database.*.tup_returned  | Number of rows returned by queries in the database.                                                           | average   |       | 0   | none | none                       | yes  | no   | no   |
| Updated Rows             | postgres.database.*.tup_updated   | Number of rows updated by queries in the database.                                                            | average   |       | 0   | none | none                       | yes  | no   | no   |
| Committed Transactions   | postgres.database.*.xact_commit   | Number of transactions in the database that have been committed.                                              | average   |       | 0   | none | none                       | yes  | no   | no   |
| Rolled Back Transactions | postgres.database.*.xact_rollback | Number of transactions in the database that have been rolled back.                                            | average   |       | 0   | none | none                       | yes  | no   | no   |
