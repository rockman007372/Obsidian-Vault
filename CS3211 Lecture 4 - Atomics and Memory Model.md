---
tags:
  - toProcess
course: CS3211
type: lecture
date: 2024-02-18 Sunday
---

## Notes

- Correctly synchronised program:
	- Order is similar to a sequential program
	- Write operations appear to be atomic
- The compiler may reorder the operations, which can mess with multi-threader program ⇒ need to know the memory model?
- As-if rule: The c++ compiler can perform any changes to the program as long as the following remains true:
	- ? Access to volatile objects are not reordered wrt other volatile accessses on the same thread
	- At program termination, data written to files is exactly as if the program was executed as written ⇒ data output is the same
	- Promting texts to I/O device are shown before program waits for input.
	- Programs with undefined behavious are free from this rule ⇒ programs should have defined behaviours
- If there is a data race, there is undefined behaviors.
- To avoid data races: implement critical section
	- Locks (mutex)
	- **Ordered Atomics**
- Atomic operations: an indivisible operation, always observed as fully done from any thread
- Atomic value: no half-result.
- Modification Order:
	- Composed of all writes to an object from all threads
	- Varies between run
	- Each object has different MO
- If object is not of atomic type:
	- programmer is responsible for ensuring threads agree on modification order of each variable.
- If variable are atomic:
	- the compiler is responsible instead
	- ! does not mean programs that use atomic variable are race-free.

## Summary

## Questions/Cues

