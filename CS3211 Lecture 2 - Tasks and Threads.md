---
tags: []
course: CS3211
type: lecture
date: 2024-02-12 Monday
---
## Notes

Program execution: decompose problem into tasks → assign tasks to threads → orchestrate between threads → map threads to physical cores.

2 types of parallelism:
- **task** parallelism: assign same types of tasks to the same threads → organize threads into a pipeline to solve problem.
- **data** parallelism: [[CS4225]]

In C++98: thread existence are not acknowledged.
in C++11: thread-aware memory model.

```c
void hello()
{
	std::cout<<"hello";
}

int main() 
{
	std::thread:: t(hello);
	t.join();
}
```

`t.join()` causes the main thread to wait until thread t finishes executing.

There are different ways to start threads:
- Thread with a function.

```c
void do_something() 
{
	...
}

std::thread my_thread(do_something);
```

- Thread with a [[Function Object in C++]].

```c
class background_task
{
public:
	void operator()() const
	{
		do_something();
		do_something_else();
	}
}

background_task f;
std::thread my_thread(f);
```

- Thread with a function object (callable type).

```c
std::thread my_thread { background_task() };
```

- Thread with lambda expression.

```c
std::thread my_thread([] {
	do_something();
	do_something_else();
})
```

Make sure to join thread in the catch block when there is exception in the main thread!

`detach()`:
- Relinquishing the control over a thread and allowing it to run independently in the background without being explicitly joined. 
- When a thread is detached, its execution becomes autonomous, and the main thread (or any other thread) doesn't wait for it to finish ⇒ Once detached, a thread is no longer joinable.
- If a detached thread accesses resources that might be destroyed before its execution completes, it can lead to undefined behavior.
	- Some arguments require explicit cast before a thread is generated (string) because the argument may be destroyed before it is automatically typecasted.

Be careful of passing by reference: if you pass an object as argument to a function, a copy of that object is created and passed into the function instead.

Ownership:
- An owner is an object that contains a pointer to the an object on the free store (heap)
- Every object on the free store must have exactly one owner.
- This rule is not enforced in C++.
- Objects are implicitly constructed and destroyed by constructors/destructors.

RAII - Resource Acquisition Is Initialisation
- C++ programming technique
- Binds the (**life cycle of a resource** that must be acquired before use) to the (**lifetime of an object**).
- ensures that resources are automatically released when they're no longer needed, reducing the risk of resource leaks and simplifying resource management.
- For example, `std::string` **object** may allocate a buffer (**resource**) to hold its characters during construction or over the course of many operations, and when the `std::string` goes out of scope, its lifetime ends, thus calling its destructor. The destructor then deallocates the buffer, ensuring that no memory is leaked.

Lifetime:
- The lifetime of an object begins when:
	- storage with proper alignment + size is obtained.
	- its initialisation is completed.
- The lifetime ends when:
	- object is destroyed (if object is non-class/primitive type)
	- destructor is called (if object is class/reference type)
	- the storage it occupies is released or reused by another object not within its scope.
- The lifetime of a referred object may end before its reference ⇒ dangling reference
- The lifetime of an object is at most as long as the lifetime of its storage (on heap)

To prevent race condition, we implement critical section using:
- Locks
- Ordered Atomics
## Summary

- RAII: Resource Management Is Initialisation
- Ownership
- Lifetime
- Thread initialisation, join and detach.

## Questions/Cues

