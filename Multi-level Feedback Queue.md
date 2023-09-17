>[!question]
> How do we schedule without perfect knowledge (process behaviour, running time, ...)

- MLFQ is adaptive - it "learns the process behaviour automatically". 
- Minimizes both response time for IO bound behaviour and turnaround time for CPU bound processs.

Basic rule:
1. If Priority(A) > Priority(B) => A runs (**preemptively**)
2. If Priority(A) == Priority(B) => A and B runs in [[Round Robin]]

Changing rule:
1. New job => highest priority
2. If a job fully utilized its time quantum => priority reduced
3. If a job gives up / blocks before finishing its time quantum => priority retained.

### Examples

![[Pasted image 20230912115401.png]]

![[Pasted image 20230912115316.png]]

![[Pasted image 20230912115335.png]]