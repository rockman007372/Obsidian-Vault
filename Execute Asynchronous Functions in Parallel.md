---
tags:
  - LeetCode
  - leetcode
topics: promise
difficulty: medium
performance: notOnTime
date: 2023-10-01 Sunday
---

## Questions

Implement [[Promise.all()]]

## Solution

Iterate over the array of promise-returning functions. For each promise-returning function:

- In the `async/await` version, await the promise. Upon resolution, place the result in the corresponding position in the `res` array and increment the `resolvedCount`. If an error is thrown, immediately reject the promise with the error.
- In the `then/catch` version, attach a then clause and a catch clause. Upon resolution, the then clause places the result in the `res` array and increments `resolvedCount`. The catch clause rejects the promise with the error.

If all promises have resolved (i.e., `resolvedCount` equals the length of the function array), it resolves the `promiseAll()` promise with the `res` array.

### then/catch

```javascript
/**
 * @param {Array<Function>} functions
 * @return {Promise<any>}
 */
var promiseAll = function(functions) {
    let result = new Array(functions.length);
    let count = 0;
    
    return new Promise((resolve, reject) => {
        
        functions.forEach((fn, index) => 
            fn().then(res => {
                result[index] = res;
                count++;

                if (count === functions.length) {
                    resolve(result);
                }
            }).catch(err => reject(err)));
    });
};
```
### async/await

```js
var promiseAll = async function(functions) {
    return new Promise((resolve,reject) => {
        if(functions.length === []) {
            resolve([])
            return
        }
        
        const res = new Array(functions.length).fill(null)

        let resolvedCount = 0

        functions.forEach(async (el,idx) => {
            try {
                const subResult = await el()
                res[idx] = subResult
                resolvedCount++
                if(resolvedCount=== functions.length) {
                    resolve(res)
                }
            } catch(err) {
                reject(err)
            }
        })
    })
};
```

Notice that we must declare the consumer in `forEach()` as `async` so that we can use `await` in its function body.

---
Link: [[LeetCode]]
