---
layout: post
title: "OS: System Calls"
date: 2016-09-22
sources: lecture; Modern Operation Systems, Tanenbaum & Bos; http://flint.cs.yale.edu/cs422/doc/art-of-asm/pdf/CH17.PDF
type: summary
---

## Why are system calls used?
Operating systems are split into two levels. The user level has restricted access to the computer, and external applications and libraries run here. The other level, which is called the kernel level, has unrestricted access to the computer. For protection, applications and libraries cannot directly access this level. However, sometimes user-level code needs to do something that's not possible given the restricted access of the user level. So user-level code uses system calls to access kernel-level services.

## How are system calls carried out?
A program in user mode uses system calls similar to how it uses other functions. A system call might involve paramters, so the program would put these parameters on the stack, as it would for other functions. Then, the program calls a procedure, which executes a TRAP. A TRAP instruction makes the computer switch from user mode to kernel mode. Once it's in the unrestricted kernel mode, the computer checks to see which system call was called and carries out that system call. After carrying out the system call, the computer returns to user mode. If the program had put parameters onto the stack for the system call, it moves the stack back up. Then it continues with the original program.
