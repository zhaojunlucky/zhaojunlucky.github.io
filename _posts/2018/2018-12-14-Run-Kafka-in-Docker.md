---
date: 2018-12-14 11:08:51 +0800
categories: docker kafka 
title: Run Kafka in Docker
---

For some development purpose with Kafka, it’s often required to test with a dedicated server, despite the official production and testing instance.

But the official installation needs to run the zookeeper and Kafka server separately, and also prepare the environment. So, it’s better to run it in the Docker, and have own controls.

## What the Docker is
* Run the zookeeper and Kafka in one Docker 
* Every start will totally create a new instance 
* Allow ssh into the Docker to do troubleshooting 

## Where is the Docker
Check in Github [Kafka Docker](https://github.com/zhaojunlucky/docker-tutorial/tree/master/kafka).
