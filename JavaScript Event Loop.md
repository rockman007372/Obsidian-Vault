---
tags: JS
aliases: 
date: 2023-05-25 Thursday
---

JavaScript uses a **call stack** to manage the execution of functions. When a function is called, it's added to the stack. When the function completes, it's removed from the stack. JavaScript, being single-threaded, can only execute **one function at a time**.

However, this could be problematic if a function takes a long time to execute (like a network request). This is where the Event Loop comes in.

**The Event Loop is a continuous loop that checks if the call stack is empty**. If it is, it takes the first task from the task queue (also known as the event queue or the callback queue) and pushes it onto the call stack, which immediately executes it.

[[How does the Event Loop work with Concurrency]]