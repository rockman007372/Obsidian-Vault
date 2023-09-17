- Assign a priority value to all tasks
- Select tasks with highest priority value using PQ
- Can starve: keep queuing high priority tasks
	- Possible solutiona: 
		- decrease priority after each quantum
		- give current process a time quantum

>[!note]
> Generally hard to guarantee or control the exact amout of CPU time using priority.

- Can lead to **priorty inversion**:
	- PQ = {A = 1, B = 3, C = 5}
	- C starts first and locks a resource (eg. file)
	- B preempts C, hence C is unable to unlock resource
	- A arrives and wants to preempt B, yet the **resouce is not available**
	- B continues execution