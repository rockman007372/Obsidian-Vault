
- Process (aka Task or Job): a **dynamic abstraction** to describe a running program. Stores info to describe a running program.
- Processes are differentiated using **process ID** (PID)
- Processes have **process states**: ready, running, not running...
- **Process model state diagram**: describe behaviors of a process through state and transitions

![[Pasted image 20230826160707.png]]

Some important states:
- Ready: Process is waiting to run (picked by scheduler)
- Running: Proces is running in CPU
- Blocked: Process is waiting for an event, cannot be executed/scheduled

This is the equivalent queuing model of the 5-state transition above:

![[Pasted image 20231001133623.png]]

---
See also: [[Process (Networking)]]