---
last_modified_at: 2020-06-07T09:31:33+00:00
title: Spring Boot Data Source
categories:
- spring boot

---
## Data Source

Exclude Spring boot auto-configuration

* DataSourceAutoConfiguration
* DataSourceTransactionManagerAutoConfiguration
* JdbcTemplateAutoConfiguration

```java
@SpringBootApplication(exclude={DataSourceAutoConfiguration.class, DataSourceTransactionManagerAutoConfiguration.class, JdbcTemplateAutoConfiguration.class})
public class SpringBootApplication {
// omit other code

  @Bean
  @ConfigurationProperties("bar.properties")
  public DataSourceProperties barDataSourceProperties() {
      return new DataSourceProperties();
  }

  @Bean
  public DataSource barDataSource() {
      var dataSourceProps = barDataSourceProperties();
      return dataSourceProps.initializeDataSourceBuilder().build();
  }

  @Bean
  @Resource
  public PlatformTransactionManager barTxManager(DataSource ds) {
      return new DataSourceTransactionManager(ds);
  }

  // configure another
}
```

## Connection Pool
### HikariCP
This is the default in SpringBoot 2.  
Why fast?
* Bytecode optimization with JavaAssist
* Replace `ArrayList` with `FastStatementList`
* No lock `ConcurentBag`
* Proxy class optimization (replace invokestatic replace invokevirtual)

General configurations.
* spring.datasource.hikari.maximumPoolSize=10
* spring.datasource.hikari.minimumIdle=10
* spring.datasource.hikari.idleTimeout=600000
* spring.datasource.hikari.connectionTimeout=30000
* spring.datasource.hikari.maxLifeTime=1800000

### Alibaba Druid
TBD

## SQL
### JdbcTemplate
* Insert, delete, update, query
* batchUpdate
  * batchPreparedStamentSetter
  
### NamedParameterJdbcTemplate
* batchUpdate
  * SqlPatameterSourceUtils.createBatch
  
## Spring Transaction
### Consistent Transaction Model
* JDBC/Hibernate/myBaits
* DataSource/JTA

### Transaction Core Interface
* PlantformTransactionManager
  * DataSourceTransactionManager
  * HibernateTransactionManager
  * JtaTransactionManager
  
* Transaction Definition
  * Propagation (Add 7)
  * Isolation (database isolation)
  * Timeout
  * Read-only status

Examples.

```java
void commit(TransactionStatus status) throws TransactionException;
void rollback(TransactionStatus status) throws TransactionException;
TransactionStatus getTransaction(@Nullable TransactionDefinition definition) throws TransactionException;
```