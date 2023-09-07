---
tags: js
aliases: 
date: 2023-05-26 Friday
---

Shallow copy:

```js
numbers = [1, 2, 3];
numbersCopy1 = [...numbers];
numbersCopy2 = numbers.slice();
```

Deep copy:

```js
nestedNumbers = [[1], [2]];
numbersCopy = JSON.parse(JSON.stringify(nestedNumbers));
```