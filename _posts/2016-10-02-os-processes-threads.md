---
layout: post
title: "OS: Processes and Threads"
date: 2016-10-02
sources: Modern Operation Systems, Tanenbaum & Bos
type: summary
---

## Motivation for Having Processes
When a computer runs a program, it spends a lot of time waiting for things that it needs to continue with the program. While it waits, it could be doing something else. Processes and threads allow the computer to fill the time that waiting time with other work that it needs to do. This makes the computer more efficient. In addition, because the computer switches much more quickly than we can observe, we perceive the illusion that computers do multiple things at the same time.

## What Processes Are
A program is a set of instructions that people write and give to the computer. Each time a computer runs the code, it runs a process. Each process represents an instance of the program in execution -- it includes the program and information related to the current state of execution. Multiple processes can be created from the same program, which happens if the program is executed multiple times. Each process has its own set of information, which includes its own address space and register values.

## What Threads Are
Threads are similar to programs in that they also represent a program in execution and allow the computer to give the illusion of multi-tasking. However, threads are smaller than processes. While each process has its own address space, each thread does not have its own address space. This means that if multiple threads are created from a program, and one of the threads changes its address space, this change will be reflected in the other threads.

### Motivation for Having Threads
Threads are less independent than processes, since they share an address space. This is an advantage when threads need to work with each other, since they all have access to the same address space. In addition, this means that its easier to switch between threads. When a computer switches processes, it needs to save lots of information (including the address space) of the outgoing process, and load all the information for the incoming process. This takes a lot of time. Since threads share the same address space, when a computer switches threads it does not have to save and load information about the address space, which saves some time.
