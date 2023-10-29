>[!definition]
> - An abstraction for synchronisation mechanism. 
> - Can have different implementations.
> - Provides a way to block a number of processes and a way to wake up one or more sleeping processes.

![[Pasted image 20231015132136.png]]

Conceptually consists of:
- A protected non-negative integer
- A queue of waiting processes
##### Characteristics

A semaphore S contains a **non-negative** integer value.

2 atomic operations can be performed on semephore:
- Wait(S)
- Signal(S)

Wait(S):
- If S <= 0, block the process/thread
- **Else**, decrement S by 1

Signal(S):
- Increment S by 1
- Wakes up any sleeping process (if exist)
- Never blocks (else, cannot wake sleeping processes up)

- - -
[[3 Classical Synchronisation Problems]]