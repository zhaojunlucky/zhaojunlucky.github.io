---
last_modified_at: 2020-06-27T02:15:15+00:00
title: Spring Data Reactive Access
categories:
- spring data reactor

---
## Spring Data Redis

**Lettuce supports Reactive**

**Spring Data Redis Reactive Supports**

* ReactiveRedisConnection
* ReactiveRedisConnectionFactory
* ReactiveRedisTemplate
  * opsForXxx()

## Spring Data MongoDB

**MongoDB provides support for Reactive**

* mongodb-driver-reactivestreams

**Spring Data MongoDB Support**

* ReactiveMongoClientFactoryBean
* ReactiveMongoDatabaseFactory
* ReactiveMongoTemplate

## Spring Data R2DBC

### R2DBC

* Reactive Relational Database Connectivity

### Supported Databases

* PostgreSQL (io.r2dbc:r2dbc-postgres)
* H2 (io.r2dbc:r2dbc-h2)
* MSSQL (io.r2dbc:r2dbc-mssql)

### R2DBC Classes

* ConnectionFactory
* DatabaseClient
  * execute().sql(SQL)
  * select() / insert()
  * inTransaction(db -> {})
* R2dbcExceptionTranslator
  * SqlErrorCodeR2dbcExceptionTranslator

### R2DBC Repository

* `@EnableR2dbcRepositories`
* `ReactiveCrudRepository<T, ID>`
  * `@Table` / `@Id`
  * All the methods return `Flux` or `Mono`
  * User-defined query needs write `@Query` by yourself

## Use AOP to Print Database Access Layer Abstract

### Spring AOP Core Concept

| Concept | Description |
| --- | --- |
| Aspect | aspect |
| Join Point | connection point, it reprents one method execution in Spring AOP |
| Advice | notification, the action executed in the join point |
| Pointcut | describe how to match the join point |
| Introduction | provide extra method and property for the existing type declaration |
| Target object | Target object |
| AOP proxy | AOP proxied object, ethier JDK dynamic proxy or CGLIB proxy |
| Weaving | the process which connect the aspect and the target object or create proxy for the type |

**Related Classes**

* `EnableTransactionManagement`
  * `boolean proxyTargetClass() default true`, true will use CGLIB
* `ProxyTransactionManagementConfiguration`
* `TransactionInterceptor`
* `MethodInterceptor`
* 