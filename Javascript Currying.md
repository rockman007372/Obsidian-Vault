---
tags: JS
aliases: 
date: 2023-05-23 Tuesday
---

Currying is a powerful technique in functional programming that transforms a function with multiple arguments into a **sequence of functions**. It allows you to create flexible and reusable code by enabling partial application of function arguments.

## Example

Suppose we have a function sum that takes three arguments and returns their sum:

```javascript
function sum(a, b, c) {
  return a + b + c;
}
```

We can create a curried version of this function, curriedSum. Now, we can call curriedSum in various ways, all of which should return the same result as the original sum function:

```javascript
const curriedSum = curry(sum);

console.log(curriedSum(1)(2)(3)); // Output: 6
console.log(curriedSum(1, 2)(3)); // Output: 6
console.log(curriedSum(1)(2, 3)); // Output: 6
console.log(curriedSum(1, 2, 3)); // Output: 6
console.log(curriedSum()()(1, 2, 3)); // Output: 6
```

Currying in JavaScript has several practical applications that can help improve code readability, maintainability, and reusability. Here are some practical use cases of currying:

1. Reusable utility functions: Currying can help create reusable utility functions that can be easily customized for specific use cases. Currying allows you to create a function that returns another function with a partially applied argument. 

```javascript
const add = a => b => a + b;
const add5 = add(5);
const result = add5(3); // 8
```
   
2.  Event handling: In event-driven programming, currying can be used to create event handlers with specific configurations, while keeping the core event handling function generic.

```javascript
const handleClick = buttonId => event => {
   console.log(`Button ${buttonId} clicked`, event);
};

const button1Handler = handleClick(1);
document.getElementById("button1").addEventListener("click", button1Handler);
```

3.  Customizing API calls: Currying can help create more specific API calls based on a generic API call function.

4.  Higher-order functions and functional composition: Currying enables the creation of higher-order functions that can be composed to create more complex functionality.    

```javascript
const compose = (f, g) => x => f(g(x));

const double = x => x * 2;
const square = x => x * x;

const doubleThenSquare = compose(square, double);

const result = doubleThenSquare(5); // (5 * 2)^2 = 100
```

## 