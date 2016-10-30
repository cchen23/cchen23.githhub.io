---
layout: post
title: "OS: Deadlock"
date: 2016-10-30
sources: lecture; Modern Operation Systems, Tanenbaum & Bos
type: summary
---

##What is Deadlock?
[Processes and threads](https://cchen23.github.io/blog/2016/10/02/os-processes-threads) allow for more efficiency by overlapping the execution of multiple tasks. In some cases, multiple tasks might use the same resources. This can cause a situation in which two or more tasks each have a resource that the other needs, but neither tasks gives up their resource until they complete their execution. In this scenario, neither task will be able to get the other resource and continue executing, so they will both wait forever. More generally, deadlock occurs when each process in a set of processes cannot continue executing until another process does something (such as releasing a resource).

##How Do We Know When Deadlock Occurs?
We can detect deadlock by determining when a set of tasks is unable to progress because they're waiting for other tasks in the set to continue executing. For example, with resource deadlock, we can make a graph of resource allocations and requests. If we find a cycle in the graph, we know that deadlock has occurred. Another way to detect if deadlock will occur involves keeping track of the allocation and requests of resources, as well as information about the total number of available resources. In this method, we repeatedly look for tasks that can run to completion giving the constraints of the current situation. If we ever find that a task will not be able to run to completion, then we know that deadlock will occur.

##How Does Deadlock Occur?
Deadlock occurs only when four conditions hold true:

1. Mutual Exclusion: multiple processes cannot share the same resource
2. Hold & Wait: processes hold their resources when they request another resource
3. No Preemption: outside forces are not allowed to take resources away from a process
4. Circular Requests: tasks form a circular chain of resource requests

##How Can We Deal with Deadlock?

###Let Deadlock Happen

####Ostrich Algorithm
The ostrich algorithm involves just letting deadlock happen. This is useful when deadlock is rare enough that it's not worth dealing with.

####Detection and Recovery
This method also allows deadlock to happen, but it tries to fix the situation afterwards. One way to fix the situation is to stop tasks that have resources needed in the resource requests causing deadlock. However, sometimes this is not possible because some processes cannot be arbitrarily stopped and restarted later.

###Stop Deadlock Before it Happens

####Resource Allocation
One way to stop deadlock from occurring involves careful resource allocation. Tasks are only allowed to continue executing if their progress does not cause a possible deadlock. However, this method requires knowledge of all the resources that all tasks will need in the future, and sometimes this information is not available.

####Prevention
Another way to stop deadlock from occuring involves preventing one of the [four conditions](##How Does Deadlock Occur?) needed for deadlock to occur.

1. Mutual Exclusion: Sometimes, we can deal with this process using a method called spooling. Spooling involves virtualizing a resource so that only one thing can directly deal with the resource. For example, spooling can be used with a printer by having tasks send their output to a buffer (instead of directly to the printer). The buffer would only send full output to the printer, so that the printer would always be able to run to completion. However, sometimes such a method is not possible. Also, this could just push the problem to another level -- instead of deadlock with the printer, deadlock could occur with the buffer if it does not have enough space to hold output from overlapped tasks.
2. Hold & Wait: If we require tasks to either get all the resources they need or get no resources at all, the Hold & Wait condition will not occur. However, we have the same problem with resource allocation -- tasks generally do not know all the resources they need ahead of time. In addition, this method can be overly cautious in terms of resource acquisition -- when a task cannot get **all** the resources it needs, it does not necessarily imply that deadlock will happen. Therefore requirement that a resource either get all or no resources can make things inefficient.
3. No Preemption: If we just take away resources that are causing deadlock, this condition will not happen. However, sometimes it's not okay to just take away resources from a process. For example, if we take away a lock that a process holds, we could violate [mutual exclusion](https://cchen23.github.io/blog/2016/10/10/os-mutexes). Or if we take away a printer from a task that's printing something, the output of the printer would become messed up.
4. Circular Requests: If we impose an order on resource requests, such that each resource has a number and each task can only request resources with a higher number than the resources it already holds, then circular resource requests will not happen. However, this makes it more difficult to write programs, and sometimes no order of resources exists that can accommodate all tasks. 

##Related Problems

###Communication Deadlock
Another type of deadlock involves communication. Instead of a set of tasks waiting for each other's resources, the tasks wait for each other's messages. For example, two tasks might try to coordinate their activity by having one task send a message to another task, and having the second task send a reply after it receives the message. If the first message gets lost, then the first task keeps waiting for a reply and the second task keeps waiting for the message. This problem can be solved by using a system to deal with possibly lost messages. This system would have to account for the fact that the first message could have been delayed rather than lost, and so having the first task send another message after a period of time could cause the second task receive the same message twice.

###Livelock
In livelock, tasks are not completely stopped, but they do not accomplish anything useful. For example, tasks A and B might both use resources X and Y. A could acquire X and B could acquire Y, and then both tasks could try to acquire the other resource, fail, release their resource, and try again. They could keep doing this forever.

###Starvation
In starvation, progress still happens, but a particular task might never get a change to keep executing. For example, if a printer always lets the task with the shortest output print, and a constant stream of short-output tasks comes in, a long-output task might never get the chance to print.
