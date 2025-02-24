---
tags:
  - toProcess
course: cs3210
type: lecture
date: 2024-08-24 Saturday
---

## Notes

Topics:
- Background
- Architecture
- Models
- Performance and scalability

3 main steps to parallelize:
1. Decomposition: break down sequential tasks 
2.  Scheduling: schedule these tasks on parallel threads/processes
3. Mapping of processes/threads to physical processing units

Process: an instance of a program **in execution**
- Identified by PID
- Can be created more than the no. cores
- Program counter (PC): executable program ins?
- stack and heap
- registers (GPRs and Special)
- Each process own exclusive address space ⇒ exclusive access to data

Memory of process:
- Text: ins of program
- Data: global variables
- Stack: grows up, store function call info (arguments...)
- Heap: grows down, stores dynamic data

Context-switch: switch between processes (OS needs to swap all pointers pointing to another process)
- overhead: states of suspended processes saved
- 2 types of execution: time slicing (concurrent) vs parallel execution of diff resources

Creating another process does not copy memory until any processs write to memory.

Inter-process Communication (IPC): avail in os
- Shared memory: protect share/write with locks
- Message passing: blocking vs non-blocking, synchronous vs asynchronous
- Pipes and Signal (Unix specific)

Exceptions vs Interrupts:
- exception is synchronous while interrupts are asynchronous (independent from program execution: user clicks sth)
- exception handler vs interrupt handler

Thread:
- a process can contain multiple threads
- a sequential execution stream with a process (with its own pc, stack pointer, registers)
- threads share address space of process ⇒ shared-memory architection

##### Synchronisation

Data race vs race condition
- Data race: 2 thread access a shared resource without any portection AND at least one thread modifies the resource
- Race condition: different interleaving of thread executions, may (but not always) cause bug/unintended effects

Mechanisms:
- Locks: 
- Semaphores: 
- Monitors: 

Locks:
- Acquire and release operations
- Can be a spinlock (?) or mutex

Semaphore:
- atomic counters
- Wait or P: decrement counter, block until counter >= 0
- Signal or V: increment, wake up a thread to enter
- Mutex semaphore: 0 or 1
- Counting semaphore: multiple thread can pass the semaphore

Drawback of semaphore:
- global variable
- independent from data being controlled (unlike mutex)

Barrier:
- implemented by semaphore
- continue the program once all threads reach the barrier

##### Synchronisation problems

Deadlock: 
- Circular wait: cyclic dependency
- Mutual exclusion: at least one resource held in a non-shareable mode
- Hold and wait: one process hold resource while waiting for another resource
- No pre-emption: critical sections cannot be aborted externally

Starvation: 
- thread/process cannot make progress because some other thread/process has the resources it requires ⇒ side effect of scheduling algo 

Livelock:
- no progress despite processes constantly changing states

[[3 Classical Synchronisation Problems]]:
- Producer-consumer
- Reader-writer
- Dining philosopher




## Summary

## Questions/Cues

1. Can we switch the order of turnstile and roomEmpty (page 65)
2. Reader-writer with priority?
3. What are monitors?
	1. High-level abstract data type that provide mutual exclusion within itself without explicit programmer's instruction ⇒ eliminate the need for complex synchronization primitives such as semaphores and locks.
	2.  Components: 
		1. a mutex
		2. a conditional variable 
		3. a condition to wait for
	3. Using condition variables, threads examine conditions and wait for the conditions to become true. When a modification to the shared resource transforms the condition into true and frees up waiting threads, signaling or notification takes place.