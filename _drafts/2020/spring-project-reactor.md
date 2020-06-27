---
last_modified_at: 2020-06-27T01:37:20+00:00
title: Spring Project Reactor
categories:
- spring project reactor

---
## Core Concept

### Operators - Publisher/Subscriber

* Nothing happens until you subscribe
* Flux \[0..N\] - onNext(), onComplete(), onError()
* Mono \[0..1\] - onNext(), onComplete(), onError()

Backpressure

* Subscription
* onRequest(), onCancel(), onDispose()