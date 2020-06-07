---
last_modified_at: 2020-06-07T09:31:33+00:00
title: Spring Boot
categories:
- spring boot

---
## Datasource

Exclude Spring boot auto-configuration

* DataSourceAutoConfiguration
* DataSourceTransactionManagerAutoConfiguration
* JdbcTemplateAutoConfiguration

```java
@SpringBootApplication(exclude={DataSourceAutoConfiguration.class, DataSourceTransactionManagerAutoConfiguration.class, JdbcTemplateAutoConfiguration.class})
public class SpringBootApplication {
...

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
```