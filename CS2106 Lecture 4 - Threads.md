---
tags: []
course: CS2106
type: lecture
date: 2023-09-16 Saturday
---
# Content

- [[Threads]]
- [[Thread Models]]
- [[POSIX thread API]]

# Questions

1. Why does each thread use different registers? Not shared? 
	1. prevent threads from overwriting the same registers (sync conflicts)
	2. used for context-switching between threads
2. How do threads have different stack space when memory is shared? How does keeping only FP and SP help?
	1. These stacks exist in the same memory (hardware), just different region/space!
3. Questions regarding the pthread_join() function call.
	1. The main thread waiting for a specific child thread.









