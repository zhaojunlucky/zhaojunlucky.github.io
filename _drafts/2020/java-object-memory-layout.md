---
last_modified_at: 2020-08-10T03:19:38+00:00
title: Java Object Memory Layout
categories:
- jvm

---
In Hotspot VM, the object layout in the heap can be divided into three parts,

1. Header
2. Instance Data
3. Padding

## Mark Word

The Officials call the header "Mark Work".
* 32 bit word

| Object              | Format                                                    |
| ------------------- | --------------------------------------------------------- |
| normal object       | hash: 25, age: 4, biased_lock: 1, lock: 2                 |
| biased object       | JavaThread*: 23, epoch: 2 age: 4, biased_lock: 1, lock: 2 |
| CMS free block      | 32 bits                                                   |
| CMS promoted object | PromotedObject*: 29, promo_bits: 3                        |

* 64 bit word

| Object                       | Format                                                       |
| ---------------------------- | ------------------------------------------------------------ |
| normal object                | unused: 25, hash: 31, unused: 1, age: 4, biased_lock: 1, lock: 2 |
| biased object                | JavaThread*: 54, epoch: 2, unused: 1, age: 4, biased_lock: 1, lock: 2 |
| CMS promoted object          | PromotedObject*: 61, promo_bits: 3                           |
| CMS free block               | 64 bits                                                      |
| COOPs && normal object       | unused: 25, hash: 31, cms_free: 1, age: 4, biased_lock: 1, lock: 2 |
| COOPs && biased object       | JavaThread*: 54, epoch: 2, cms_free: 1, age: 4, biased_lock: 1, lock: 2 |
| COOPs && CMS promoted object | narrowOop: 32, unused: 24, cms_free: 1, unused: 4, promo_bits: 3 |
| COOPs && CMS free block      | unused: 21, size: 35, cms_free: 1, unused: 7                 |

> * hash contains the identity hash value: largest value is
>   31 bits, see os::random().  Also, 64-bit vm's require
>   a hash value no bigger than 32 bits because they will not
>   properly generate a mask larger than that: see library_call.cpp
>   and c1_CodePatterns_sparc.cpp.
>
> * the biased lock pattern is used to bias a lock toward a given
>   thread. When this pattern is set in the low three bits, the lock
>   is either biased toward a given thread or "anonymously" biased,
>   indicating that it is possible for it to be biased. When the
>   lock is biased toward a given thread, locking and unlocking can
>   be performed by that thread without using atomic operations.
>   When a lock's bias is revoked, it reverts back to the normal
>   locking scheme described below.
>
>   Note that we are overloading the meaning of the "unlocked" state
>   of the header. Because we steal a bit from the age we can
>   guarantee that the bias pattern will never be seen for a truly
>   unlocked object.
>
>   Note also that the biased state contains the age bits normally
>   contained in the object header. Large increases in scavenge
>   times were seen when these bits were absent and an arbitrary age
>   assigned to all biased objects, because they tended to consume a
>   significant fraction of the eden semispaces and were not
>   promoted promptly, causing an increase in the amount of copying
>   performed. The runtime system aligns all JavaThread* pointers to
>   a very large value (currently 128 bytes (32bVM) or 256 bytes (64bVM))
>   to make room for the age bits & the epoch bits (used in support of
>   biased locking), and for the CMS "freeness" bit in the 64bVM (+COOPs).
>
>   [JavaThread* | epoch | age | 1 | 01]       lock is biased toward given thread
>
>   [0           | epoch | age | 1 | 01]       lock is anonymously biased
>
> * the two lock bits are used to describe three states: locked/unlocked and monitor.
>
>   | Format                   | Flag | Lock States | Description                          |
>   | ------------------------ | ---- | ----------- | ------------------------------------ |
>   | prt                \| 00 | 00   | locked      | ptr points to real header on stack   |
>   | header  \| 0 \| 01       | 01   | unlocked    | regular object header                |
>   | ptr                \| 10 | 10   | monitor     | inflated lock (header is wapped out) |
>   | ptr                \| 11 | 11   | marked      | used by markSweep to mark an object  |
>   |                          |      |             | not valid at any other time          |
>
>   We assume that stack/thread pointers have the lowest two bits cleared.