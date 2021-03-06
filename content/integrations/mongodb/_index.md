---
title: "MongoDB"
#date: 2018-12-12
draft: false
tags: ["#mongoDB", "#integrations" ]
author: Lawrence Lane
---
 MongoDB is a document-oriented NoSQL database. CloudWisdom can be used to monitor your MongoDB’s performance.

## Prerequisites

The [Linux Agent][1] must be setup before you proceed with the MongoDB integration.

## Configure

1. Navigate to the collectors folder, `/opt/netuitive-agent/conf/collectors`.
2. Open the **MongoDBCollector.conf** file.
3. Change the **enabled** setting to `True`.
4. Replace the default host address and/or port number if necessary.
5. **Save** the configuration file, and **restart** the Linux Agent.

{{% notice info %}}
Due to the large number of metrics generated by MongoDB, you shouldn’t monitor more than one MongoDB host per agent.
{{% /notice %}}

## Collector Options

| Option                 | Default                                                                                                                                                | Description                                                                                                                                                                                                                |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| enabled                | FALSE                                                                                                                                                  | Enable collecting these metrics.                                                                                                                                                                                           |
| host                   | 127.0.0.1:27017                                                                                                                                        | A single hostname(:port) to collect from. Overrides hosts.                                                                                                                                                                 |
| metrics_blacklist      | “.*databases.*\|.*metrics.repl.executor.shuttingDown.*\|.*storageEngine.*\|.*writeBacksQueued.*\|.*mem.supported.*\|.*tcmallocformattedString.*\|^percent.*” | Regex list to match metrics to block. Mutually exclusive with metrics_whitelistoption.                                                                                                                                     |
| simple                 | TRUE                                                                                                                                                   | Set to “True” to only collect the same metrics as mongostat.                                                                                                                                                               |
| byte_unit              |                                                                                                                                                        | Default numeric output(s).                                                                                                                                                                                                 |
| cluster                |                                                                                                                                                        | If this node is part of a cluster, the collector will collect metrics on the cluster health.                                                                                                                               |
| collection_sample_rate | 1                                                                                                                                                      | Only send stats for a consistent subset of collections. This is applied after collections are ignored via the ignore_collectionssetting. Sampling uses crc32 to ensure consistency across replicas. Value between 0 and 1. |
| databases              | .*                                                                                                                                                     | A regex of databases to gather metrics for.                                                                                                                                                                                |
| hosts                  | ['localhost']                                                                                                                                          | An array of hostname(:port) elements to collect metrics from. Set an alias by prefixing “host:port” with alias@                                                                                                            |
| ignore_collections     | '^tmp\.mr\'                                                                                                                                            | A regex of which collections to ignore. MapReduce temporary collections (tmp.mr.*)are ignored by default.                                                                                                                  |
| metrics_whitelist      |                                                                                                                                                        | Regex list to match metrics to transmit. Mutually exclusive with metrics_blacklistoption.                                                                                                                                  |
| network_timeout        |                                                                                                                                                        | Timeout for mongodb connection (in milliseconds).                                                                                                                                                                          |
| passwd                 |                                                                                                                                                        | Password for authenticated login (optional).                                                                                                                                                                               |
| replica                | False                                                                                                                                                  | Set to “True” to enable replica set logging. Reports health of individual nodes as well as basic aggregate stats.                                                                                                          |
| ssl                    | False                                                                                                                                                  | Set to “True” to enable SSL connections to the MongoDB server.                                                                                                                                                             |
| translate_collections  | False                                                                                                                                                  | Translate dot (.) to underscores (_) in collection names.                                                                                                                                                                  |
| user                   |                                                                                                                                                        | User name for authenticated login (optional).                                                                                                                                                                              |
| ssl_certfile           |                                                                                                                                                        | The certificate file used to identify the local connection against mongod.
| ssl_keyfile            |																			  | The private keyfile used to identify the local connection against mongod.
| ssl_pem_passphrase     |																			  | The password or passphrase for decrypting the private key in ssl_certfile or ssl_keyfile. Only necessary if the private key is encrypted.
| ssl_cert_reqs          |																			  | Specifies whether a certificate is required from the other side of the connection, and whether it will be validated if provided.
| ssl_ca_certs           |																			  | The ca_certs file contains a set of concatenated certification authority certificates, which are used to validate certificates passed from the other end of the connection.
| ssl_crlfile            |																			  | The path to a PEM or DER formatted certificate revocation list.
| ssl_match_hostname     | True																			  | Enables hostname verification.
| auth_mechanism         | SCRAM-SHA-1																		  | The default MongoDB authentication mechanism.

[1]: /integrations/agents/linux-agent
