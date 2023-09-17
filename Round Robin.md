- A preemptive version of [[First Come First Served]]
- FIFO queue
- Run first task from queue until 
	- quantum elapsed
	- task gives up CPU / task blocks
- Task is then placed at the end of the queue **if there are other tasks in queue**
- Guarantee response time (**no starvation**): bound by (n - 1)q where q is quantum 
- **Timer interrupt** is needed for scheduler to check on quantum expiry
- Choice of time quantum matters:
	- too big: better cpu utilization but long waiting time
	- too small: big overhead (worse cpu utilization) but short waiting time

![[Pasted image 20230912103115.png]]