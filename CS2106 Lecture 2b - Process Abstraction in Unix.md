---
tags: toProcess
course: CS2106
type: lecture
date: 2023-08-30 Wednesday
---

### System Call

- Sys Call =  API to OS 
- Not the same as normal function call, need to switch from user to **kernel mode**
- Different OS have different APIs
- We have libraries to indirecly call system calls (e.g. printf, getpid, write, read...) in our code
- Sys call mechanism:
	- user prog invokes lib call
	- lib call places the sys call number into a designated register
	- TRAP: switch from user to kernel mode and save CPU state
	- Determine appropriate sys call handler, using a Dispatcher
	- Sys call handler is executed (perform task)
	- When sys call handler ended, it restore CPU state, return to lib call, switch from kernel to user mode
	- lib call return to user prog

![[Pasted image 20230903174511.png]]

### Exception 

- execute machine level ins can cause exception
	- arithmetic error
	- memory accessing error
- **synchronous**, occur due to prog execution
- Have to execute an **exception handler**, similar to a forced func call

### Interupt

- external event can interrupt the execution of a prog
- hardware related: timer, mouse movement, key pressed
- **asynchronous**: event is independent of prog execution
- program execution is suspended, have to execute an **interrupt handler**

### Fork

```c
#include <sys/types.h>
#include <unistd.h>

int fork();
```

- Fork creates a new process known as child processs
- Returns either:
	- PID of the newly created process (for parent process)
	- 0 (for child process)
- The child process is a duplicate of the current executable image
	- same code, same address space
	- ! memory in child is a copy of the parent (not shared)
- The child process differs only in:
	- PID
	- Parent's PID
	- `fork()` return value
- Both parent and child processes continue executing after `fork()`
- Use case: execute different tasks using parent/child
- Use the return value of `fork()` to distinguish parent and child.
##### Examples

>[!question]
> What is printed by the end of the program?

```c
int main() {
	printf("one")
	
	fork()
	fork()
	fork()
	
	print("double") // 8 times
	return 0;
}
```

Solution: draw a tree with forks! Keep track of parent and child process. Backtrack whenever we reach return statement!

![[CS2106 Lecture 3 - Process Abstraction in Unix 2023-09-03 17.51.19.excalidraw]]

>[!question]
> What happen if parent and child tries to modify the same variable?

```C
int main() {
	int var = 1234;
	int result = fork();
	if (!result) {
		var++;
		printf("%d", var); // 1235
	} else {
		var--;
		printf("%d", var); // 1233
	}
}
```

- Child copy the entire memory content of parent
- var accessed by each parent and child processes are different vars.

### C command line argument

```C
int main(int argc, char* argv[]) {
	// use argc and argv
}
```

- `argc`: number of command line arguments, including the program name
- `argv`: 
	- An array of string (`char* []`)
	- Each element in `argv[]` is a C character String

Example:

```
$ a.out 123 hello world
```

- argv[0] = "a.out"
- argv[1] = "123"


### execl() System Call

- replace current executing process image w a new one

```C
#include <unistd.h>

int execl(const char *path, const char *arg0, ..., const char *argN, NULL);
```

- `path` : location of the executable
- `arg0...`: command line arguments
- `NULL`: indicate end of arg list
- The exec() functions **return -1 only if an error has occurred**. 

```c
int main() {
	execl("/bin/ls", "ls", "-al", NULL);
}

// equivalent to $ls -al
```

- Replace the current memory content (code, data...) with one of the new program.

### Combining fork() and exec()

- spawn off a child process w `fork()`, then assign it to a task through `exec()`
- meanwhile, parent process is still around to accept a new request

>[!question]
> Are the parent and child processes working asynchronously? or sequentially?

### Master Process

Special initial process:
- *init* process
- created in kernel at boot up time
- PID = 1
- Watches for other processes and respawns where needed
- fork() creates a process tree where *init* is the root process.

![[Pasted image 20230903205517.png]]
### Process Termination

```c
void exit(int status)
```

- `exit(0)`: normal termination
- `exit(!0)`: problematic execution
- does not return (void)
- Some system resources are released on exit (file descriptors), but not all (pid)

Most programs have no explicit exit() call => return from main() implicitly calls exit().

Calling exit on a child process turns it into a **zombie process**.
### Wait/Synchronization

```c
int wait(int *status)
```

Make parent process wait for child process to terminate. It cleans up remainder of the child system resources => kill zombie process.

![[Pasted image 20230830154248.png]]

### Zombie process vs Orphan process

- Zombie: child process terminates before parent but parent did not call `wait` to clear it. Can fill up the process table.
- Orphan: parent process terminates before child process. Init process node becomes pseudo parent of child processes.

### Implementation of fork()

- how to copy parent memory space effciently?
	- Copy on Write: only copy a memory location when it is written to. the remaining memory space is still **shared**
- Linux provides clone() which supersedes fork().

## Summary

>[!Unix Process System Call]
> - `fork()`: process creation
> - `exec()`: change executing program/image
> - `exit()`: process termination (can create zombies)
> - `wait()`: get exit status, synchronize with child (clear zombies)
> - `getpid()`: get process info


## Questions/Cues

---
Links:
