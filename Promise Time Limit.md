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

Note that ou can only use the `await` keyword inside an `async` function, so we must add the `async` keyword to the callback passed to `new Promise`

### Promise.Race

We can simplify the code by using the `Promise.race` function. It accepts an array of promises and returns a new promise. The returned promise resolves or rejects with the first value one of the promises resolves or rejects with.

```javascript
var timeLimit = function(fn, t) {
	return async function(...args) {
        const originalPromise = fn(...args);
        const timeoutPromise = new Promise((_, reject) => {
            setTimeout(() => reject('Time Limit Exceeded'), t)
        });
        
        return Promise.race([originalPromise,timeoutPromise]);
    }
};
```

If we want to clear the timeout to free up memory, we can do:

```typescript
var timeLimit = function(fn, t) {
	return async function(...args) {
        const originalPromise = fn(...args);
		
		let timeoutId;
        const timeoutPromise = new Promise((_, reject) => {
            timeoutId = setTimeout(() => reject('Time Limit Exceeded'), t)
        });
        
        return Promise.race([originalPromise,timeoutPromise])
	        .finally(() => clearTimeout(timeoutId));
    }
};
```


---
Link: [[LeetCode]]
