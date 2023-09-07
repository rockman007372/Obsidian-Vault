---
tags: LeetCode, leetcode
topics: 
difficulty:
performance:
date: 2023-05-25 Thursday
---

## Questions

Given an **asyncronous** function `fn` and a time `t` in milliseconds, return a new **time limited** version of the input function.

A **time limited** function is a function that is identical to the original unless it takes longer than `t` milliseconds to fullfill. In that case, it will reject with `"Time Limit Exceeded"`.  Note that it should reject with a string, not an `Error`.

Example:

```javascript
const limited = timeLimit(
	(t) => new Promise(res => setTimeout(res, t)), 100);

limited(150).catch(console.log) 
// "Time Limit Exceeded" at t=100ms
```

## Solution

Idea:
- Run 2 independent promises inside the **executor function** of the Promise. One is for the timer and the other is for the given function.
- We resolve or reject the promise based on which ever promise is resolved first.
- We can handle clearing timeout after the promise is resolved using `finally` and `clearTimeout()`

```javascript
/**
 * @param {Function} fn
 * @param {number} t
 * @return {Function}
 */
var timeLimit = function(fn, t) {
	
    return async function(...args) {
        return new Promise((resolve, reject) => {
            
            // set time limit asynchronously
            const timeoutId = setTimeout(() => reject("Time Limit Exceeded"), t);
            
            // calls the function right after
            fn(...args)
                .then(resolve)
                .catch(reject)
                .finally(() => clearTimeout(timeoutId));
        })
    }
};
```

### Async/Await

We can also use Async/Await syntax to simplify the logic.

```javascript
var timeLimit = function(fn, t) {
  return async function(...args) {
    return new Promise(async (resolve, reject) => {
      const timeout = setTimeout(() => {
        reject("Time Limit Exceeded");
      }, t);

      try {
        const result = await fn(...args);
        resolve(result);
      } catch(err) {
        reject(err);
      }
      clearTimeout(timeout);
    });
  };
};
```

---
Link: [[LeetCode]]
