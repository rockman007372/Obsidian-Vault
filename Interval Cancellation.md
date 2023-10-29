---
tags:
  - LeetCode
  - leetcode
topics: promise
difficulty: medium
performance: uncomplete
date: 2023-09-28 Thursday
---

## Questions

Given a function `fn`, an array of arguments `args`, and an interval time `t`, return a cancel function `cancelFn`.

The function `fn` should be called with `args` immediately and then called again every `t` milliseconds until `cancelFn` is called at `cancelT` ms.

**Input:** 

```
fn = (x) => x * 2, args = [4], t = 35, cancelT = 190
```

**Output:** 
```
[
   {"time": 0, "returned": 8},
   {"time": 35, "returned": 8},
   {"time": 70, "returned": 8},
   {"time": 105, "returned": 8},
   {"time": 140, "returned": 8},
   {"time": 175, "returned": 8}
]
```
## Solution

### Recursion and Lazy Evaluation

```javascript
var cancellable = function(fn, args, t) {
    fn(...args);
    
    let timerId = null;

    const recursiveCall = () => {
        timerId = setTimeout(() => {
            fn(...args);
            recursiveCall();
        }, t)
    };

    recursiveCall();

    return () => {
        clearTimeout(timerId);
    };
};
```

We make use of both recursion + setTimeout to delay calling the function every t milisecond. 
- setTimeout is async, hence `cancellable()` will return the cancellable function immediately.
- Recursion and lazy evalution enforces sequential execution of functions.

### setTimer API

```js
var cancellable = function(fn, args, t) {
    fn(...args);
    const timer = setInterval(() => fn(...args), t);

    const cancelFn = () => clearInterval(timer);
    return cancelFn;
};
```

It's important to note that `setInterval` does not immediately call the function before `t` milliseconds, which is why we manually call `fn(...args)` once before setting the interval.

---
Link: [[LeetCode]]
