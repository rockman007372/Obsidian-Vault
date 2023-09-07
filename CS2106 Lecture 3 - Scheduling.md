---
tags:
  - toProcess
course: CS2106
type: lecture
date: 2023-09-06 Wednesday
---

## Notes

### Concurrent Execution

- It is more a logical concept. Even if you have 1 CPU-core, concurrent execution is possible
	- Virtual parallelism: interleaving processes to create illusion of parallism
	- Physical parallelism: multi-cores architecture running processes at the same time.
- multitasking OS:
	- 1 core: timeslice execution of tasks
	- n-core: timeslicing on n cores
- Question: if processes > CPUs, which should be chosen => scheduing problem
- Scheduler: part of OS, makes scheduling decision; each scheduler uses different schedulling algo.
- Process behavior: a typical process goes through phases of:
	- CPU activity: computation; **compute-bound process** spends majority of time here.
	- IO-activity: request and receive services from I/O devices. **IO-bound processes** spends majority of time here.
- Processing environment: 3 types
	- Batch processing: no user interaction, no need to be responsive; 
	- Interactive: has active user interacting w system; must be responsive, consistent in response time (laptop...)
	- Real time processing: has deadline; usually periodic process (embedded system, robots...)
- Criteria/metrics to evaluate scheduling algo
	- Fairness: each process gets fair share of CPU time, no **starvation** (long time no processed)
	- Utilization: all parts of the computing system must be utilized, else got room for improvement
- When to perform scheduling?
	- Non-preemptive (cooperative): process stays scheduled until it blocks or gives up cpu voluntarily
	- Preemptive: fixed time quota/process. OS picks next process to execute.
- Criteria for batch processing:
	- Turnaround time: total time taken (waiting time + execution time)
	- Throughput: no. task/time
	- CPU utilization: percentage of **time** when CPU is working on a task.

### Algorithm for batch processing

- First Come First Serve (FCFS): FIFO queue
	- Guarantee **no starvation**: once u enter the queue, u will eventually get scheduled (no. tasks before it strictly decreases)
	- Average waiting time is high if random order => reordering in ascending order to minimize wait time.
	- Convoy effect:
		- Queue = `[A, x, x, x, x...]`, where A is CPU bound, x is IO bound
		- A takes a long time in CPU, I/O is idle
		- Once A finishes, it transits to I/O
		- x takes very little time in CPU, then transits to I/O too
		- Now CPU is idle
- Shortest-Job-First:
	- How to guess future CPU time by the previous CPU bound phases?
	- ! Exponential Average
- Shortest Remaining Time (SRT)
	- Premptive: when a new job comes, if the new job has a smaller remaining time, replace the current job with new job
	- Starvation: if we keep queuing short jobs with short remaining time, longer jobs will never get executed.

### Interactive environment

- criteria:
	- response time: time btw request and response by system
	- predictability: consistent in response time
- Hence, preemptive scheduling algo are used to ensure good response time.
- Timer Interrupt: OS scheduler is invoked on every timer interrupt
- Interval of Timer Interrupt (ITI)
	- typical values = (1ms - 10ms)
	- If too short, processes keep being interuptted
	- If too large: cannot preempt the current process => high response time
- Time Quantum: 
	- execution duration given to a process
	- ! must be a multiple of ITI
	- Once time quantum passes, switch to a diff process
#### Algorithms for interactivce environment

- Round Robin:
	- FIFO queue
	- Run first task from queue until quantum elapsed/task gives up CPU/task blocks
	- Task is then placed at the end of the queue **if there are other tasks in queue**
	- Guarantee response time: bound by (n - 1)q where q is quantum
- Priority Scheduling:
	- Assign a priority value to all tasks
	- Select tasks with highest priority value using PQ?
	- Can starve: keep queuing high priority tasks
		- Solution: decrease priority after each quantum
- 




## Summary

## Questions/Cues

