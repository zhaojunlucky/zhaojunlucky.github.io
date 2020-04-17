---
date: 2019/11/18 12:01
categories:
- java
title: Store two integers in a long

---
Store two integers in a long in Java. 
```java
    long l = (((long)x) << 32) | (y & 0xffffffffL);
    int x = (int)(l >> 32);
    int y = (int)l;
```