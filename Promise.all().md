
The `Promise.all()` method is used to handle multiple promises concurrently. 

It takes an array of promises as input and returns a new promise. This new promise resolves when all the promises in the input array have resolved. 

The resolved values of the promises are available in the `.then()` block as an array in the same order as the input promises.

```js
// With then()
var addTwoPromises = async function(promise1, promise2) {
    return Promise.all([promise1, promise2])
	    .then(res => res[0] + res[1]);
};

// With await
var addTwoPromises = async function(promise1, promise2) {
    const [res1, res2] = await Promise.all([promise1, promise2]);
    return res1 + res2;
};

/**
 * addTwoPromises(Promise.resolve(2), Promise.resolve(2))
 *   .then(console.log); // 4
 */
```

This is to avoild consequential execution of promise chains:

```js
var addTwoPromises = async function(promise1, promise2) {
    return promise1.then((val) => promise2.then((val2) => val + val2));
};

// or alternatively

var addTwoPromises = async function(promise1, promise2) {
    return await promise1 + await promise2;
};
```