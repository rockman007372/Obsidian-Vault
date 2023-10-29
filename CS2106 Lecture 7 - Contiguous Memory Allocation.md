---
tags:
  - toProcess
course: CS2106
type: lecture
date: 2023-10-24 Tuesday
---

## Revision

- Revise [[Memory Organization In MIPS]]
- Contiguous memory region: an interval of consecutive addresses.
- We organise memory in a hierarchy to maximises size, speed and cost savings
- Why Chrome's tab are processes? If tabs are threads in the same process, threads can access each other memory => security reason
- OS handles these memory related tasks:
	- Allocate memory space to new process
	- Manage memory space for process
	- Protect memory space of process from each other
	- Provides memory related system calls to process
	- Manage memory space for internal use (OS is just another program)

## Memory Abstraction

- Processes should not store the actual hardware address to read/write (concurrency/synchronisation issues + security issues of reading and writing to the same memory space )
- Instead, it should store some logical address that maps to a physical address. 
- Each process has a self-contained, independent **logical** memory space (code, data, heap, stack).
- We explore a simple solution using **base** and **limit** registers.
	- Load the starting address of the process into the base register (at run time).
	- Load the range of the memory space into the limit register. 
	- Actual physical address = base + logical address.
	- If actual > limit, invalid read.

## Contiguous Memory Management

If we were to store the processes contiguously in memory, we can partition them in 2 ways:
- [[Fixed-size partition]]
- [[Dynamic partition]]








