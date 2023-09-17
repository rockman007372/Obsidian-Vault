
- Criteria:
	- response time: time btw request and response by system should be low
	- predictability: consistent in response time
	- Hence, **preemptive** scheduling algo are predominant
- Timer Interrupt: Interrupt that goes off periodically based on hardware clock
	- Timer interrupt cannot be intercepted by any other program
	- **OS scheduler** is invoked on every timer interrupt
- Interval of Timer Interrupt (ITI)
	- typical values = (1ms - 10ms)
	- If too short: processes keep being interupted
	- If too large: cannot preempt the current process => high response time
- Time Quantum: 
	- execution duration given to a process
	- ! must be a multiple of ITI (else process ends before/after scheduler is invoked, dont know which task to execute next)
	- Once time quantum passes, switch to a diff process

![[Pasted image 20230911155222.png]]

#### Algorithms for interactive environment

- [[Round Robin]]
- [[Priority Scheduling]]
- [[Multi-level Feedback Queue]]
- [[Lottery Scheduling]]