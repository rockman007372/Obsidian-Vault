---
tags:
  - toProcess
course: CS3211
type: lecture
date: 2024-02-14 Wednesday
---

## Notes

Recap:
- Ownership: an object that contains a pointer to another object on the heap. The owner is responsible for calling the constructor/destructor on the dynamic object.
- RAII: bind the life cycle of a resource to the lifetime of an object.

Synchronising multiple threads:
1. Concurrent access to shared data: Mutex
2. Concurrent actions: 
	1. Condition variable 
	2. Monitor

Race Condition vs Data Race:  [Link](https://stackoverflow.com/questions/11276259/are-data-races-and-race-condition-actually-the-same-thing-in-context-of-conc) 
- Race Cond: outcome depends on the relative ordering of execution. May or may not affect correctness. Usually is a **flaw**. ⇒ not always bad.
- Data Race: 2 threads access and modify the same memory location in unsynchronised manner. Causes undefined behavior. ⇒ always bad.
- eg: There is no data race, but race condition may occur if correctness of the program is dependent on the order of execution.

```
2 threads carrying 2 functions:

thread 1:
	lock(l)
	x = 1
	unlock(l)

thread 2:
	lock(l)
	x = 2
	unlock(l)
```

Mutex:
- Semaphore with value = 1.
- lock() and unlock() = wait() and signal().
- ! Not recommended since we must manually call unlock() on every code path out of a function.
- Instead, we should apply RAII to mutex by using a `std::lock_guard` object. Whenever this object is constructed, mutex is locked. When object is destroyed at the end of its lifetime (e.g, function ends), the mutex is unlocked automatically.

```C
std::mutex my_mutex;
std::list<int> some_list;

void add_to_list(int new_value)
{
	std::lock_guard{some_mutex}; // new standard: use curly bracket as much as possible
	some_list.push_back(new_value);
}
```

- common to group mutex and **protected data** together in a class rather than using global variable.
	- however, this may cause issues when passing references of the protected data outside of the class.
	- cannot be enforced, must practice good habits
- avoid deadlocks when using multple mutexes
	- avoid nested locks (lock within lock)
	- avoid calling user-supplied code while holding a lock
	- acquire locks in a fixed order
- other types of lock
	- `std::unique_lock` object: 
		- allows us to defer locking mutex at construction using `std::defer_lock`
		- allows us to pass ownership of the mutex to another `unique_lock`
	- `std::lock()` function: locks one or more mutexes at once. We can use `std::adopt_lock` later to indicate to `std::lock_guard` object that the mutexes are already locked, hence the object should acquire ownership instead of locking the mutex again).
	- `std::scoped_lock`  object: locks a list of mutexes at once instead of many sequential steps. Implementation allows no deadlock.

Condition variable:
- Usage: when one thread is waiting for another thread to complete a task before proceeding.
- A thread can continuously check a flag in shared data, and proceeds only when the other thread set the flag ⇒ busy waiting, wasteful
- More efficient implementation: `std::condition_variable` object with `wait()` and `notify_one()` functions allow a thread to wait for a condition to become true before proceeding.
- ! Condition variable works in conjunction with a mutex to ensure the thread is not locking the mutex while waiting.
- Kinda like a semaphore, but the condition in the semaphore is whether the integer is positive??
## Summary

## Questions/Cues

