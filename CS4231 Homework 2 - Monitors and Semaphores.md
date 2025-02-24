---
tags:
  - toProcess
course: CS4231
type: assignment
date: 2025-02-05 Wednesday
---
### Question 1
Give a starvation-free solution to readers-writers problem using Java-style monitors.

Big idea:
- some sort of maximum readers allowed? when quota is reached, must finish reading and notify a writer.
- perhaps use another object?

Attempt:

```java
Object object;
Object readerObject;

void writeFile() {

    synchronized (object) {
        while (numReader > 0 || numWriter > 0)
            object.wait();

        numWriter = 1;
    }

    // write to file;

    synchronized (object) {
        numWriter = 0;
        object.notifyAll();
    }
}


void readFile() {

	synchronized (object) {
		while (numWriter >= maxReaderAllowed)
			readerObject.wait() // WRONG CONCEPT! Must obtain lock in obj before wait
			
        while (numWriter > 0)
            object.wait();
            
        numReader++;
    }
    
    // read from file

    synchronized (object) {
        numReader--;
        object.notify(); // notify writer?
        readerObj.notify(); // then notify any waiting reader?
    }
}
```

=> Starvation can still occur! If readers keep coming in, writer will always have to wait!!

Attempt 2: 
- If there is a writer writing or any writer waiting to write, any subsequent readers have to wait until the writer finishes.
- What if new writers keep coming in? Would readers now starve?

Solution
```java
Object object;
int numWaitingWriter;
int numWriter;
int numReader;

void writeFile() {
	synchronized (object) {
		waitingWriter++;
		while (numReader > 0 || numWriter > 0)
            object.wait();
        waitingWriter--;
        
        numWriter = 1
     
	    // write to file;
	    
        numWriter = 0;
        object.notifyAll();
	}
}

void readFile() {

	synchronized (object) {
        while (numWaitingWriter > 0 && numWriter > 0)
            object.wait();
            
        numReader++;
    }
    
    // read from file

    synchronized (object) {
        numReader--;
        object.notify(); // notify writer?
    }
}


```

Solution:
- maintain an explicit queue. Each monitor queue has at most one element.


### Question 2

Give a solution to the following synchronization problem , using Java-style monitors:
- There are 3 processes (P, Q, and R). Process P repeatedly prints “P”, process Q repeatedly prints “Q”, and process “R” repeatedly prints “R”.
- The number of “R” printed should always be less than or equal to the sum of the numbers of “P” and “Q” printed (`Rs <= Ps + Qs`)

```java

Object objR;

int R = 0;
int P = 0;
int Q = 0;

printR() {
	synchronized(objR) {
		while (R >= P + Q) {
			objR.wait();	
		}
	}
	print(R);
	R++;
}

printP() {
	print(P);
	
	synchronized(objR) {
		P++;
		objR.notify();
	}
}

printQ() {
	print(Q);
	
	synchronized(objR) {
		Q++;
		objR.notify();
	}
}

```

### Question 3

Given a solution to the following **sleeping barber** problem, using Java-style monitors:

- There is a process called barber. The barber does haircut for any waiting customer. If there is no customer, the barber goes to sleep.
- There are multiple processes each called a customer. **A customer waits for the barber if there is any chair left in the barber shop**. Otherwise the customer leaves immediately. If there is an available chair, the customer occupies it. If the barber is sleeping, the customer wakes up the barber. There are total n chairs in the barber shop.
- You should write out the pseudo-code for the barber process and the customer processes.

```Java
int customers = 0;
int chairs = n;
Object queue;

void barber() {
	while (true) {
		synchronized(queue) {
			if (queue.isEmpty()) {
				queue.wait();
			}
			
			Customer c = queue.pop();
		} 
		
	}
}

void customer() {

	synchronized(chairs) {
		if (chairs == 0) {
			return; // leave
		}
		chairs--;
	}
	
	Customer c = new Customer();
	c.done = false;
	synchronized(queue) {
		queue.add(c);
		queue.notify();
	} 

	synchronized(c) {
		if (!c.done) {
			c.wait(); // no need while loop
		}
	}

	synchronized(chairs) {
		chairs++;
	}
}
```
