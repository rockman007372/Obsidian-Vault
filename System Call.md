
- Sys Call =  API to OS kernel.
- Calling facilities/services in kernel
- Not the same as normal function call, need to switch from user to **kernel mode**
- Different OS have different APIs
- We can use library calls (e.g. printf, getpid....) to indirectly call system calls (e.g. write, getpid,....) in our code.
- Sys call mechanism:
	1. User prog invokes lib call.
	2. Lib call places the sys call number into a designated register.
	3. TRAP: switch from user to kernel mode and save CPU state.
	4. A dispatcher determine an appropriate **system call handler**.
	5. ! Sys call handler executes task.
	6. Once done, sys call handler restores CPU state, returns to lib call, switches from kernel to user mode.
	7. Lib call return to user prog.

![[Pasted image 20230903174511.png]]