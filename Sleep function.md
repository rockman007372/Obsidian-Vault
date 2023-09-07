---
tags: LeetCode, leetcode
topics: javscript, promise
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

```javascript
/**
 * @param {number} millis
 */
async function sleep(millis) {
    return new Promise(resolve => setTimeout(resolve, millis)) 
    // the resolve function is only called after timeout
}
```

---
Link: [[LeetCode]]
