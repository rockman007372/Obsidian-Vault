---
tags: []
course: CS2106
type: lecture
date: 2023-09-06 Wednesday
---
# Content

## Concurrent Execution

- It is more a logical concept. Even if you have 1 CPU-core, concurrent execution is possible
	- Virtual parallelism: interleaving processes to create illusion of parallism
	- Physical parallelism: multi-cores architecture running processes at the same time.
- multitasking OS:
	- 1 core: timeslice execution of tasks
	- n-core: timeslicing on n cores
- Question: if processes > CPUs, which should be chosen => scheduling problem
- Scheduler: part of OS, makes scheduling decision; each scheduler uses different schedulling algo.
- Process behavior: a typical process goes through phases of:
	- CPU activity: computation; **compute-bound process** spends majority of time here.
	- IO-activity: request and receive services from I/O devices. **IO-bound processes** spends majority of time here.
- Processing environment: 3 types
	- **Batch processing**: no user interaction, no need to be responsive; 
	- **Interactive**: has active user interacting w system; must be responsive, consistent in response time (laptop...)
	- **Real time processing**: has deadline; usually periodic process (embedded system, robots...)
- The goal of any scheduler is to maintain fairness while maximising utilization.
	- **Fairness**: each process gets fair share of CPU time, no **starvation** (long time never processed)
	- **Utilization**: all parts of the computing system must be utilized, else got room for improvement
- When to perform scheduling?
	- **Non-preemptive** (cooperative): process stays scheduled until it blocks or gives up cpu voluntarily
	- **Preemptive**: fixed time quota/process. OS scheduler picks next process to execute.

## Scheduling algorithms


Criteria for evaluation:
- Turnaround time: duration between request submission and process completion (waiting time + execution time).
- Throughput: no. task/time
- CPU utilization: percentage of **time** when CPU is working on a task.

We have different algorithms for different processing environments:
- [[Scheduling for Batch Processing]]
- [[Scheduling for Interactive Environment]]

# Question

1. What does it mean for a process to "block"?
- When a process is waiting for some event to occur / resource to become availble 
- e.g. **I/O operations**

2. Why do we give priority to tasks that block a lot in [[Multi-level Feedback Queue]]?
- task blocks a lot, likely to be IO bound => not cpu intensive, but requires consistent and low response time => higher priority.

3. Waiting time vs response time?
- Waiting time: total time spent in the queue.
- Response time: time waited before first being executed.




