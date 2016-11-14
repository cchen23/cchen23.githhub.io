---
layout: post
title: "OS: Thrashing"
date: 2016-11-13
sources: lecture; Modern Operation Systems, Tanenbaum & Bos;
type: summary
---

## What Causes Thrashing?
As part of the [virtual memory](https://cchen23.github.io/blog/2016/11/07/os-virtual-memory) system, the operating system moves pages of tasks' address spaces between disk and memory. The OS can use various [algorithms](https://cchen23.github.io/blog/2016/11/09/os-page-replacement-algorithms) to try to minimize the movement of pages (since moving pages between disk and memory takes time). However, sometimes tasks can still cause excessive movement of pages. This is known as thrashing.

## How Can the OS Deal With Thrashing?
The idea of [working sets](https://cchen23.github.io/blog/2016/11/09/os-page-replacement-algorithms#working-set) says that tasks use certain sets of pages at different points in the code. If memory holds a task's working set, then the operating system will not have to retrieve pages from disk. However, sometimes a task's working set does not fit in the memory allocated to it by the operating system.

### Allocating Pages in Memory
One solution involves allocating memory. The operating system can allocate memory locally or globally. If it allocates memory locally, then each process has a certain number of pages in memory. Each page only holds memory for its specified process. If an operating system allocates memory globally, then it takes into account all tasks' memory requests when deciding what to store on a given page in memory. With global allocation, the operating system uses more information to decide what to store on each page in memory, so it can allocate pages in a way that is more optimal overall. However, this might be unfair, since some tasks could use disproportionately many pages in memory.

The operating system can try to deal with thrashing by balancing page allocation between processes. If one task has many page misses, then it probably does not have enough pages in memory. If another task has very few page rates, then it might have too many pages in memory. The operating system can give pages from the task with the low miss rate to the task with the high miss rate.

### Make Processes Inactive
Sometimes, balancing page allocation does not stop thrashing. In these cases, perhaps the computer does not have enough memory to run all the tasks at once. Therefore the operating system might make some tasks inactive, and give their pages to other tasks. Once the active tasks finish running, then the operating system can re-activate inactive tasks and let them run with more pages in memory. The operating system might decide which tasks to make inactive by choosing tasks with high miss rates, since they are not running efficiently anyways. In addition, the operating system can try to maintain a mix of CPU-heavy and I/O-heavy active tasks since a task using the CPU and a task using I/O can run at the same time.
