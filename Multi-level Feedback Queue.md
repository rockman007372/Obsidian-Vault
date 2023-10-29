>[!question]
> How do we schedule without perfect knowledge (process behaviour, running time, ...)

- MLFQ is adaptive - it "learns the process behaviour automatically". 
- Minimizes both response time for IO bound behaviour and turnaround time for CPU bound processs.

Basic rule:
1. If Priority(A) > Priority(B) => A runs (APPARENTLY **NOT PREEMPTIVE** ANYMORE)
2. If Priority(A) == Priority(B) => A and B runs in [[Round Robin]]

Changing rule:
1. New job => highest priority
2. If a job fully utilized its time quantum => priority reduced
3. If a job gives up / blocks before finishing its time quantum => priority retained.

### Examples

If 1 job is being processed, it goes down the priority queues as it continuously exhausts its quantum. At the lowest PQ, there is no other jobs, hence it continues running until finishing.

![[Pasted image 20230912115401.png]]

If another job arrives, it will be given the highest priority and preempt the current lower priority job.

![[Pasted image 20230912115316.png]]

Below is the case where a CPU-bound job (in Q0) and a IO-bound job (in Q2) are processed concurrently. CPU-bound job is processed in CPU most of the time, but will be preempted(?) by IO-bound job whenever it needs processing. This interleaving of execution maximizes utilization of both CPU and I/O.

![[Pasted image 20230912115335.png]]

### Weaknesses

It is possible to abuse the algorithm through 2 behaviors:
- Change-of-heart: a process has a CPU-intensive phase, followed by a IO-intensive phase => process cannot move up in priority when in IO phase.
- Gaming-the-system: a process repeatedly gives up CPU just before its quantum expires => process is CPU intensive, yet always stay in the highest priority queue.

Solution (in above order):
- Timely-boost: periodically boost priority for processes
- Accounting-matter: accumulate all CPU runtime. Once total runtime exceeds a quantum, reduce priority.