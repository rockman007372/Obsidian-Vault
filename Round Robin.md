- A preemptive version of [[First Come First Served]]
- FIFO queue
- Run first task from queue until 
	- quantum elapsed
	- task gives up CPU voluntarily / task blocks 
- Task is then placed at the end of the queue **if there are other tasks in queue**
- Guarantee response time (**no starvation**): bound by (n - 1)q where q is quantum 
- **Timer interrupt** is needed for scheduler to check on quantum expiry

![[Pasted image 20230912103115.png]]

## Comparison between Round Robin and FIFO

RR performs better than FIFO with the right time quantum, because it can **reduce the waiting time** for a task to receive CPU time (no need to wait for long processes to finish).

However, too short time quantum hurts RR performance compared to FIFO.
- Reduce throughput: high overhead of context-switching by CPU, fewer processes finished per unit time.
- Increase average turnaround time (time between request and finish).

When time quantum is too big, RR is no different from FIFO .