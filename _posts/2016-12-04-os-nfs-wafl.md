---
layout: post
title: "OS: NFS and WAFL"
date: 2016-12-4
sources: lecture; Modern Operation Systems, Tanenbaum & Bos
type: summary
---

## Network File System (NFS)
Network file systems allow computers to access files on other computers over a network. Clients request access to files on servers by specifying a path name. Servers respond to requests with a file handle containing information about the file, such as its i-node and security info.

### Stateful vs Stateless
NFS can be stateful or stateless. 
Stateful NFS servers maintain information on behalf of clients. For example, if a client reads something from a file the server keeps track of the client's location. This means that the client can send less information in each request, but if the server crashes then information about open files would be lost.
Stateless NFS servers do not keep any information about the client. This means that the client needs to send more information in each request, but it also means that a server crash does not lose information about open files. Also, if the network contains a cluster of servers, clients do not have to use the same stateless server for each request.

### Challenge: Caching
One problem that arises in network file systems involves caching. If two clients request and cache the same file, a client might not know of updates made to the file by the other client. A partial solution, which decreases the risk of uncoordinated modifications, involves updating the file at regular intervals. These updates involve both propagating a client's changes to the server and retrieving an updated version of the file from the server.
Other solutions involve only allowing a single client to cache a file at a time, or using a network lock manager to make sure that updates look sequential.

## Write Anywhere File Layout (WAFL)
The WAFL provides faster file services and more flexible file growth.

### Layout
The WAFL uses different i-node formats for different file sizes. For the smallest files, the i-node directly stores data blocks. For larger files, the i-node consists of pointers, which either point to data (for smaller files) or to more pointers, which can in turn point either to data or pointers (depending on the file size).
The file system consits of a root i-node which points to everything else and metadata files, such as an i-node file, a file indicating free blocks, and a file indicating free i-nodes. Because of this, the file system can write metadata blocks anywhere on disk, which allows it to optimize metadata location for read/write performance and also allows it to more easily grow the file system.

### Snapshots
WAFL uses snapshots to store previous versions of the file system. To make a snapshot, it copies the root i-node and sets the copy as the active file system. The system then uses copy-on-write for files: when a file changes for the first time after snapshot creation, the file system creates an updated copy of the block. The root i-node in the active file system points to the updated copy while the root i-node in the snapshot points to the original copy of the block. (The file system similarly copies any ancestors of the changed block.)
After a crash, the file system reverts to the latest snapshot, which ensures that it returns to a consistent version of the file system.
To impmlement these snapshots, WAFL uses a block map in which each entry contains bits indicating whether a given snapshot is using a specific block.
