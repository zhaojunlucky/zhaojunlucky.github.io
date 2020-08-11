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
  * from JDK 7, String constant moved from perm generation to Java heap. From JDK 8, perm generation has been replaced by metaspace
  * The following code will print "true", "true" in JDK 6, print "true", "false" in JDK 7 and later.

    ```java
    String str1 = new StringBuilder("computer").append("software").toString();
    System.out.println(str1.intern() == str1);
    
    String str2 = new StringBuilder("ja").append("va").toString();
    System.out.println(str2.intern() == str2);
    ```
* `-XX:MaxMetaspaceSize`, set the max size of the metaspace. Default -1 no limitation.
* `-XX:MetaspaceSize`, set the initial size of the metaspace, the unit is bytes. If the used size exceeds this size, will trigger GC and size adjustment:
  * If released a lot of space, then decrease this value
  * If released space is low, then increase this value(not exceeds the max value)
* `-XX:MinMetaspaceFreeRation`, set the minimal ration of the free space
* `-XX:MaxMetaspaceFreeRation`, set max ration of the free space
* `-XX:MaxDirectMemorySize`, set the max direct memory size. Default is the same as the -Xmx.