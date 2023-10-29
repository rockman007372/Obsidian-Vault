---
tags: JS
aliases: 
date: 2023-05-25 Thursday
---

## Definition

- A [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) is an object representing the eventual completion or failure of an asynchronous operation.
- It allows you to associate handlers with an asynchronous action's eventual success value or failure reason. 
- This lets asynchronous methods return values like synchronous methods: instead of immediately returning the final value, the asynchronous method returns a _promise_ to supply the value at some point in the future.

A `Promise` is in one of these states:

- _pending_: initial state, neither fulfilled nor rejected.
- _fulfilled_: meaning that the operation was completed successfully.
- _rejected_: meaning that the operation failed.

A promise is said to be _settled_ if it is either fulfilled or rejected, but not pending.

## Content

- [[Promise Constructor]]
- [[Async and Await in Promises]]
- [[Promise.all()]]
- [[Promise.race()]]

## Nice Leetcode Questions

- [[Sleep function]]
- [[Promise Time Limit]]
- [[Interval Cancellation]]
- [[Execute Asynchronous Functions in Parallel]]