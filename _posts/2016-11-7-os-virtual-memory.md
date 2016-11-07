---
layout: post
title: "OS: Virtual Memory"
date: 2016-11-07
sources: lecture, misc reading
type: summary
---

## Motivation for Virtual Memory
Computer usually have a memory hierarchy that includes slow/large memory and fast/small memory. There is not enough fast/small memory to fulfill the memory requirements for all the processes, and virtual memory gives the CPU a way to deal with that problem.
Since multiple processes may run at the same time, we want to prevent them from interfering with each other. One process should not mess up another process' address space, and virtual memory can enforce that protection.
In addition, as a general rule, 80% of a process' references deal with 20% of the process' memory, so we want a way to keep that 20% in physical memory. The rest of the memory remains on disk. When it's needed, it can be pulled in from disk (the slow/large memory), but this takes longer.

## Memory Management
Each process sees a virtual address space, with contiguous addresses ranging from 0 to the maximum memory address. These virtual addresses correspond to different physical addresses in the computer's actual memory.
A memory management unit translates virtual addresses into physical addresses. There are different ways that the MMU can manage memory.

### Base and Bound
This method gives each process a base address and a bound, which specifies the maximum size of the process' address space. The process is allowed to access only the memory in the range [base, base+bound]. This method is relatively simple but not very efficient, since processes might need to relocate when their memory grows, and the computer has to swap process' memory in and out of physical memory since not all process' [base, base+bound] can fit inside physical memory.

### Paging
This method involves splitting a process' virtual memory into different pages. Each virtual memory address maps to an entry in a page table, and the page table gives the physical address of the virtual memory address (or tells the computer that the virtual address is not in physical memory, in which case the computer must retrieve the memory from disk).
Page tables themselves can become very big, so it becomes unwieldy to keep the entire page table in memory. One way to deal with this involves using a Transition Lookaside Buffer, which holds commonly used page table entries. If a needed virtual address is not found in the TLB, then the page table entry is retrieved from memory.
