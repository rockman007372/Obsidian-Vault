---
tags:
  - toProcess
course: CS3211
type: lecture
date: 2024-01-30 Tuesday
---

## Notes

- True concurrency (multiple CPUs) vs Illusion of concurrency (Task switching on one CPU)
- Exceptions vs Interrupts
	- Exception: synchronous, caused when executing machine level ins
	- Interrupts: asynchronous, caused by hardware-related event (mouse movement, keyboard presses)
	- Both have to execute handlers.
- [[Processes vs Threads]]:
	- A process traditionally has one thread. A thread defines the sequential execution stream within a process, through hardware contexts (PC, registers, SP)
	- Threads share the address space of the process (virtual mem?) - it can access shared code, data, heap and OS resources like files. Meanwhile, processes have independent memory space.
	- Threads are like light-weight processs. Less costly to create and terminate. Easier to communicate with each other since they share memory.
- Race condition: situation where multiple threads/programs access shared resources at the same time
- Critical section: code sequence that have mutual exclusion property.
- Critical section requirements:
	- Mutual Exclusion: only one can access at a time
	- Bounded-Waiting: no starvation, any thread waiting to enter will eventually enter
	- Progress: If some thread is not in CS, it should not prevent others from entering
	- Performance: the overhead of entering and leaving CS should be small compared to the work being done.
- Rule of thumb when designing concurrent algo: safety > liveliness
	- safety: nothing bad happens
	- liveliness: good things (progress, bounded-wait)
- Basic mechanisms:
	- Locks
	- Semaphores
	- Monitors?
	- Messages?
- Conditions for deadlock: occur if and only if these 4 conditions happen simultaneously:
	- Mutual exclusion
	- Hold-and-wait: a thread holds on a resource while waiting for another resources
	- No pre-emption
	- Circular wait: `P1 < P2 < P3 < P1`
- Starvation: side-effect of scheduling algo
	- high priority process/threads always access resources before low priority processes
	- one threads always beat another when acquring a lock
- [[Livelock]]: a thread/process keeps switching state to not block each other, but by doing so continue to block each other?
- 2 types of parallelism:
	- Task parallelism: do same work faster
	- Data parallelism: do more work in the same amt of time ⇒ distributed system
## Summary

## Questions/Cues

