---
tags: 
aliases: 
date: 2023-05-20 Saturday
---

At their core, _**objects**_ are just mappings from strings to other values. The values can be anything: strings, **functions**, other objects, etc. The string that maps to the value is called the _**key**_.

```csharp
const object = {
  "num": 1,
  "str": "Hello World",
  "obj": {
    "x": 5
  },
};
```

There are three ways to access values on an object:

1.  _**Dot Notation**_.

```kotlin
const val = object.obj.x;
console.log(val); // 5
```

2.  _**Bracket Notation**_. This is used when the key isn't valid variable name. For example `".123"`.

```kotlin
const val = object["obj"]["x"];
console.log(val); // 5
```

3.  _**Destructuring Syntax**_. This is most useful when accessing multiple values at once. You can read more about the syntax [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment).

```python
const { num, str} = object;
console.log(num, str); // 1 "Hello World"
```

You can read more about objects [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_objects).