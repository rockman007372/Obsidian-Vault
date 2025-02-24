
[[User Thread vs Kernel Thread vs Hybrid]]

### User Thread

Threads implemented as a **user library** => a runtime system in the process will handle thread-related operations.

Kernel is **not aware of the threads** in the process => only schedule processes.

![[Pasted image 20230918111538.png]]

Advantages:
- Any program on ANY OS can be multi-threaded
- Thread operations are just library calls => faster than system calls
- Configurable: customize thread scheduling policy

Disadvantages:
- OS not aware of threads => one thread blocked = whole process blocked => all threads blocked by OS.
- Cannot exploit multiple CPUs to run threads.

### Kernel Thread

- Thread implemented in the OS. Operations are handled by system calls.
- Hence, OS can schedule threads instead of processes (Threads are treated as processes/tasks)
- Kernel may use threads for its own execution.

![[Pasted image 20230918111913.png]]

Advantages:
- Make use of multiple CPUs to run threads (parallelization)

Disadvantages:
- Threads are system calls => defeat the purpose of replacing processes with threads
- Less flexible: may have **too many or too few features** depending on which program is executed.

### Hybrid Thread Model

![[Pasted image 20230918112149.png]]

- A user thread can bind to a kernel thread.
- Can be 1:1, M:1 or M:N 
- Kernel threads allow for multi-threading in parallel (in different CPU cores)
- User threads allow flexible customization (more or less multi-threading)