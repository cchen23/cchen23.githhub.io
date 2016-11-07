---
layout: post
title: "OS: Message Passing"
date: 2016-11-07
sources: lecture, misc reading
type: summary
---

## Motivation
Message passing allows different processes to communicate with each other. This communication can happen between processes on the same computer or on different computers in the same network. The consumer process receives a message and the producer process sends a message.

## Message Passing within a System
Various methods allow processes to communicate with each other within a system. One method, called direct addressing, allows processes to specify which process they want to send a message to or receive a message from. Since this method specifies the producer or consumer, it works for message passing between a single producer and a single consumer.
Another method, called indirect addressing, allows multiple producers and consumers communicate with each other. In this method, processes specify a mailbox that they wish to send a message to a receive a message from, instead of specifying the other process. By specifying the same mailbox, processes can communicate with each multiple other processes.
Both of these methods provide one-way communication -- processes specify whether they wish to send or receive a message.
Another method, which uses sockets, allows for two-way communication between processes. Sockets come in two types. A datagram socket gives higher performance but does not guarantee that messages will be successfully sent, or that they will be sent in a given order. In contrast, a stream socket gives lower performance but provides more reliable guaranteees about communication order and success. Within this method, sockets bind to an endpoint which specifies an IP address (which identifies a machine) and a port. A process within the specified machine that listens at the same port can receive information from that socket.

### Indirection
Ports and mailboxes both provide indirection. This indirection means that producers and consumers specify the port or mailbox they wish to communicate with, which means that they do not have to name a specific process with which they will communicate.

## Message Passing Over a Network
Remote procedure calls allow a process to communicate with processes on the same network but on a different computer. They are structured so that a process can communicate with a process on a different computer using something that, for the process, looks like a local function call.

## Problems
Two problems that arise from message passing involve lost messages and corrupted messages. 
When a producer sends a message to a consumer, the consumer might never actually receive the message. To deal with this problem, the consumer might send an acknowledgement message back to the producer. However, this message might become lost as well -- if so, the producer might end up sending the message again, and the consumer would receive the same message multiple times. One way to deal with this problem uses identifiers for each message. Using these identifiers, the consumer can figure out when it has received the same message multiple times.
In addition, messages might become corrupted. To know when this happen, the producer can send a checksum along with its message, which is some function of the message. The consumer can check that the message matches its checksum. If it does not, the consumer can ask the producer to re-send the message.
