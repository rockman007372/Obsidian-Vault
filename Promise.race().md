 It accepts an array of promises and returns a new promise. The returned promise resolves or rejects with the **first value** of the promises it resolves or rejects with.

```js
var timeLimit = function(fn, t) {
	return async function(...args) {
        const originalPromise = fn(...args);
        const timeoutPromise = new Promise((_, reject) => {
            setTimeout(() => reject('Time Limit Exceeded'), t)
        });
        
        return Promise.race([originalPromise, timeoutPromise]);
    }
};
```