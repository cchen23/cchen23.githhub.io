s---
layout: post
title: "OS: Scheduler"
date: 2016-10-11
sources: Modern Operation Systems, Tanenbaum & Bos; lecture
type: summary
---

## Purpose of Schedulers
Computers use [processes and threads](https://cchen23.github.io/blog/2016/10/02/os-processes-threads) to use the CPU more efficiently. Sometimes this involves overlapping the execution of these jobs, and a scheduler decides the order and length of time that the jobs get to use the CPU.

## Pre-emptive vs Non-pre-emptive Schedulers
One way to differentiate schedulers looks at whether they use pre-emption. Pre-emptive schedulers can force a job to pause and give up the CPU. Non-pre-emptive schedulers only put a new job on the CPU if the running process volunatarily yields the CPU or cannot continue running on the CPU (for example, if it becomes blocked by an unavailable resource or if it needs to wait for I/O input).

## Algorithms for Scheduling
A variety of algorithms exist for scheduling, and different algorithms have their own benefits and limitations. 
Some goals for scheduling algorithms include fairness and measurements of speed. Fairness means that the scheduling algorithm treats similar jobs in similar ways. Various measurements of speed exist. For example, people can measure average time a job takes to complete (turnaround), average number of jobs processed per hour (throughput), and the amount of time an interactive system takes before responding to a command (response time).
Different systems prioritize different goals, and choose scheduling algorithms accordingly.
