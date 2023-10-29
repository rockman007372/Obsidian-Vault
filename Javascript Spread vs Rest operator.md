---
tags:
  - JS
aliases: 
date: 2023-09-25 Monday
---
Links: 
- - -

## The rest syntax

- allows a function to accept an indefinite number of arguments. 
- denoted by three dots (`...`) followed by a parameter name. 
- collects all the remaining arguments passed to a function into an array.

```javascript
function printArgs(...args) { 
	console.log(args);
}

printArgs(1, 2, 3, 4, 5); // logs [1, 2, 3, 4, 5]
```

## The spread syntax

- unpack elements from an array or an iterable object (like a string or a set) into individual elements. It "spreads" the elements out.
- Use cases:

1. Combine or clone arrays, 

```js
// Clone array
const array = [1, 2, 3];
conts clone = [...array];

// Combine/merge
const array1 = [1, 2, 3]; 
const array2 = [4, 5, 6]; 
const combinedArray = [...array1, ...array2];
```

2. Passing Array Elements as Function Arguments

```js
function sum(a, b, c) {
  return a + b + c;
}

const numbers = [1, 2, 3];
const result = sum(...numbers);
```

3. Convert an iterable into an array.

```javascript
const string = "hello";
console.log([...string]); // Output: ['h', 'e', 'l', 'l', 'o']

const set = new Set([1, 2, 3]);
console.log([...set]); // Output: [1, 2, 3]
```

