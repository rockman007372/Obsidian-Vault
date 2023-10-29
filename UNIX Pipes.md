## Introduction

A process in UNIX has 3 default communication channels:
- stdin: usually keyboard input
- stdout: usually terminal
- stderr: usually terminal, print error message

![[Pasted image 20231002151810.png]]

In a shell terminal, you can pipe the output of one program to the input of another program using `|`:

```
./program-A | ./program-B
```

![[Pasted image 20231002151956.png]]

Shell pipes are built on top of a UNIX IPC mechanism known as **UNIX pipe.**

## UNIX Pipes

![[Pasted image 20231002152230.png]]

- Set up a pipe between 2 processes.
- FIFO behavior: must access data in order.
- Circular-bounded byte buffer: the pipe has fixed size, oldest data is overwritten
- **Implicit synchronisation**: Writer waits when buffer is full and reader waits when buffer is empty => can be used to implement mutex
- Can be half-duplex or full-duplex (bidirectional data)

```C
// make an array into a pipe
int pipe(int fd[]); 
// fd[0] == read end
// fd[1] == write end
```

```C
#define READ_END 0 
#define WRITE_END 1 

int main() { 
	int pipeFd[2], pid, len; 
	char buf[100], *str = "Hello There!"; 
	
	pipe( pipeFd ); 
	
	if ((pid = fork()) > 0) { /* parent */ 
		close(pipeFd[READ_END]); 
		write(pipeFd[WRITE_END], str, strlen(str)+1); 
		close(pipeFd[WRITE_END]); 
	} else { /* child */ 
		close(pipeFd[WRITE_END]); 
		read(pipeFd[READ_END], buf, sizeof(buf)); 
		printf("Proc %d read: %s\n", pid, buf); 
		close(pipeFd[READ_END]); 
	} 
}
```

Notice:
- Must close read/write ends when not in use.

### dup() and dup2()

It is possible to change the standard communication channels of processes to one end of the pipes using `dup()` and `dup2()`.

Signature:

```C
int dup2(int oldfd, int newfd);
```

Parameters:
- `oldfd`: the file descriptor you want to duplicate
- `newfd`: the file descriptor you want `oldfd` to duplicate to.

Usage:
- The new file descriptor will refer to the same file/channel as the old file descriptor.

Example:

```C
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <sys/wait.h>
#include <fcntl.h>

int main() {

    // your program should do the equivalent of 
    // ./slow 5 | talk > results.out
    // WITHOUT using | and > from the shell.

    int p[2];
    int READ = 0;
    int WRITE = 1;

    if (pipe(p) < 0)
        perror("pipe error");
        
    // parent
    if (fork() > 0) {
        close(p[READ]);
        // redirect output to write end of pipe
        dup2(p[WRITE], STDOUT_FILENO);
        close(p[WRITE]);

        // exec slow()
        execl("./slow", "slow", "5", NULL);
        
    // child
    } else {
        close(p[WRITE]);
        // redirect input to read end of pipe
        dup2(p[READ], STDIN_FILENO);
        // write to results.out
        int fp_out = open("./results.out", O_CREAT | O_WRONLY, 0644);
        dup2(fp_out, STDOUT_FILENO);
        close(p[READ]); // why do we close first?
        
        // exec talk()
        execl("./talk", "talk", NULL);
    }
}
```
