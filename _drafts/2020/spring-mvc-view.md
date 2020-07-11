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