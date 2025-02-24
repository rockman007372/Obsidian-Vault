---
tags:
  - toProcess
course: CS3211
type: tutorial
date: 2025-02-14 Friday
---


1. Cohenrence order:
	- records the sequence of write **and READ** operations performed to a particular memory location.
	- place each read operation immediately after the write that it reads from.
	- the coherence order of **a single atomic variable** must be consistent across all threads
	- **The takeaway**: we can use the guarantees provided by the coherence order to reason about the values read by the read operations.
	
	```c++
	x.store(1, stdmo::relaxed);  // (a)
	x.store(2, stdmo::relaxed);  // (b)
	```
	- After we finish executing the code snippet above, the modification order of `x` must always be `0 -> (a) -> (b)`. It cannot be `0 -> (b) -> (a)` since `(a)` happens before `(b)`, and a reversal here would violate coherence.

2. To ensure sync with relationship, must always use a while loop to ensure one thread reads the same value written by the other thread

3. Draw ordered graph and analyze carefully: there may not be an order between 2 operations!

```
a -> b 
a -> c

b and c has no order!

Hence if the variable is not atomic, b and c can result in data race if at least one is a write op
```

4. modification order is relevant to one variable, not between threads!
	- happen-before relationship does not mean executed before
	```java
	(a) happens before (b) but (b) can get executed before (a)
	
	T1:
	(a) fetch-add(x, 1, relaxed)
	(b) fetch-add(y, 1, relaxed)
	
	T2:
	(c) fetch-add(y, 1, relaxed)
	(d) fetch-add(x, 1, relaxed)
	
	MO of x: 0, (d), (a)
	MO of y: 0, (b), (c)
	```
	
	- ? Question: What if we change the memory order to `acq_rel` or `seq_cst`? 

## Memory order vs Coherence/Modification order

Memory order:
- defines **how operations on memory (reads and writes) are observed** in a multi-threaded environment. It controls **visibility and ordering** of memory accesses across CPU cores.

Coherence order:
- ensures that **all threads observe writes to a single memory location in the same order**. It does not guarantee order **between different memory locations**.

> For all memory orders (including relaxed consistency), all threads must agree on the same coherence order for each atomic variable.