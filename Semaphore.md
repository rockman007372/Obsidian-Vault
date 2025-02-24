#### Definition

- An abstraction for synchronisation mechanism. 
- Can have different implementations.
- Provides a way to block a number of processes and a way to wake up one or more sleeping processes.
- Conceptually consists of:
	- A protected non-negative integer
	- A queue of waiting processes

![[Pasted image 20231015132136.png]]
#### Characteristics

A semaphore S contains a **non-negative** integer value.

2 atomic operations can be performed on semephore:
- Wait(S)
- Signal(S)

| Wait(S) | Signal(S) |
| ---- | ---- |
| If S <= 0, block the process/thread.<br><br>**Else**, decrement S by 1. | Increment S by 1.<br><br>Wakes up any sleeping process (if exist).<br> |


- - -
[[3 Classical Synchronisation Problems]]