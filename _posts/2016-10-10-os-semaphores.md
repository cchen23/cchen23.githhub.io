---
layout: post
title: "OS: Semaphores"
date: 2016-10-10
sources: Modern Operation Systems, Tanenbaum & Bos; lecture
type: summary
---

## Motivation
[Mutexes](https://cchen23.github.io/blog/2016/10/10/os-mutexes) can ensure that no two threads access the same resource at the same time, but it cannot control which thread accesses the resource first. Sometimes it matters that a certain thread must access the resource before the other thread. For example, two threads might share a buffer, with one thread (the producer) putting items into the buffer and the other (the consumer) taking items out of it. If the buffer is full, then the producer must wait for the consumer to run first, and if the buffer is empty then the consumer must wait for the producer. Programs can use semaphores to enforce both order and mutual exclusion.

## Semaphores
Semaphores address this problem. A semaphore has an integer value that represents access to a resource. The value can only be changed by two operations: wait() and signal(). When a thread calls the wait() function, it decrements the value of the semaphore. If the value of the semaphore is negative, that means that the resource is not available so the thread blocks. When a thread calls the signal() function, it increments the value of the semaphore. If the value of the semaphore is not positive, that means that there is at least one thread waiting for the resource, so the thread that called signal() unblocks one of the waiting threads. The unblocked thread now has access to the resource and continues executing.

## Semaphores as Mutexes
Semaphores that only hold two values can implement mutual exclusion. For example, the semaphore can represent a free lock with a value of 1 and a held lock with 0. When a value tries to acquire a lock, it calls wait() on the semaphore. If the semaphore had value 1, then wait() decrements it to 0 and acquires the lock. If the semaphore had value 0, that means the lock is not free, so the thread blocks. When a thread releases a lock, it calls signal() on the semaphore to set its value to 1, and unblocks a thread that is waiting for the semaphore.
