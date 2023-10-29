---
tags:
  - LeetCode
  - leetcode
  - JS
topics: promise
difficulty: easy
performance: uncomplete
date: 2023-05-25 Thursday
---

## Questions

Given a positive integer `millis`, write an asyncronous function that sleeps for `millis` milliseconds. It can resolve any value.

**Example:**

```javascript
/**
Input: millis = 100
Output: 100
Explanation: It should return a promise that resolves after 100ms.
*/

let t = Date.now();
sleep(100).then(() => {
  console.log(Date.now() - t); // 100
});

```

## Solution

Must call `resolve()` after timeout! Else promise will never resolve.

```javascript
/**
 * @param {number} millis
 */
async function sleep(millis) {
    return new Promise(resolve => setTimeout(resolve, millis)) 
    // the resolve function is only called after timeout
}
```

- `setTimeout` is a web API method that introduces a delay in the execution of code.
- Once `setTimeout` is called, the JavaScript runtime sets up the timer, but then **immediately continues** executing any following code. 
- `setTimeout()` returns `timeoutID`, a positive integer value which identifies the timer created by the call to `setTimeout()`. This value can be passed to [`clearTimeout()`](https://developer.mozilla.org/en-US/docs/Web/API/clearTimeout "clearTimeout()") to cancel the timeout.

---
Link: [[LeetCode]]
