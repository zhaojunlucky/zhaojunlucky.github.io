---
last_modified_at: 2020-07-11T08:55:30+00:00
title: Spring MVC Expcetion Handling
categories:
- spring mvc expcetion handling

---
## Spring MVC Exception Basic

### Core

* HandlerExceptionResolver

### Implementation

* SimpleMappingExpcetionResolver
* DefaultHandlerExceptionResolver
* ResponseStatusExceptionResolver
* ExeptionHandlerExceptionResolver

## Spring MVC Exception Handle Methods

### Method

* @ExceptionHandler

### Add Location

* @Controller/@RestController
* @ControllerAdvice/@RestControllerAdvice

>  Low priority than @ExpceionHandler in controller class.

Add HTTP status annotation in Exception class.

## Spring MVC Interceptor

### Core

* HandlerInterceptor
  * boolean preHandle()
  * void postHandle()
  * void afterCompletion()