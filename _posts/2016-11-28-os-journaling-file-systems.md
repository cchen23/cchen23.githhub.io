---
layout: post
title: "OS: Journaling File Systems"
date: 2016-11-28
sources: lecture; Modern Operation Systems, Tanenbaum & Bos
type: summary
---

## Why are Journaling File Systems Used?
When a user modifies files, the computer initially stores these modifications in main memory and then writes the modifications to disk, which takes more time. If the computer crashes before fully writing the changes to disk, the disk could hold inconsistent files. For example, file directories on disk might point to garbage if directories are updated before their files. Even if the computer only performs bottom-up updates to avoid this problem, garbage blocks could still exist. For example, the computer might update a file but crash before it updates the directory to point to the updated file. To avoid this problem, journaling file systems make consistent updates.

## How Do Journaling File Systems Work?

### Transactions
Journaling File Systems group operations into transactions, and ensure that these transactions have the following properties (ACID):

* Atomicity: each transaction either happens fully or not at all
* Consistency: each transaction brings the system to a valid state
* Isolation: transactions have the appearance of occuring sequentially (though a certain sequence is not specified)
* Durability: transactions remain in place after they have occurred

### Logging
When carrying out a transaction, the system creates a log and performs the write-ahead process. This process writes operations that carry out the transaction in the log and writes the log to disk. Each of these operations must be idempotent. Then, it writes "commit" at the end of the log and begins the write-behind process. In this process, the system writes the log's updates to disk and then clears the log.

The computer needs to make sure that logs survive a system crash. To do this, it could write the log to disk, but this adds a large amount of overhead. Instead, the computer can write the log to NVRAM. NVRAM, another form of nonvolatile memory, is smaller than disk but writing to NVRAM takes less time. However, since the log does not include a lot of data, it can be stored on NVRAM.

### Dealing with Crashes
After a system crashes, it looks at the log. If the log has a "commit" statement, then the system re-starts the write-behind process from the beginning of the log. Since each operation in the log is idempotent, it is okay that the system might carry out an operation multiple times.
