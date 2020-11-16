---
last_modified_at: 2020-11-16T08:57:07+00:00
title: Use Reflection in Jenkins Pipeline
categories:
- jenkins pipeline

---
Jenkins Pipeline's class loading is different from the normal Java class loading. It has its own designed class loading within the plugins.

Here is the official introduction [dependencies-and-class-loading](https://www.jenkins.io/doc/developer/plugin-development/dependencies-and-class-loading/ "dependencies-and-class-loading").

Briefly, if we want to use reflection to dynamic load class defined in pipeline, we need to use **`Thread`**`.currentThread().getContextClassLoader()`.

```java
Class<?> cls = Class.forName(className, true, Thread.currentThread().getContextClassLoader())
return cls.getDeclaredConstructors()[0].newInstance()
```