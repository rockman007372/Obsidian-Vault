---
tags: processed
course: CS2100
type: 
date: 2022-08-09 Tuesday
---
## Side-effect of assignment

- Assignments have side-effect of returning the assignment value
- This allows for nested assignments

```C
c = (b = (a = 12)) // a = 12 returns 12
```

## Arithmetic Operations

- Execution from left to right: respecting parentheses, then **precedence rule**, then associative rule.

  ![[Pasted image 20220817025341.png]]

```C
// difference btw expr++ and ++expr
int a = 5, b;
b = ++a; // a = 6, then b = 6
b = a++; // b = 5, then a = 6

int a = 5, b = 5
int c = (a++) + (b++); // c = 10, a = 6, b = 6

// % has higher precedence than + and -
int x = 1 + 10 % 3; // 1 + 1 = 2
```
  
- Truncate result if result cant be stored:

```C
int n = 9 * 0.5 // result = 4, truncated to 4 bytes
```

### Mixed type Arithmetic Expression

```C
int m = 10 / 4; // m = 2 

float p = 10 / 4; // p = 2.0, 10 / 4 is reduced to 2 (int) → becomes 2.0

float q = 10 / 4.0; // q = 2.5
float q = 10.0 / 4; // q = 2.5

int n = 10 / 4.0; // n = 2

int r = -10 / 4.0; // r = -2, NOT -3?? (2.5 → 2 → -2)
```

### Type Casting

```C
int a = 6; 
float f = 15.8;

float p = (float) a / 4; // 1.5

float q = (float) (a / 4); // 1.0 (1.5 -> 1 -> 1.0)

int n = (int) f / a; // reduced to 2

```

- - -
Links: [[CS2100]]


