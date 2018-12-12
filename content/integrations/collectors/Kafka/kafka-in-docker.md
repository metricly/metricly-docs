---
title: "Kafka in Docker"
date: 2018-12-11
draft: false
tags: ["kafka", "integrations", "collectors", "docker" ]
author: Lawrence Lane
---
Getting the Jolokia agent running in a Kafka container requires three additional modifications to the `docker run` command. To illustrate the modifications needed, we’re going to assume that your `docker run` command looks like this initially:

```
docker run -p 2181:2181 -p 9092:9092 --env ADVERTISED_HOST=`docker-machine ip\`docker-machine active\`` --env ADVERTISED_PORT=9092 spotify/kafka
```
## Update `Docker Run` Command

1. Make the Jolokia JAR file available to the container by passing it in as a mounted volume.

```
-v /opt/netuitive-agent/jolokia-jvm-1.3.4-agent.jar:/opt/netuitive-agent/jolokia-jvm-1.3.4-agent.jar
```
2\. Pass in the `KAFKA_OPTS` environment variable to Kafka so it starts with the Jolokia agent included.

```
-e KAFKA_OPTS=-javaagent:/opt/netuitive-agent/jolokia-jvm-1.3.4-agent.jar=port=8778,host=0.0.0.0
```
3\. Expose the Jolokia port.

```
-p 8778:8778
```

Here’s what the full command looks like with the three additional portions added:

```
docker run -p 2181:2181 -p 9092:9092 -p 8778:8778 -e ADVERTISED_HOST=`docker-machine ip \`docker-machine active\`` -e ADVERTISED_PORT=9092 -e KAFKA_OPTS=-javaagent:/opt/netuitive-agent/jolokia-jvm-1.3.4-agent.jar=port=8778,host=0.0.0.0 -v /opt/netuitive-agent/jolokia-jvm-1.3.4-agent.jar:/opt/netuitive-agent/jolokia-jvm-1.3.4-agent.jar spotify/kafka
```
