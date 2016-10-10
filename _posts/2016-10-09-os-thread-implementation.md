---
layout: post
title: "OS: Thread Implementation Types"
date: 2016-10-09
sources: Modern Operation Systems, Tanenbaum & Bos
type: summary
---

[Threads](https://cchen23.github.io/blog/2016/10/02/os-processes-threads) allow computers to work more efficiently. They represent multiple executions of the same program, all of which share memory. There are two main ways to implement threads: at the kernel level and at the user level. People also use combinations of these two ways in hybrid implementations.

## Type: User Level Implementation
When threads are implemented at the user level, the kernel does not know that they exist. The responsibility for scheduling threads falls on the user, which lets the user specify how to schedule these threads. This lets the user take the specifics of the program into account, and create a better scheduling algorithm. In addition, this implementation allows for faster context switches, because the OS does not have to get involved in context switching. However, this causes some problems. The OS does not know how many threads each process has, so it cannot take that information into account when scheduling processes. This could cause uneven allocation of CPU time. Also, when one thread becomes blocked, it causes the kernel to block the thread's process and take it off of the CPU. This could stop the process' threads that are ready to run from executing.

## Type: Kernel Level Implementation
Implementing threads at the kernel level solves some of these problems. Since the kernel knows about the threads, it can take into account how many threads a process has when scheduling CPU time. In addition, it can make sure that a single blocked thread does not prevent all other threads in the process from executing. However, this comes at a cost. This implementation causes more expensive context switches, since the kernel needs to get involved.
