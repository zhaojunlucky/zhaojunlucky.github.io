---
last_modified_at: 2020-06-26T03:48:34+00:00
title: Spring Cache
categories:
- spring cache

---
## Spring Provide Uniformed Cache Abstraction

* Add cache support for Java method to cache the execute result
* Support `ConcurrentMap`, `EhCache`, `Caffeine`, `JCache(JSR-107`
* Interfaces
  * `org.springframework.cache.Cache`
  * `org.springframework.cache.CacheManager`

## Cache Annotations

### `@EnableCaching(procyTargetClass=true)`

* `@Cacheable`
* `@CacheEvict`
* `@CachePut`
* `@Caching`
* `@CacheConfig`

### Use Redis as Cache

Configurations,

* spring.cache.type = redis
* spring.cache.cahe-names = coffee
* spring.cache.redis.time-tolive = 5000
* spring.cache.redis.cache-null-values = false
* spring.redis.host = localhost