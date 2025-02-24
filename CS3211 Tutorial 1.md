---
tags:
  - toProcess
course: CS3211
type: tutorial
date: 2025-02-07 Friday
---
Always call join() / detach() on a thread running some function.
- thread t1 calls its destructor and realises its not detached => error code returns

```c++
int main() {
	std::thread t1{test};
	// t1.join();
	return 0; // Never returns 0, returns error code
}
```

When is a thread not joinable:
- Default-constructed thread with no function passed in.
- Moved-From: A `std::thread` that has been **moved from** is no longer associated with a thread of execution.
- Once a thread has been **joined**, it is no longer joinable.
- Alr detached thread

