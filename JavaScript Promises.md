---
tags: JS
aliases: 
date: 2023-05-25 Thursday
---

Definition:

- A [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) is an object representing the eventual completion or failure of an asynchronous operation.
- It allows you to associate handlers with an asynchronous action's eventual success value or failure reason. 
- This lets asynchronous methods return values like synchronous methods: instead of immediately returning the final value, the asynchronous method returns a _promise_ to supply the value at some point in the future.

A `Promise` is in one of these states:

- _pending_: initial state, neither fulfilled nor rejected.
- _fulfilled_: meaning that the operation was completed successfully.
- _rejected_: meaning that the operation failed.

A promise is said to be _settled_ if it is either fulfilled or rejected, but not pending.

## Constructor

In the promise constructor, you pass a callback function, often referred to as the "**executor function**". This callback function receives two parameters: `resolve` and `reject`. These **parameters are functions** that allow you to control the state and outcome of the promise.

The `resolve` function is used to fulfill or resolve the promise with a successful value. By invoking `resolve` and passing a value as an argument, you transition the promise from a pending state to a fulfilled state. Any registered `then` callbacks associated with the promise will be triggered, and the resolved value will be passed as an argument to those callbacks.

The `reject` function, on the other hand, is used to reject or fail the promise with a reason or an error. By invoking `reject` and passing an argument (typically an `Error` object or an error message), you transition the promise from a pending state to a rejected state. Any registered `catch` or `onRejected` callbacks associated with the promise will be triggered, and the rejected reason will be passed as an argument to those callbacks.

```javascript
const myPromise = new Promise((resolve, reject) => {
  // Simulating an asynchronous operation
  setTimeout(() => {
    const success = true;
    if (success) {
      resolve('Success!');
    } else {
      reject(new Error('Something went wrong.'));
    }
  }, 2000);
});

myPromise
  .then(result => console.log(result))  // Success!
  .catch(error => console.error(error)) // Error: Something went wrong.
```


## Async and Await

[[Async and Await in Promises]]