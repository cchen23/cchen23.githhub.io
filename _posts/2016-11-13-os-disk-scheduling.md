---
layout: post
title: "OS: Disk Scheduling"
date: 2016-11-13
sources: Lecture
type: summary
---

## Why Do We Schedule Disks?
Disks offer relatively large amounts of storage. When a computer tries to read from or write to [disk](http://cdn.computerhope.com/harddrive.jpg), it needs to move the disk so that the disk head is at the proper spot on the disk. This involves spinning the disk to place the correct [sector](http://www.minitool.com/images-mt/lib/hard-disk-bad-sectors.jpg) underneath the disk head. It also involves moving the disk arm so that the correct [track](http://www.minitool.com/images-mt/lib/hard-disk-bad-sectors.jpg) is under the disk head. Moving the disk and arm takes time, so we want to schedule read/write requests to more efficiently move the disk and arm.

## How Can We Schedule Disks?
Various algorithms exist for scheduling disks. Some of these algorithms use the sectors of read/write operations to determine how best to spin the disk.

### FIFO
The FIFO algorithm responds to read/write operations in the order that they arrive. This provides fairness, but at the cost of efficiency, since the disk might excessively spin back and forth.

### Shortest Seek Time First (SSTF)
This algorithm responds to operations according to which is closest to the head's current location. It provides more efficiency, but it might never respond to an operation if other, closer requests keep coming in.

### Elevator
This algorithm always moves the disk in a certain direction. It starts from a point on disk, and spins in one direction, responding to the closest read/write operations in the current direction of travel. When the disk reaches one end, it changes direction and does the same thing. This helps avoid starving requests, but it still might cause a request to wait a long time, since a request might have to wait until the disk spins all the way to one end and then spins all the way back, picking up requests along the way in each direction.

### C-SCAN
This algorithm works similarly to the elevator algorithm, but it only picks up requests in one direction. When it switches directions, it spins directly to the opposite end without picking up requests. Once it reaches the opposite end, it switches directions again and starts picking up requests. This decreases the maximum wait time for a request. However, it has some efficiency costs since the disk does not respond to any requests when it spins back to the starting end.
 
