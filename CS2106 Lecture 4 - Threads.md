---
tags:
  - toProcess
course: CS2106
type: lecture
date: 2023-09-16 Saturday
---

## Threads

Motivation for thread:
- process is expensive: 
	- whenever you create a new process, the whole memory space + process context are duplicated.  
	- duplication is actually conceptual (we only copy on write). but still expensive
- Communication btw processes is difficult, require IPC table?
- As much as possible, we want to avoid system calls (waste cyles?)

Thread was invented to overcome process model problems.

Basic idea:
- Traditionally, each process has a single thread of control => execute 1 instruction of the prog at any time
- Add more threads to the same process => multiple instructions of the prog is executed at the same time conceptually

Whenever we fork(), what happens to the program counter (PC)? There is only one PC, but it is loaded with different values through process context switch.

key difference btw fork() and multi-threading: context switching in multi-threads is done within the same process.

Process vs thread?
- a singel process can have multiple threads
- what can we share btw threads? the same memory space, including global and local variables...
- Unique information of each thread: 
	- thread_id 
	- **registers** (why? register values not shared btw functions)
	- stack (FP and SP)

Illustration of single-threaded process vs multi-threaded processes:

![[Pasted image 20230916144237.png]]

Threading is usually preferred over forking.

Every chrome tab is a process, not a thread. Hence too many tabs => slow af

Process context switch vs thread switch:
- Switching btw processes: memory, hardware, os context are saved and restored.
- Switching threads: only save and restore **hardware context**: registers + stack (just FP and SP registers).

Threads are just "light-weight" processes.

Problems of threads:
- Multiple threads can write over each other in the memory
- Make process operation more complex (what happen to the threads when we call fork, exec, exit on the process?)

## Thread Models

User Thread vs Kernel Thread vs Hybrid 

## POSIX threads - thread API









