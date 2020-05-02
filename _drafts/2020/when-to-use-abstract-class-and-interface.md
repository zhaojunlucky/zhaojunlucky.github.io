---
last_modified_at: 2020-05-02T07:37:21+00:00
title: When to Use Abstract Class and Interface
categories:
- java

---
Consider using interfaces if any of these statements apply to your situation:

1. You expect that unrelated classes would implement your interface. For example, the interfaces Comparable and Cloneable are implemented by many unrelated classes.
2. You want to specify the behavior of a particular data type, but not concerned about who implements its behavior.
3. You want to take advantage of multiple inheritances.