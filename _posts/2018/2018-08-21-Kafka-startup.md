---
date: 2018-08-21 13:27:19 +0800
categories: Kafka Java
title:  Kafka Startup
update: 2018-08-21 13:27:19 +0800
---

## Installation

Please refer to [https://kafka.apache.org/quickstart](https://kafka.apache.org/quickstart).

## Configurations

One important thing is to change the **advertised.listeners** in ${KAFKA_HOME}/config/server.properties, like,

> \# Hostname and port the broker will advertise to producers and consumers. If not set,
> \# it uses the value for "listeners" if configured.  Otherwise, it will use the value
> \# returned from java.net.InetAddress.getCanonicalHostName().
> **advertised.listeners=PLAINTEXT://\<IP or hostname\>:9092**


Otherwise, any clients, like java, will not poll any messages from the server.
