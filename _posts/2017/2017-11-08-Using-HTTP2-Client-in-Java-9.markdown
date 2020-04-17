---
title:  " Using HTTP/2 Client in Java 9"
date:   2017-11-08 21:27:21 +0800
categories: java
---

To use HTTP/2 in Java 9, it's required to declare the dependency of module `jdk.incubator.httpclient`. Here is the Java 9 [module overview summary](https://docs.oracle.com/javase/9/docs/api/overview-summary.html).

Assume the root package is `com.jdk9.http`.

- To use module `jdk.incubator.httpclient` module,
create `module-info.java` file with content:

  ```java
  module com.jdk9.http {
      requires jdk.incubator.httpclient;
  }
  ```

- Create `HTTPClientTest.java` with following content to use HTTP Put method:

  ```java
  package com.jdk9.http;

  import jdk.incubator.http.HttpClient;
  import jdk.incubator.http.HttpRequest;
  import jdk.incubator.http.HttpResponse;
  import java.io.IOException;
  import java.net.URI;

  public class HttpClientTest {
      public static void main(String args[]){

          HttpClient client = HttpClient.newHttpClient();

          HttpRequest req =
                  HttpRequest.newBuilder(URI.create("<the url>"))
                          .headers("User-Agent","Java", "Content-Type", "application/json")
                          .PUT(HttpRequest.BodyProcessor.fromString("<body string>"))
                          .build();

          HttpResponse<String> resp = null;
          try {
              resp = client.send(req, HttpResponse.BodyHandler.asString());
              System.out.println(resp.body());
          } catch (IOException e) {
              e.printStackTrace();
          } catch (InterruptedException e) {
              e.printStackTrace();
          }
      }
  }
  ```
