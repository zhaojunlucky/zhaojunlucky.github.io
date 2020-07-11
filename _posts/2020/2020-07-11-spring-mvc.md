---
last_modified_at: 2020-07-05T02:03:27+00:00
title: Spring MVC
categories:
- spring mvc

---
## Understanding Spring MVC

### DispatcherServlet

* Controller
* xxxResolver
  * ViewResolver
  * HandlerExceptionResolver
  * MultipartResolver
* HandlerMapping

## Spring MVC Annotations

* `@Controller`
  * `@RestController`
* `@RequestMapping`
  * `@GetMapping` / `@PostMapping`
  * `@PutMapping` / `@DeleteMapping`
* `@RequestBody` / `@ResponseBody` / `@ResponseStatus`

## Spring Application Context

### Diagram

### Interface

* BeanFactory
  * DefaultListableBeanFactory
* ApplicationContext
  * ClassPathXmlApplicationContext
  * FileSystemXmlApplicationContext
  * AnnotationConfigApplicationContext
* WebApplicationContext

## Understanding the Request Handling Process

### Bind Attributes

* WebApplicationContext / LocalResolver / ThemeResolver

### Process Multipart

* Convert the request to MultipartHttpServletRequest if it's multipart

### Handler Processing

* Execute the controller `pre` and `post` logic if handler found

### Process and Render the Model

## Custom Processing Method

### Custom Mapping Relationship

#### `@Controller`

#### `@RequestMapping`

* path/method. Specify the path and method
* params/header. Limit the mapping scope
* consumes/produces. Limit request/response format

#### Some shortcuts

* `@RestController`
* `@GetMapping`/`@PostMapping`/`@PutMapping`/`@DeleteMapping`/`@PatchMapping`
* `@RequestBody`/`@ResponseBody`/`@ResponseStatus`
* `@PathVariable`/`@RequestParam`/`@RequestHeader`
* `HttpEntity`/`ResponseEntity`

### Custom Type Converter

#### Implement `WebMvcConfigurer`

* Spring Boot implements one `WebMvcAutoConfiguration`
* Add User-defined `Converter`
* Add User-defined `Formatter`

### Custom Validation

* Validate the binding result through `Validator`
  * Hibernate Validator
* `@Valid` Annotation
* BindingResult

### Multipart Upload

* Configure MultipartResolver
  * Spring Boot supports auto-configure `MultipartAutoConfiguration`
* Support Type `multipart/form-data`
* MultipartFile type