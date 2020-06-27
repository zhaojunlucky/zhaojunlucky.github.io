---
last_modified_at: 2020-06-27T01:37:20+00:00
title: Project Reactor
categories:
- project reactor

---
## Core Concept

### Operators - Publisher/Subscriber

* Nothing happens until you subscribe
* Flux \[0..N\] - onNext(), onComplete(), onError()
* Mono \[0..1\] - onNext(), onComplete(), onError()

### Backpressure

* Subscription
* onRequest(), onCancel(), onDispose()

### Thread Schedulers

* immediate() / single() / newSingle()
* elastic() / parallel() / newParallel()

### Error Handling

* onError / onErrorReturn / onErrorResume
* doOnError / doFinally