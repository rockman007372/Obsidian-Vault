##### Problem

![[Pasted image 20231015134224.png]]

5 philosophers seated ard a table.
- There is a single chopsticks between each pair of philosopher. 5 in total.
- When anyone wants to eat, must pickup both left and right chopsticks.
##### Solution

Big idea:
- Whenever the person to your left and right are not eating, pick up the chopsticks and eat.
	- Else, wait until them **both** are not eating.
- Whenever you finish eating, signal your left and right.

Implementation: 
- each person has a state and a semaphore.
- state represents current state of philosopher (thinking, hungy, eating).
- semaphore allow philosopher to wait for chopsticks and signal to one another they have finished using the chopsticks.

![[Pasted image 20231015134627.png]]

```C
#define N 5 
#define LEFT ((i+N-1) % N) 
#define RIGHT ((i+1) % N) 

#define THINKING 0 
#define HUNGRY 1 
#define EATING 2 

int state[N]; 
Semaphore mutex = 1; 
Semaphore s[N]; // all initialised to 0
void philosopher( int i ) { 
	while (TRUE) { 
		Think( ); 
		takeChpStcks( i ); 
		Eat( ); 
		putChpStcks( i ); 
	} 
}

void takeChpStcks( i ) { 
	wait( mutex ); // critical session
	
	state[i] = HUNGRY; 
	safeToEat( i ); // check if left and right are not eating
	
	signal( mutex ); 
	
	wait( s[i] ); // if okay to eat, eat. Else, wait.
}

void safeToEat( i ) { 
	if( (state[i] == HUNGRY) && 
		(state[LEFT] != EATING) && 
		(state[RIGHT] != EATING) ) { 
		
		state[ i ] = EATING; 
		signal( s[i] ); // signal that u r allowed to eat
	} 
}

void putChpStcks( i ) { 
	wait( mutex ); 
	
	state[i] = THINKING; 
	safeToEat( LEFT ); 
	safeToEat( RIGHT ); 
	
	signal( mutex ); }
```

##### Alternative problem

What happens if at most 4 philosophers are allowed to dine at any time? We can have a solution that ensures no deadlock without any explicit synchronisation (meaning no mutex and critical conditions). 

![[Pasted image 20231024100420.png]]

Idea:
- each chopstick has a semaphore initialised to 1.
- each philosopher takes the left chopstick if available, then the right chopstick if available.
- there is always **at least** one philosopher who have 2 available chopsticks (there is an extra one)
- ! this does not mean only one philosopher can eat at anytime. It depends on the order of execution. 
- Advantage: no mutex bottleneck.

```C
void philosopher( int i ) { 
	while (TRUE) { 
		Think( ); 
		
		wait( seats ); 
		wait( chpStk[LEFT] ); 
		wait( chpStk[RIGHT] ); 
		
		Eat( ); 
		
		signal( chpStk[LEFT] ); 
		signal( chpStk[RIGHT] ); 
		signal( seats ); 
		} 
	}
```





