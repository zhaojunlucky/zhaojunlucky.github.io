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
  
### Mapping
* `@Column(name, nullable, length, insertable, updatable)`
* `@JoinTable(name)`, `@JoinColumn(name)`

### Relationship
* `@OnetoOne`, `@OneToMany`, `@ManyToOne`, `@ManyToMany`
* `@OrderBy`

## Repository
### Enable JPA Repository
* `@EnableJPARepositories`

### `Repository<T, ID>` Interface
* `CrudRepository<T, ID>`
* `PagingAndSortingRepository<T, ID>`
* `JpaRepository<T, ID>`

### Query Methods
* find...By.../read...By.../query...By.../get...By...
* count...By...
* ...OrderBy...\[ASC/DESC\]
* And/Or/IgnoreCase
* Top/First/Distinct