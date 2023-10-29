---
tags: []
course: CS2100
type: lecture
date: 2022-08-19 Friday
---

1. [[Pointers in C]]
2. [[Functions in C]]

- - -
## Practice Questions
##### Q1. Pointer to a pointer

```C
int x = 2;
int *p;
int **q;

p = &x;
q = &p;

(**q)++; // *(*q) = *p = x

x == 3; // true
```
##### Q2. Pointers casting

```C
int main() {
	int a = 130; // stored as hex: 0x86 = 1000 0010 (1 byte)
	char *ptr;
	ptr = (char *) &a;
	printf("%d", *ptr); // -126, because char variable is a signed var
	return 0;
}
```


