---
tags: LeetCode, leetcode
topics: 
difficulty:
performance:
date: 2023-05-26 Friday
---

## Questions


## Solution

### Recursive

```javascript
/**
 * @param {Function[]} functions
 * @param {number} n
 * @return {Function}
 */
var promisePool = async function(functions, n) {
    return new Promise((resolve) => {
        
        let fnsInProgress = 0;
        let fnIndex = 0;

        const helper = async function() {

            // resolve the returned promise once all promises are resolved
            if (fnIndex >= functions.length) {
                if (fnsInProgress === 0) {
                    resolve();
                    return;
                }
            }

            // add functions to "queue"
            while (fnsInProgress < n && fnIndex < functions.length) {
                const promise = functions[fnIndex]();
                fnsInProgress++;
                promise.then(() => {
                    fnsInProgress--;
                    helper();
                });
                fnIndex++;
            }
        }

        helper();
    });
};
```

### Async/Await Syntax

```javascript
/**
 * @param {Function[]} functions
 * @param {number} n
 * @return {Function}
 */
var promisePool = async function(functions, n) {
    const copiedFunctions = [...functions];
        
    async function evaluateNext() {
        if (copiedFunctions.length === 0) {
            return; 
        } 
        const fn = copiedFunctions.shift(); 
        
	    // ensures the async function is not resolved early
        await fn(); 
        await evaluateNext();
		
		// alternatively, we can return a promise
		// return fn().then(evaluateNext);
    }

    const promiseQueue = Array(n).fill().map(evaluateNext);
    await Promise.all(promiseQueue);
};
```

Key note:
- Use spread syntax to make shallow copy of new array
- Array.shift() is JS equivalent of Array.pop(0) in Python
- Array(n) creates an empty array of size n. Must fill it with `undefined` before we can apply map
- Use `Promise.all` to wait for all the promises to resolve and then resolve the original promise.
- ! `Promise.all` will consider a promise as resolved IF the promise does not return any promise! 

### 2 Liner Solution

```js
var promisePool = async function(functions, n) {
    const evaluateNext = 
	    () => functions[n++]?().then(evaluateNext);
    
    return Promise.all(
	    functions.slice(0, n).map(f => f().then(evaluateNext))
    );
};
```

- `functions[n]?.()` will return `undefined` if `n` is out of bounds, else it executes the function at index `n`.
- ! `evaluateNext` must return a promise so the Promise.all is not resolved.

