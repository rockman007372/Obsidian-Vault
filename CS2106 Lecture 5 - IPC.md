---
tags: []
course: CS2106
type: lecture
date: 2023-09-20 Wednesday
---
2 types of Inter-Process Communication: 
- Shared memory
- Message Passing

## Shared Memory

Basic idea:
- Process P1 creates a shared memory region M (identified by a unique id)
- Process P1 and P2 attach memory region M to its own memory space (using a pointer)
- P1 and P2 can now communicate using memory region M 
	- M behaves very similar to normal memory region 
	- Any writes to the region are visible to the other processes

![[Pasted image 20231002145948.png]]

Advantage: Efficient (less syscalls, only involve OS in create/attach memory)
Disadvantage: Hard implementation (synchronisation issues)

POSIX api:

```C
// create shared memory region of specific size
// return a unique id
int shmid = shmget(..., size, ... | 0600);

// attach shared memory region, return a pointer
int *shm = shmat(shmid, ...);

// read and write to the memory pointed by the pointer

// detach shm and destroy shmid
shmdt( (char*) shm) 
shmctl(shmid,...)
```

Note:
- detaching the shared memory segment is crucial to avoid memory leaks
- removing the shared memory id is optional. If you remove the shared memory segment, make sure all processes have detached it before removal.
## Message Passing

General idea:
- Process P1 sends a message M through OS
- Process P2 receives the message M from OS
- M has to be stored in kernel memory space
- Every send/receive ops involve a syscall.

Naming scheme: How to identify sender and receiver.
-  Direct: explicitly name the other party, one link per pair
- Indirect: messages sent/received through a mailbox/**port**.

Synchronisation: Behavior of sender/receiver
- Blocking Primitive: `Receive()` is blocked until message arrived
- Non-blocking Primives: receiver can run other codes while waiting for message.

Advantage: Easier implementation + automatic synchronisation
Disadvantage: inefficient (more syscalls + copies of data)

In UNIX, there are 2 message passing mechanisms:
- [[UNIX Pipes]]
- [[UNIX Signals]]

Differences in use case:

- **Pipes**: streaming data between processes. 
- **Signals**: more commonly used for event notification.

# Questions/Cues

- Page 25, 17

