---
layout: post
title: "OS: I/O Devices"
date: 2016-11-7
sources: Modern Operation Systems, Tanenbaum & Bos
type: summary
---

## I/O Devices
I/O Devices serve as a means of communication between a computer and the outside world. They have two main types -- character-oriented devices read data byte-by-byte, and block-oriented devices read data in bigger chunks called blocks. Within these two main types, there are many different types of devices. To deal with the diversity of devices, device controllers provide an interface to hide the implementation details of the devices. These controllers allow software to communicate with hardware devices. In addition, device drivers provide an API so that the operating system can communicate with a device controller.

## Communication Between I/O Devices and the CPU
The CPU can use various methods to communicate with I/O Devices.

### Programmed I/O
In this method, the CPU gives a command to the device and then polls the device, continuously checking to see if it has finished the command. This takes up a lot of time, since the CPU does not accomplish other tasks while polling and waiting for the device to finish.

### Interrupt-Driven
With interrupt-driven devices, the CPU gives a command to the device and then does other work. The device generates an interrupt once it completes the command. This tells the CPU when the device finishes executing, so the CPU does not have to constantly check in with the device. However, the CPU still has to spend time transfering data with the device, which takes up CPU time.

### Direct Memory Access
Direct memory access lets an I/O device communicate directly with memory. The CPU gives guidelines about what data to transfer, and a disk adaptor handles the actual transfer of data so that the CPU can perform other tasks while data moves between the computer and the I/O device.
