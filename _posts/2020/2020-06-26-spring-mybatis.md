---
last_modified_at: 2020-06-21T07:55:27+00:00
title: Spring MyBatis
categories:
- spring mybatis

---
## Simple Configurations

* mybatis.mapper-location = classpath_:mapper/_**/*.xml
* mybatis.type-aliases-package = type alias' package name
* mybatis.type-handlers-package = type handler package name
* mybatis.configuration.map-underscore-to-camel-case = true

## Mapper's Definition and Scan
* `@MapperScan` configures scan location
* `@Mapper` defines interface
* Mapping definition (XML and anotation)

  ```java
  @Mapper
  public interface CoffeeMapper {
      @Insert("insert into t_coffee (name, price, create_time, update_time)"
              + "values (#{name}, #{price}, now(), now())")
      @Options(useGeneratedKeys = true) // return the new id
      int save(Coffee coffee);

      @Select("select * from t_coffee where id = #{id}")
      @Results({
              @Result(id = true, column = "id", property = "id"),
              @Result(column = "create_time", property = "createTime"),
              // map-underscore-to-camel-case = true 可以实现一样的效果
              // @Result(column = "update_time", property = "updateTime"),
      })
      Coffee findById(@Param("id") Long id);
  }
  ```