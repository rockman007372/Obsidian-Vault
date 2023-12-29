---
tags: []
course: CS2106
type: lecture
date: 2023-09-20 Wednesday
---

- Learn about the problem with unsynchronised concurrency.
- **Race condition**: undesirable situation when multiple threads/processes try to **access and modify shared resources** in unsynchronised manner.
	- Shared resources are usually global variables (e.g. a thread hasn't finished writing to a global varible, but another thread already reads it)
- Solution: create a **critical section** (code segment with race condition). Then only allow one process to execute that code at any time.
- Property of correct CS implementation:
	- **Mutually exclusive**: only one process in CS at a time
	- **Bounded-wait**: after process P request, there is an **upper bound** of other processes entering CS before P => No starvation
	- **Progress**: whenever CS is free, a process must enter it.
	- **Independence**: process not in CS should never **block** other processes from entering CS.
- Symptoms of incorrect synchronisation:
	- deadlock: all processes blocked
	- livelock: processes keep changing state to avoid deadlock, but they are not blocked.
	- starvation
- Low-level implementation: [[Test and Set]]
- High Level Implementation: [[Semaphore]]



