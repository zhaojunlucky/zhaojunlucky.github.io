---
title: "Jenkine Pipeline Basic Usage"
date: "2018-12-19 13:05"
categories: Jenkins pipeline groovy
---

Jenkins pipeline is groovy based DSL, we can use groovy to access the Jenkins instance, and access its project job, or even builds.

In order to access the Jenkins instance, we need to import its class.
```java
import jenkins.model.Jenkins
import hudson.model.*
```
Here are some basics,
* find a job

  `def job = Jenkins.instance.getItemByFullName('project name')`

  For free style job, its class is `hudson.model.FreeStyleProject`.
* list its build

  `def builds = job.builds`

  The class of the builds is `hudson.util.RunList<hudson.model.FreeStyleBuild>`.
* get build's parameters as a HashMap

  ```groovy
  def paras = build.actions.find{ it instanceof ParametersAction }?.parameters
  def map = new java.util.HashMap<String, String>()
  for (def p : paras) {
     map.put(p.name, p.value)
  }
  return map
  ```

* get build's environment variables (depends on EnvInject plugin)

  ```groovy
  def envs = build.actions.find{it instanceof org.jenkinsci.plugins.envinject.EnvInjectPluginAction}.getEnvInjectVarList().getEnvMap()

  def map = new java.util.HashMap<String, String>()
  for (def env : envs) {
      map.put(p.key, p.value)
  }
  return map
  ```
