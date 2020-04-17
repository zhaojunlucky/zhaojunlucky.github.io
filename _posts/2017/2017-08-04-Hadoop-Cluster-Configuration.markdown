---
title:  "Hadoop Cluster Configuration"
date:   2017-08-04 21:27:21 +0800
categories: hadoop
---

## Environment Configuration

### User configuration
* Create hadoop user  
  `sudo useradd -m hadoop -s /bin/bash`
* Set password for user 'hadoop'  
  `sudo passwd hadoop`
* Add hadoop user into sudoers
  `sudo adduser hadoop sudo`  
  
> You Need configure hadoop user on all related servers

### SSH configuration
Master needs connect to all slaves via ssh without password, we need copy master's public key to all slaves.   

* Generate key pair for hadoop user on all servers with following steps:  

  * Create .ssh directory for hadoop user  
    `mkdir -p ~/.ssh`
  * Generate key pair  
    `ssh-keygen -t rsa -b 4096`
* Copy master's public key to all slaves  
  `ssh-copy-id haddop@slaves`
  
> Then in master server can ssh to any slaves without input the password

### Java Installation

Install Java JDK on all servers with ***same version and location***. And configure JAVA_HOME and add java into system or user environment path.
> You can set the Java home and the path in user profile *~/.bashrc* or system profile */etc/profile*, and source the changed profile to make it effective

## Hadoop Configuration

Download the Hadoop binary file from apache site to master server, and configure it with following steps:  
> Make sure the user hadoop have the ownership on the decompressed hadoop binary directory, and configure the hadoop under hadoop user

### Configure hadoop

* Set JAVA_HOME in hadoop enviroment file  
  In $HADOOP_HOME/etc/hadoop/hadoop-env.sh file, edit `export JAVA_HOME=$JAVA_HOME` as `export JAVA_HOME=${your java installation}`
* Configure `core-site.xml` as  
  ```xml
  <configuration>
    <property>  
      <name>hadoop.tmp.dir</name>
      <value>/usr/hadoop/tmp</value>
    </property>
    <property>
      <name>fs.default.name</name>
      <value>hdfs://$Master IP:9000</value>
    </property>
  </configuration>
  ```  
  > Make sure the path of hadoop.tmp.dir exists, and ***don't put it under /tmp***   

* Configure `hdfs-site.xml`  
  Based on how many slaves you are, make sure the `dfs.replication` value less than the number of slaves.  
  ```xml
  <configuration>
    <property>
        <name>dfs.replication</name>
        <value>2</value>
    </property>
    <property>
        <name>dfs.namenode.datanode.registration.ip-hostname-check</name>                   
        <value>false</value>
    </property>
  </configuration>
  ```
> The `dfs.namenode.datanode.registration.ip-hostname-check` will disable the IP hostname check if you don't want it  

* Configure `mapred-site.xml`  
  Configure the job tracker.
  ```xml
  <configuration>
    <property>
        <name>mapred.job.tracker</name>
        <value>http://$Mastetr IP:9001</value>
    </property>
  </configuration>
  ```

* Configure `slaves`  
  Edit file `slaves` add all slaves' IP address or hostname into it line by line. Master also can be added as slave.

* Add HADOOP_HOME, and add $HADOOP_HOME/bin into PATH in master server
* Copy the configured hadoop directory into all slaves  
  `scp -r $HADOOP_HOME hadoop@slave`
  
> Put $HADOOP_HOME on all slaves with same location as master, and run `sudo chown -R hadoop:hadoop $HADOOP_HOME` on all slaves if needed

## Start & Stop Hadoop

* Format namenode in master with user hadoop (one-time operation)  
  `hadoop namenode -format` 
* Start Hadoop  
  ```
     start-dfs.sh  
     start-yarn.sh
  ```
  Open [http://Master IP:50070](http://Master IP:50070) to view Hadoop status
* Stop Hadoop
  ```
     stop-yarn.sh
     stop-dfs.sh
  ```
> You may search google for any issues
