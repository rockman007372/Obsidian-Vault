
Async/await can be seen as **syntax sugar** on top of promises, making asynchronous code easier to write and understand. 

When we mark a function with the `async` keyword, it becomes an asynchronous function that automatically returns a promise. 

Within an async function, we can use the `await` keyword to pause the execution of the code until the promise is resolved or rejected.

```javascript
// Using explicit .then() and .catch() with promises
fetchData()
  .then(response => {
    // Handle the response
    console.log("Response:", response);
    return processData(response);
  })
  .then(result => {
    // Handle the processed data
    console.log("Processed data:", result);
  })
  .catch(error => {
    // Handle any errors
    console.error("Error:", error);
  });
```

Compared the above with `async and await`:

```javascript
async fetchAndProcessData() {
	try {
		const response = await fetchData();
		console.log("Response:", response);
		
		const result = await procesData(response)
		console.log("Processed data:", result);
	} catch(error) {
		console.error("Error:", error);
	}
}

fetchAndProcessData();
```