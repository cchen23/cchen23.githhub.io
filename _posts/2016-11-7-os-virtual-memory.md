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
This method gives each process a base address and a bound, which specifies the maximum size of the process' address space. The process is allowed to access only the memory in the range [base, base+bound]. This method is relatively simple but not very efficient, since processes might need to relocate when their memory grows, and the computer has to swap process' memory in and out of physical memory since physical memory cannot hold the full memory address ([base, base+bound]) of all processese at the same time.

### Paging
Since physical memory cannot hold all processes' full memory space at the same time, the computer can hold parts of processes' memory in physical memory. This method involves splitting a process' memory space into different pages. The operating system maintains a page table, which holds an entry for each virtual memory page. The page table entry tells where the virtual page lies in memory. If the page is in physical memory, then the page table entry gives the physical address of the virtual memory address. If not, the page table entry indicates that the page is not in physical memory, in which case the computer must retrieve the memory from disk (which takes much longer).
Page tables themselves can become very big, so it becomes unwieldy to keep the entire page table in memory. 

#### Translation Look-Aside Buffer
One way to deal with this involves using a Transition Lookaside Buffer, which holds commonly used page table entries. If a needed virtual address is not found in the TLB, then the operating system looks for the virtual address' page table entry. 

#### Alternate Page Table Types
An inverted page table maps physical pages to virtual pages. This means that the table size grows with the number of physical pages, rather than with the number of virtual pages. The operating system can use a hash table to quickly find virtual pages in this method.

A hierarchical page table contains multiple layers. Each virtual page number is split into an index into each level of the page table, and with those indices the operating system can traverse the multi-level page table to find the virtual address' page table entry. Because this page table is split into multiple smaller page tables, the full page table need not remain in memory.
