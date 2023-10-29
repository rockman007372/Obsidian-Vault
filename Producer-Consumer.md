
##### Problem

![[Pasted image 20231015121058.png]]

- Producer writes to buffer if buffer is not full.
- Consumer reads from buffer if buffer is not empty.
- Producers cannot write at the same time and consumers cannot read at the same time.
##### Solution
- Initially: 
	- `in` = `out` = `0`
	- `mutex = S(1)`
	- `notFull = S(K)`
	- `notEmpty = S(0)`
- Big idea:
	- mutex implements a critical session, only allowing one producer to write and one consumer to read at anytime.
	- `notEmpty` and `notFull` force consumer/producer to sleep when buffer is empty/full.

```C
// Producer
while (true) {
	Produce Item;
	
	wait(notFull);
	wait(mutex)
	
	buffer[in] = item
	in = (in + 1) % K;
	
	signal(mutex);
	signal(notEmpty); // signal consumers to read
}
```

```C
// Consumer
while (true) { 
	wait( notEmpty ); 
	wait( mutex ); 
	
	item = buffer[out]; 
	out = (out + 1) % K; 
	
	signal( mutex ); 
	signal( notFull ); // signal producer to write
	
	Consume Item; 
}
```