---
tags:
  - JS
aliases: 
date: 2023-06-19 Monday
---
Links: 
- - -

```js
for (let i = 0; i < 5; i++) { 
	console.log(i); 
}
```

To iterate through the keys of an object:

```js
const person = {
  name: "John",
  age: 30,
  city: "New York"
};

for (let key in person) {
  console.log(key + ": " + person[key]);
}
```

To iterate through the elements of an array:

```js
const numbers = [1, 2, 3, 4, 5];

for (let num of numbers) {
  console.log(num);
}
```