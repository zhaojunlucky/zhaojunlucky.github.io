---
last_modified_at: 2020-08-10T01:51:29+00:00
title: JVM Arguments
categories:
- jvm

---
* `-Xms`, minimum heap memory
  * Example: -Xms20m
* `-Xmx`, max heap memory
  * Example: -Xmx20m
* `-XX:+HeapDumpOnOutOfMemoryError`, let JVM dump current memory snapshot when out of memory
* `-Xss`, max stack size, different on OS
  * Example: -Xss128k. Recursive call or define more local arguments.
* `-XX:PermSize`, `-XXMaxPermSize`
  * only take effect below JDK6
  * from JDK 7, perm generation moved to Java heap
  * ```java
    aa
    ```