---
tags: JS
aliases: 
date: 2023-05-20 Saturday
---
## Class

You can define _**classes**_ in ES6. The classes's constructor returns an object which is an instance of that class.

```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log("My name is", this.name);
  }
}

const alice = new Person("Alice", 25);
alice.greet(); // Logs: "My name is Alice"
```

## Prototype

JavaScript implements classes with special objects call `prototypes`. **All the methods (in this case `greet`) are functions stored on the object's prototype**.

The behavior of the above code could be replicated with the following code:

```javascript
const alice = {
  name: "Alice",
  age: 25,
  __proto__: {
    greet: function() {
      console.log("My name is", this.name);
    }
  }
};
alice.greet(); // Logs: "My name is Alice"
```

 "How can you access the greet method even though it's not a key on the alice object"?

- Looking up keys involve traversing the _**prototype chain**_. 
- First, JavaScript looks at the keys on the object. If key is not found, it then looks on the keys of the prototype object. If it still wasn't found, it looks at the prototype's prototype, and so on. => _**inheritance**_ 

Why prototype?  **Efficiency**. 
- Every time a new `Person` is created, `age` and `name` fields are added to the object. 
- However only a single _**reference**_ to the prototype object is added. => only a single prototype object is generated for every instance of the class.

You can read more about classes [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes).