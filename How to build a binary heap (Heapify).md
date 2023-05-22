---
tags: 
aliases: heapify
date: 2023-05-22 Monday
---

Given an array of priorities in a random order, we can heapify using this algorithm: 

>[!algorithm]
> Starting at the end of the array, perform bubble down on each element (right to left)

```Java
Heapify(int[] priorities) {
	for (int i = priority.length - 1; i >= 0; i--) {
		bubbleDown(priorities[i]);
	}
}
```

We can even do better by starting at the first non-leaf node:

```
Starting at last non-leaf node (index = n / 2 - 1)
eg: [3, 2, 4, 5, 6, 1]
           ^ start here
```

Using abstract math, we can prove Heapify has asymptotic cost of O(N) .