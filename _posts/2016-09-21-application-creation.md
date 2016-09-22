---
layout: post
title: "OS: Creating Applications"
date: 2016-09-21
sources: lecture, misc reading
type: summary
---

Source code written in C become something that a computer can execute through a series of four steps, each of which change the file into a slightly different format.

1. **Preprocessing**: People use comments to make the coding process clearer. They also use directives to give instructions to the computer -- for example, they might define a constant to use throughout the code. The preprocessor deals with these things by removing comments, which the computer doesn't use, and following directives. It produces a modified file written in C for the compiler to use.
2. **Compiling**: C is easier for people to work with, but computers don't work directly with C, so the compiler translates the program from C to assembly as an intermediate step.
3. **Assembler**: The computer doesn't deal directly with assembly, either, so the assembler translates the program from assembly language to object code, which the computer can actually understand.
4. **Linker**: However, there are some parts of the program that are still missing. First, the programmer references functions from libraries that are outside the provided code. The linker needs to find those references and add them into the code. Adding this code changes the location of certain things in the code, and the program needs to know where things are. Therefore, after adding in the things that the code references, the linker also patches in addresses that were previously missing in the code.

These steps change a program written by people in C into one that a machine can understand and execute.

