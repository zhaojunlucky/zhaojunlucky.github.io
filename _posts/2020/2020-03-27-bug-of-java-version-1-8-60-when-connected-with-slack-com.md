---
date: 2020/03/27 05:52
categories:
- java
- ssl
- https
- slack
title: 'HTTPS connection bug in Java version 1.8.60 when connected with slack.com '

---
Recently, our Jenkins job integrated with slack.com occurred error like,

```java

    javax.net.ssl.SSLHandshakeException: Remote host closed connection during handshake
    	at sun.security.ssl.SSLSocketImpl.readRecord(SSLSocketImpl.java:992)
    	at sun.security.ssl.SSLSocketImpl.performInitialHandshake(SSLSocketImpl.java:1375)
    	at sun.security.ssl.SSLSocketImpl.startHandshake(SSLSocketImpl.java:1403)
    	at sun.security.ssl.SSLSocketImpl.startHandshake(SSLSocketImpl.java:1387)
    	at org.apache.http.conn.ssl.SSLSocketFactory.connectSocket(SSLSocketFactory.java:543)
    	at org.apache.http.conn.ssl.SSLSocketFactory.connectSocket(SSLSocketFactory.java:409)
    	at org.apache.http.impl.conn.DefaultClientConnectionOperator.openConnection(DefaultClientConnectionOperator.java:177)
    	at org.apache.http.impl.conn.ManagedClientConnectionImpl.open(ManagedClientConnectionImpl.java:304)
    	at org.apache.http.impl.client.DefaultRequestDirector.tryConnect(DefaultRequestDirector.java:611)
    	at org.apache.http.impl.client.DefaultRequestDirector.execute(DefaultRequestDirector.java:446)
    	at org.apache.http.impl.client.AbstractHttpClient.doExecute(AbstractHttpClient.java:882)
    	at org.apache.http.impl.client.CloseableHttpClient.execute(CloseableHttpClient.java:82)
    	at jenkins.plugins.http_request.util.HttpClientUtil.execute(HttpClientUtil.java:155)
    	at jenkins.plugins.http_request.HttpRequest.performHttpRequest(HttpRequest.java:298)
    	at jenkins.plugins.http_request.HttpRequest.performHttpRequest(HttpRequest.java:262)
    	at jenkins.plugins.http_request.HttpRequestStep$Execution.run(HttpRequestStep.java:220)
    	at jenkins.plugins.http_request.HttpRequestStep$Execution.run(HttpRequestStep.java:195)
    	at org.jenkinsci.plugins.workflow.steps.AbstractSynchronousNonBlockingStepExecution$1$1.call(AbstractSynchronousNonBlockingStepExecution.java:47)
    	at hudson.security.ACL.impersonate(ACL.java:213)
    	at org.jenkinsci.plugins.workflow.steps.AbstractSynchronousNonBlockingStepExecution$1.run(AbstractSynchronousNonBlockingStepExecution.java:44)
    	at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:511)
    	at java.util.concurrent.FutureTask.run(FutureTask.java:266)
    	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
    	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
    	at java.lang.Thread.run(Thread.java:745)
    Caused by: java.io.EOFException: SSL peer shut down incorrectly
    	at sun.security.ssl.InputRecord.read(InputRecord.java:505)
    	at sun.security.ssl.SSLSocketImpl.readRecord(SSLSocketImpl.java:973)
    	... 24 more
```

This error starts from March 6, before that date, it works well.

I tried with Java 13 on my notebook, everything is ok. So, I guess maybe slack did some change in their HTTPS certificate cause the error.

_Solution:_

Upgrade Java `1.8.60` to Java `1.8.241` fixed this issue