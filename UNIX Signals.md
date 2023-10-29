Signal is a IPC mechanism.

Signals are **asynchronous notification** sent to a process or to a specific thread within a process, notifying it that a **particular event** has occurred.


The recipient of the signal must handle it by:
- Default handlers
- User-supplied handlers (**only applicable to some signals**)

Common signals:
- Kill
- Interrupt
- Stop
- Continue
- Memory Error...


```C
void myOwnHandler( int signo ) { 
	if (signo == SIGSEGV) { 
		printf("Memory access blows up!\n"); 
		exit(1); 
	} 
	
} int main() { 
	int *ip = NULL; 
	
	// assign user-defined handler
	if (signal(SIGSEGV, myOwnHandler) == SIG_ERR) 
		printf("Failed to register handler\n"); 
		
	*ip = 123; // sends a Memory Segmentation Fault signal
	return 0; 
}
```