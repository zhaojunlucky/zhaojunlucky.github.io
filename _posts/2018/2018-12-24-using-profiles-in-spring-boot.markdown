---
title: "Using Profiles in Spring Boot"
date: "2018-12-24 16:45"
categories: [spring, spring boot, profile]
---

When developping a Spring Boot application, or developping any applicaions, it's offen to follow below process,
* Develop in local environment. Mostly may be on Windows
* Run some automation test, such as integration test on a testing environment
* Deploy to a product environment

In each stage, a separated environment is required, such as,
* different database
* different server hostname
* different Kafka server or topic name

So, we may have define all the configurations in a file, such as 'application.properties',
  ```
  spring.datasource.url=jdbc:mysql://localhost/test
  spring.datasource.username=dbuser
  spring.datasource.password=dbpass
  spring.datasource.driver-class-name=com.mysql.jdbc.Driver
  spring.kafka.bootstrap-servers=localhost:9092
  ```
And, there also may be some common configurations are applied for all, so how can we use the Spring profile to make easiest work to achieve?

Here is the way,
* By default, the Spring boot will try to read condfigurations from file `application.properties` or `application.yml`. Let's name it as common profile.
* To create a `dev` profile, simply add new configuration file such as `application-dev.properties` or `application-dev.yml`
  Now, we can put common configurations into the `common` profile, and put the `dev` configurations into the dev profile.

And then, the next step is how to let the Spring boot known to use which profile?

There are several ways to do,
* Use `Profile` annotation
  In the configuration class, we can define to use which profile.
  ```java
  @Configuration
  @Profile("dev")
  public class ProfileConfiguration {
    ...
  }
  ```
* Use environment variable
  before start the application, export environment.
  ```bash
  export SPRING_PROFILES_ACTIVE=dev
  ```
  On windows,
  ```bash
  set SPRING_PROFILES_ACTIVE=dev
  ```
* Use startup argument
  Pass in the application arguments.
  `java -jar <application.jar> --spring.profiles.active=dev`.


Now, you could create and use multiple profiles in Spring boot.
