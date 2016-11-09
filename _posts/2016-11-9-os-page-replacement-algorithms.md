---
layout: post
title: "OS: Page Replacement Algorithms"
date: 2016-11-9
sources: Modern Operation Systems, Tanenbaum & Bos
type: summary
---

## Why are Page Replacement Algorithms Needed?
Computers use [virtual memory](https://cchen23.github.io/blog/2016/11/07/os-virtual-memory) to run programs more effectively and to provide protection. This involves keeping certain pages in physical memory, where they can be retrieved more quickly. Physical memory is not big enough to hold the full virtual address space of all processes, so the operating system uses page replacement algorithms to decide which virtual memory pages to replace when it brings in pages from disk.

## Types of Page Replacement Algorithms
Ideally, a page replacement algorithm runs quickly and always replaces the page that will not be used for the longest time. However, since the operating system does not usually know when pages will be used in the future, a number of algorithms exist to approximate this ideal. Some of these algorithms involve adding reference bits and modified bits to each page table entry. If a process modifies a page, then the page's modified bit becomes one. If a process references a page in a given time period, then the page's reference bit becomes 1.

### Not Recently Used
This algorithm keeps track of the pages that a process has modified, and the pages that a process has referenced within a given time period. When the algorithm must choose a page to replace, it chooses a page that the process has not recently used -- it tries to use the past to predict the future. This algorithm comes with some overhead, since it must maintain and scan through information about whether a process has modified and/or referenced each page.

### FIFO (with Second Chance)
The most straightforward version of this algorithm always replaces the oldest page. This method comes with relatively low overhead, but it might not approximate the ideal algorithm very well, since a process might use an old page very frequently.

The FIFO with Second Chance algorithm helps address that problem. Instead of always replacing the oldest page, this algorithm checks the oldest page's reference bit. If it is zero, then it replaces the page. If the reference bit is one, then the algorithm sets the page's reference bit to zero and places the page at the end of the list. This method can be implemented with a queue, but that adds overhead since the algorithm might move pages relatively frequently. A different implementation uses the idea of a clock, in which the clock hand points to the oldest page and advances along pages in order of page age.

### Least Recently Used
This method keeps track of the latest use of each page and replaces the page that has not been used for the longest time. The implementation of this method poses some overhead, since the operating system must keep track of a timestamp for each page, and the algorithm must compare all the timestamps when choosing a page to replace.

To address these difficulties, an algorithm can instead approximate LRU by separating pages into various bins depending on their last time of reference (as opposed to keeping track of the exact time of last reference for each page).

### Not Frequently Used (with Aging)
A straightforward implementation of this algorithm just counts the number of times a page has been referenced. However, a program might reference a page many times towards the beginning of its executing and then stop using it. This algorithm cannot account for that change.

A modification of this algorithm, NFU with Aging, accounts for changes in a program's use of pages by weighting reference counts. For example, it might periodically right-shift each page's reference counts, which has the effect of weighting reference counts according to how long ago they occurred.

### Working Set
Usually, programs use different subsets of its pages at different parts of the code, and the working set contains the pages that a program uses at a given time. Algorithms that use this idea try to keep the working set in memory. They can approximate the working set by looking at the pages that a process has used within a given time period, and replaces pages that the process has not referenced in a given time period. This algorithm can also be implemented using a clock model.
