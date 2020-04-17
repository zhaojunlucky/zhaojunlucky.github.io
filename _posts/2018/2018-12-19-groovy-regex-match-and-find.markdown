---
title: "Groovy & Java Regex Match and Find"
date: "2018-12-19 15:21"
categories: groovy regex java
---

Groovy provides some operators to have an efficient way to create pattern, find or test regex compared with Java.

Here are some common use case in Groovy and Java,

* create a pattern

  In Groovy,
  ```groovy
  Pattern pattern = ~/regex/
  ```
  With Java,
  ```java
  Pattern pattern = Pattern.compile(regex)
  ```

* find with Regex

  In Groovy,
  ```groovy
  Matcher matcher = "string" =~ /regex/
  if (matcher.find()) {
      def str = matcher.group(1)
  }
  ```
  With Java,
  ```java
  Pattern pattern = Pattern.compile("pattern");
  Matcher matcher = pattern.matcher("string");
  if (matcher.find()) {
      var str = matcher.group(1);
  }
  ```
* test with Regex

  In Groovy,
  ```groovy
  def match = "string" ==~ /regex/
  ```
  With Java,
  ```java
  var match = "string".matches("regex");
  ```
  or
  ```java
  var match = Pattern.matches("regex", "string");
  ```
