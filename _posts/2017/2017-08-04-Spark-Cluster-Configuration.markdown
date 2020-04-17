---
title:  "Spark Cluster Configuration"
date:   2017-08-04 21:27:21 +0800
categories: spark
---

Following the [Hadoop configurations](https://zhaojunlucky.github.io/2017/08/04/Hadoop-Cluster-Configuration.html).
 
In $SPARK_HOME/conf:

* Configure `spark-env.sh` <br>   

  ```cp spark-env.sh.template spark-env.sh ``` and add following:  
  ```
  PYSPARK_DRIVER_PYTHON=python3
  export HADOOP_CONF_DIR=/usr/local/hadoop/etc/hadoop
  export SPARK_MASTER_HOST=$Master IP
  export SPARK_WORKER_PORT=20001
  ```
* Configure `slaves`   
  `cp slaves.template slaves` and add all slaves IP address or hostname line by line, master also can be added as slave.
* Add environment variable SPARK_HOME and add $SPARK_HOME/bin into path
* SCP configured SPARK into all slaves
  > Make sure $SPARK_HOME are at same location on all slaves like master

* Start and Stop Spark cluster  
  Start Spark cluster by run
  `$SPARK_HOME/sbin/start-all.sh`, then open [http://Master IP:8080](http://Master IP:8080) to view Spark status.  
  Stop Spark cluster by run `$SPARK_HOME/sbin/stop-all.sh`

* Test with Spark PI example  
  ```
  /usr/local/spark/bin/spark-submit \
  --class org.apache.spark.examples.SparkPi \
  --master spark://Master IP:6066 \
  --deploy-mode cluster \
  --supervise \
  --executor-memory 1G \
  --total-executor-cores 3 \
  /usr/local/spark/examples/jars/spark-examples_2.11-2.2.0.jar \
  100000
  ```
  Check the Spark Web UI to see results.
