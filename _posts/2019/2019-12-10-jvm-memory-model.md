---
date: 2019/12/10 03:28
categories:
- java
- memory model
title: JVM Memory Model

---
## Java JVM Memory Model

### JDK 8

![/uploads/JVM Memory Model-JDK8.png](https://app.forestry.io/sites/iavzbjhqguasuw/body-media//uploads/JVM Memory Model-JDK8.png)

## GC

### Garbage Collection Algorithm

* Mark-Sweep
  * Performance issue (stop the world)
  * Space fragmentation(the free space is not continuous)
* Copying

  To solve the problem of efficiency, a "copy" collection algorithm has emerged. It divides the memory into two blocks of the same size and uses one of them at a time. When this piece of memory is cleaned up, the surviving objects are copied to another piece, and then the used space is cleaned up. In this way, each time the memory is collected, half of the memory range is collected.
* Mark-Compact

  A tagging algorithm based on the characteristics of the old generation. The tagging process is still the same as the "mark-sweep" algorithm, but the subsequent steps are not to directly recycle the recyclable objects, but to move all surviving objects to one end and then clean up directly. Memory beyond the end boundary. No division.
* Generational Collection

  The current generation of garbage collection for virtual machines uses a generational collection algorithm. This algorithm has no new ideas, but only divides the memory into several blocks according to the different life cycle of the object. The java heap is generally divided into new generation and old generation, so we can choose the appropriate garbage collection algorithm according to the characteristics of each generation.

  For example, in the new generation, a large number of objects die every time you collect, so you can choose a replication algorithm, and you only need to pay a small amount of object replication costs to complete each garbage collection. The old generation object has a higher probability of survival, and there is no extra space to guarantee its allocation, so we must choose "mark-clear" or "mark-finish" algorithms for garbage collection.

### Why Young Generation & Old Generation (Tenured Generation)

The only reason is to optimize GC performance.

The HotSpot VM divides the young generation into three parts. One Eden and two Survivors and the default ration are 8:1. The garbage in the young generation is Minor GC. On the contrary, the garbage in the old generation is Major GC or Full GC. The frequency of Minor GC is much higher than the Major GC.

### Garbage collector

* Serial

  ![/uploads/Serial.png](https://app.forestry.io/sites/iavzbjhqguasuw/body-media//uploads/Serial.png)
  * Young Generation

    Copying
  * Old Generation

    Mark-Compact
  * Suit for client mode
* PairNew

  ![](/uploads/PairNew.png)

  It's the same as the Serial collector except it uses multiple GC threads.

  It suits for server-side mode.
* Parallel Scavenge

  ![](/uploads/PairNew.png)

  It likes the same as the PairNew collector. But it cares about the throughput, efficient use of CPU.

  The so-called throughput is the ratio of the time in the CPU used to run user code to the total CPU consumption time. The Parallel Scavenge collector provides many parameters for users to find the most suitable pause time or maximum throughput. If you do not know much about the collector operation, if manual optimization is difficult, you can choose to hand over memory management optimization to the virtual machine to complete it.
* CMS

  ![](/uploads/CMS.png)
  * Initial Mark

    Pause all other threads and record the objects directly connected to root, very fast
  * Concurrent Mark

    Turn on the GC and user threads at the same time, and use a closure structure to record reachable objects. But at the end of this phase, this closure structure is not guaranteed to contain all currently reachable objects. Because the user thread may continuously update the reference domain, the GC thread cannot guarantee the real-time performance of the reachability analysis. So this algorithm keeps track of where these reference updates occur.
  * Remark

    The remark phase is to modify the marking record of the part of the object whose marking changes due to the user program continuing to run during the concurrent marking period. The pause time in this phase is generally slightly longer than the initial marking phase, which is much longer than the concurrent marking phase. short
  * Concurrent Sweep

    The user thread is started, and the GC thread starts cleaning the marked area.
  * Concurrent Reset

  Advantages & Disadvantages
  * Advantages

    Concurrent collection, low pause
  * Disadvantage

    Sensitive to CPU resources.

    Unable to handle floating garbage.

    The"mark-clear" algorithm it uses will cause a large amount of space debris to be generated at the end of the collection.
* G1

  TBD