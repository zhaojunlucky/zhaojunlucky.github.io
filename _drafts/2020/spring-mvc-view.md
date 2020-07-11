---
last_modified_at: 2020-07-11T07:16:05+00:00
title: Spring MVC View
categories:
- spring mvc

---
## View Process

### ViewResolver and View Interface

* AbstractCacheingViewResolver
* UrlBasedViewResolver
* FreeMarkerViewResolver
* ContentNegotiatingViewResolver
* InternalResourceViewResolver

### View Resolve Logic in `DispatchServlet`

* initStrategies()
  * initResolvers() initialize the ViewResolver
* doDispatch()
  * processDispatchResult()
  * if no view returns, try RequestToViewNameTranslator
  * resolveViewName() resolve view object

#### @ResponseBody

* In HandlerAdapter.handle(), it outputs the response
  * RequestMappingHandlerAdapter.invokeHandlerMethod()
    * HandlerMethodReturnValueHandlerComposite.handlerReturnValue()
      * RequestResponseBodyMethodProcessor.handleReturnValue()

### Redirect

* `rediect:`, http client 302
* `forward:`, server side

## Spring MVC Common Views

### Supported Views

* [https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html#mvc-view](https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html#mvc-view "https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html#mvc-view")
* Jackson-based JSON/XML
* Thymeleaf & Freemarker

### Configure MessageConverter

* Through configureMessageConverters() of WebMvcConfigurer
  * Spring boot auto find and register HttpMessageConverters  
    ![](/uploads/message-converter.png)

### Jackson Support in Spring Boot

* JacksonAutoConfiguration
  * Spring boot register JSON serialization component through @JsonComponent
  * Jackson2ObjectMapperBuilderCustomizer
* JacksonHttpMessageConvertersConfiguration
  * Add `jackson-dataformat-xml` to support XML serialization

## Spring Boot Static Resource Configuration and Cache

### Resource Configuration

#### Core

* WebMvcConfigurer.addResourceHandlers()

#### Common Configurations

* spring.mvc.static-path-pattern = /**
* spring.resources.static-locations = classpath:/META-INF/resources/, classpath:/resources/,classpath:/static/,classpath:/public/

### Spring Boot Resouce Cache

#### Common Configurations

* ResourceProperties.Cache
* spring.resouce.cache.cachecontrol.max-age=time
* spring.resouce.cache.cachecontrol.no-cache=true/false
* spring.resouce.cache.cachecontrol.s-max-age=time

### Controller Manually Set (Not Recommend)

![](/uploads/controller-manually-set-cache.png)