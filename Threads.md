
Motivation:
- Process creation is expensive: the whole memory space + process context are duplicated.
- ? Communication btw processes is difficult due to independent memory, require IPC 
- As much as possible, we want to avoid system calls (waste cyles?)

Basic idea:
- Traditionally, each process has a single thread of control => execute 1 instruction of the program at any time
- Add more threads to the same process => multiple instructions of the program are executed at the same time (concurrently to gives illusion of parallelism)

There is only one PC register in a CPU core. 
- In single-threaded processes,  the PC is loaded with different values through process context switch. 

![[Pasted image 20230918110817.png]]

- However, in multi-threaded processes, each thread has its own PC counter value.

![[Pasted image 20230918110851.png]]

Context switching in multi-threads is done within the same process, while context switching between processes is done by the kernel.


What can we share btw threads? 
- Memory Context: text, data, heap (e.g. global variables)
- OS Context: Process id, other resources like file

Unique information of each thread: 
- thread_id 
- Hardware context:
	- **registers** (values in the registers)
	- stack (FP and SP)

Illustration of single-threaded process vs multi-threaded processes:

![[Pasted image 20230916144237.png]]

>[!note]
> Threading is usually preferred over forking.


Process context switch vs thread switch:
- Switching btw processes: **memory, hardware, os context** are saved and restored.
- Switching threads: only save and restore **hardware context**: registers + stack (through FP and SP registers).
- Hence, threads are just "light-weight" processes.

Problems of threads:
- Multiple threads can read and write over each other in the memory => incorrect result
- Make process operation more complex (what happen to the threads when we call fork, exec, exit on the process?)