---
tags: 
aliases: 
date: 2023-05-20 Saturday
---

You can also define _**classes**_ in JavaScript. The classes's constructor returns an object which is an instance of that class.

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

JavaScript implements classes with special objects call `prototypes`. All the methods (in this case `greet`) are functions stored on the object's prototype.

To make this concrete, the behavior of the above code could be replicated with the following code:

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

Looking at this code, you might wonder "How can you access the greet method even though it's not a key on the alice object"?

The reason is that accessing keys on an object is actually slightly more complicated than just looking at the object's keys. There is actually an algorithm that traverse the _**prototype chain**_. First, JavaScript looks at the keys on the object. If the requested key wasn't found, it then looks on the keys of the prototype object. If it still wasn't found, it looks at the prototype's prototype, and so on. This is how _**inheritance**_ is implemented in JavaScript!

You might also wonder why JavaScript has this strange prototype concept at all. Why not just store the functions on the object itself? The answer is **efficiency**. Every time a new `Person` is created, `age` and `name` fields are added to the object. However only a single _**reference**_ to the prototype object is added. So no matter how many instances of `Person` are created or how many methods are on the class, only a single prototype object is generated.

You can read more about classes [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes).