---
tags: []
course: CS2106
type: lecture
date: 2023-08-30 Wednesday
---
### C command line argument

```C
int main(int argc, char* argv[]) {
	// use argc and argv
	int i; 
	for (i = 0; i < argc; i++) { 
		printf("Arg %i: %s\n",i, argv[i] ); 
	} 
	return 0;
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
### Fork

```c
#include <sys/types.h>
#include <unistd.h>

int fork();
```

- Fork creates a new process known as child process.
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

Solution: 
- Draw a fork tree! Keep track of parent and child process. Backtrack whenever we reach return statement! 
- Total number of processes $= 2^{n} = 2^{3}= 8$

![[CS2106 Lecture 3 - Process Abstraction in Unix 2023-09-03 17.51.19.excalidraw]]

>[!question]
> What happen if parent and child tries to modify the same variable?

```C
int main() {
	int var = 1234;
	int result = fork();
	if (!result) { // parent
		var++;
		printf("%d", var); // 1235
	} else { // child
		var--;
		printf("%d", var); // 1233
	}
}
```

- Child copy the entire memory content of parent
- var accessed by each parent and child processes are different vars.
### execl() System Call

- replace current executing **process image** with a new one.
	- Only code replacement.
	- PID and other information (?) still intact.

```C
#include <unistd.h>

int execl(
	const char *path, 
	const char *arg0, ..., const char *argN, 
	NULL
);
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
- ! IMPORTANT: after execl, process will never return the previous process image (in other words, code after **a successful execl()** will never be executed).

### Combining fork() and exec()

- spawn off a child process w `fork()`, then assign it to a task through `exec()`
- meanwhile, parent process is still around to accept a new request

>[!question]
> Are the parent and child processes working asynchronously? or sequentially?
> Ans: dependent on number of cores.

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
- Most programs have no explicit exit() call => return from main() implicitly calls exit().
- Calling exit on a child process turns it into a **zombie process** if the parent process **does not call wait**.
### Wait/Synchronization


```c
int wait(int *status)
```

Signature:
- Returns the PID of the terminated child process.
- Status is a **pointer** that stores exit status of the terminated child process. Can sometimes be used to retrieve function's return values.

Usage:
- Make parent process wait for **any** child process to terminate. It cleans up remainder of the child system resources => **kill zombie process**.

![[Pasted image 20230830154248.png]]

### Zombie process vs Orphan process

- Zombie: child process terminates before parent but parent did not call `wait` to clear it. Can fill up the process table.
- Orphan: parent process terminates before child process. Init process node becomes pseudo parent of child processes.

Why do zombie processes exist?
- Without the zombie process, we cannot return information about the terminated child to its parents.
- Hence it aids the implementation of `wait()`

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
