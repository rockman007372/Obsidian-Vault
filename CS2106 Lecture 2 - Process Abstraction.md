---
tags:
  - processed
course: CS2106
type: lecture
date: 2023-08-26 Saturday
---
- recap on assembly code and program execution in memory
- [[Stack Memory]]
- [[Dynamically Allocated Memory (Heap)]]

### Process Management

#### OS Context

- Process (aka Task or Job): a **dynamic abstraction** to describe a running program. Stores info to describe a running program.
- Key topics:
	- Process Abstraction: info of an executing prog
	- Process Scheduling: decide which process is executed
	- Inter-Process Communication and Synchronization: passing info btw processes
	- Alternative to process: light-weight process (threads)
- Processes are differentiated using **process ID** (PID)
- Processes have **process states**: ready, running, not running...
- **Process model state diagram**: describe behaviors of a process through state and transitions

![[Pasted image 20230826160707.png]]

> [!note]
> In CS2106, our CPU has 1 core:
> - <= 1 process in running state
> - conceptually 1 transition at a time

When a program is under execution, there are information to keep track:
- **Memory** context: text, data, stack, heap
- **Hardware** context: GPR, PC, SP, FP...
- **OS** context: process ID, process state...
#### Process Control Block and Process Table

- Process Control Block: stores the entire execution context of a process
- Process Table: stores the PCB of all processes

![[Pasted image 20230826161148.png]]
## Summary

>[!checkpoint]
> When a program is under execution, there are information to keep track:
> - Memory context: text, data, stack, heap
> - Hardware context: GPR, PC, SP, FP...
> - OS context: process ID, process state...


