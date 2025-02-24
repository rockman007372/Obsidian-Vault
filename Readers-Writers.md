## Problem

![[Pasted image 20231015121937.png]]

- Writer must have exclusive access to D.
- Readers can read with other readers.
- Readers cannot read while a writer is writing and vice versa.

##  Semaphore solution

Big idea:
- `roomEmpty` semphore initialised to 1. 
- There can be at most one writer modifying the data. When the writer writes, it decrement `roomEmpty` to 0.
- There can be multiple readers reading data at once. The first reader decrement `roomEmpty` to 0 and the remaining readers concurrently read the data. Once the last reader finishes reading, it increments `roomEmpty` back to 1.

Problem: Violation of bounded-wait for writer (starvation)
- If more readers keep reading, writers can never write.

```C
// Writer
while (TRUE) { 
	wait( roomEmpty ); 
	Modifies data; 
	signal( roomEmpty ); // signal to other writers and readers
}
```

```C
// Reader
while (TRUE) { 
	// first reader checks if room is empty
	wait( mutex ); 
	nReader++; 
	if (nReader == 1) 
		wait( roomEmpty ); 
	signal( mutex ); 
	
	Reads data; 
	
	// last reader signals the room is empty
	wait( mutex ); 
	nReader--; 
	if (nReader == 0) 
		signal( roomEmpty ); 
	signal( mutex ); 
}
```

Starvation-free solution:
- Use a turnstile to force new readers to wait whenever a writer appear.
- Turnstile is a semaphore with value 1 (mutex-ish)

```C
// Writer
while (TRUE) { 
	wait( turnstile ) // decrement turnstile, diallowing new readers
	wait( roomEmpty ); 
	Modifies data; 
	signal( turnstile ) // allowing new readers to resume
	signal( roomEmpty ); 
}
```

```C
// Reader
while (TRUE) {
	// prevents starvation
	wait( turnstile )
	signal( turnstile )
	
	// first reader checks if room is empty
	wait( mutex ); 
	nReader++; 
	if (nReader == 1) 
		wait( roomEmpty ); 
	signal( mutex ); 
	
	Reads data; 
	
	// last reader signals the room is empty
	wait( mutex ); 
	nReader--; 
	if (nReader == 0) 
		signal( roomEmpty ); 
	signal( mutex ); 
}
```

## Monitor solution

```java
int numReader, numWriter; Object object;

void writeFile() {

    synchronized (object) {
        while (numReader > 0 || numWriter > 0)
            object.wait();

        numWriter = 1; 
        
	    // write to file;
	    
		numWriter = 0;
		object.notifyAll();
    }
}

void readFile() {

	 synchronized (object) {
        while (numWriter > 0)
            object.wait();

        numReader++;
    }

    // read from file;
    synchronized (object) {
        numReader--;
        object.notify();
    }

}
```