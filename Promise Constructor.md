
In the promise constructor:
- you pass a callback function, often referred to as the "**executor function**".
- This callback function receives two parameters: `resolve` and `reject`.
- These **parameters are functions themselves** that allow you to control the state and outcome of the promise.

```js
Promise example = new Promise((resolve, reject) => {});
```

The `resolve` function: 
- Fulfill the promise with a successful value. 
- Any registered `then` callbacks associated with the promise will be triggered, and the resolved value will be passed as an argument to those callbacks.

The `reject` function:
- Reject or fail the promise with a reason or an error. 
- Any registered `catch` or `onRejected` callbacks associated with the promise will be triggered, and the rejected reason will be passed as an argument to those callbacks.

```javascript
const myPromise = new Promise((resolve, reject) => {
  // Simulating an asynchronous operation
  setTimeout(() => {
    const success = true;
    if (success) {
      resolve('Success!'); // pass "success" to resolve
    } else {
      reject(new Error('Something went wrong.'));
    }
  }, 2000); // Timeout for 2 seconds
});

myPromise
  .then(result => console.log(result))  // "Success!"
  .catch(error => console.error(error)) // "Error: Something went wrong."
```