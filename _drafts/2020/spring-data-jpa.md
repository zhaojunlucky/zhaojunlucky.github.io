---
last_modified_at: 2020-06-20T07:31:56+00:00
title: Spring Data JPA
categories:
- jpa

---
## Java Persistence API
JPA provides a POJO based persistence model for object relationship mapping
* Simplify the persistence code development
* Shield the differences of different persistence APIs for java community

## Spring Data JPA Anotations
### Entity
* `@Entity`, `@MappedSuperclass
* `@Table(name)`

### Primary Key
* `@Id`
  * `@GeneratedValue(stategy, generator)`
  * `@SequenceGenerator(name, sequenceName)`