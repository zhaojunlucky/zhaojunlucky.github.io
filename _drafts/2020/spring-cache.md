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

## Connection with Redis

The new spring data Redis uses `LettuceConnectionFactory` to replace `JedisConnectionFactory`.

* RedisStandaloneConfiguration
* RedisSentinelConfiguration
* RedisClusterConfiguration

### Read-Write Separation

Lettuce supports read-write separation.

* Read-only primary server, read-only secondary server
* Read primary server first, read secondary server first

LettuceClientConfiguration

LettucePoolingClientConfiguration

LettuceClientConfigurationBuilderCustomizer

### RedisTemplate

_RedisTemplate<K, V>_

* opsForXxx()

_StringRedisTemplate_

**Don't forget to set expire time**

### RedisRepository

**Annotations**

* `@RedisHash`
* `@Id`
* `@Indexed`

**Example**

* Properties
  ```bash
  spring.redis.host=localhost
  spring.redis.lettuce.pool.maxActive=5
  spring.redis.lettuce.pool.maxIdle=5
  ```

* Repository
  ```java
  public interface CoffeeCacheRepository extends CrudRepository<CoffeeCache, Long> {
      Optional<CoffeeCache> findOneByName(String name);
  }
  ```
* Cache Entity
  ```java
  @RedisHash(value = "springbucks-coffee", timeToLive = 60)
  @Data
  @NoArgsConstructor
  @AllArgsConstructor
  @Builder
  public class CoffeeCache {
      @Id
      private Long id;
      @Indexed
      private String name;
      private Money price;
  }
  ```

## Handle Different Data Source Repository

How to distinguish these repositories?

* Based on entity annotation
* Based on the inherited interface type
* Scan different package