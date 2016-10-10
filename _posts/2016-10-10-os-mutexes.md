---
layout: post
title: "OS: Mutexes"
date: 2016-10-10
sources: Modern Operation Systems, Tanenbaum & Bos; lecture
type: summary
---

## Motivation
When mutiple [threads](https://cchen23.github.io/blog/2016/10/02/os-processes-threads) run at the same time, they take turns executing on the CPU. A pre-emptive scheduler periodically switches the thread that has control of the CPU, interrupting the running thread and running a different thread. 

### Critical Section
Sometimes programs have critical sections -- if multiple threads overlap in their execution of the critical section, errors might occur. For example, a program might increase a variable  by a certain amount by retrieving the value, calculating the new value, and saving the new value. A scheduler might interrupt a thread that has calculated, but not stored, the new value. The scheduler might start running a different thread that tries to do the same thing. Since the first thread did not store the new value, the second thread uses the original value in its calculation. It increases the old value and saves its calculation into the variable. When the scheduler returns to the first thread, it continues executing where it left off -- the first thread stores its calculation (which increased the original vallue of the variable). At the end of all this, even though both threads tried to increase the variable, the value of the variable was only increased once.

### Mutual Exclusion
When threads overlap in their execution of critical sections, the outcome depends on how the OS schedules the threads. Since this scheduling is not determined by the program, unexpected outputs might result. This is called a race condition. Mutual exclusion prevents this from happening. Mutexes, which implement mutual exclusion, make sure that threads do not overlap in executing critical sections.

## Locks
Mutexes use locks to enforce mutual exclusion. Only one thread has the lock at each time, and a thread can only execute a critical section when it has the lock.
A thread attempts to acquire a lock. If the lock is not free, then the CPU puts itself on a queue for the lock and yields the CPU. When a thread finishes its critical section, it gives up the lock, and dequeues a waiting thread (if any threads are waiting for the lock). 
However, implementing locks might run into the same problem -- two threads might both try to access a lock, and interrupts might make both threads think that they are the only thread with the lock. There are various ways to get around this.

### Implementation: Disable Interrupts
One way to implement locks involves disabling interrupts when attempting to acquire a lock. Since the scheduler cannot interrupt the thread while it acquires the lock, the lock can enforce mutual exclusion.

### Implementation: Use Hardware Support
Some hardware supports a Test&Set atomic operation. The scheduler cannot interrupt an atomic operation. The Test&Set operation tries to set a value -- if the value is already set, it returns a failure. This can be used with value that guards access to a lock. When a thread wants to access the lock, it checks if the guard has been set. If so, it gets access to the lock. If not, it waits until the guard is free.
