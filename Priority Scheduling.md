- Assign a priority value to all tasks
- Select tasks with highest priority value using PQ
- May or may not be preemptive.
- Can starve: keep queuing high priority tasks
	- Possible solutions: 
		- decrease priority after each quantum
		- give current process a time quantum

>[!note]
> Generally hard to guarantee or control the exact amout of CPU time using priority.



- Can lead to **priorty inversion**:
	- PQ = {A = 1, B = 3, C = 5}, in descending priorities
	- C starts first and locks a resource (eg. file)
	- B preempts C, hence C is unable to unlock resource
	- A arrives and wants to preempt B, yet the **resource is not available**
	- B continues execution despite lower priority (inversion).

>[!definition]
>Priority Inversion: when low-priority task holds a resource needed by a high-priority task. This situation can lead to unexpected delays in the execution of the high-priority task.