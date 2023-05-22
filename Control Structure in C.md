---
tags: processed
course: CS2100
type: 
date: 2022-08-09 Tuesday
---
Links: [[CS2100]]
Previous: [[Computations in C]]
- - -

## Switch Structure

```C
switch(<variable or expression>) {
	case value1:
		code to execute if variable/expression == value1
		break;
	case value2:
		code...== value 2
		break;
	default:
		code to execute in else body
		break;
}
```

## Boolean Values

- There are **NO** boolean values in C  → They are stored as integers
- `0 == false`
- `Any other values == true` (1 is representative, but can be any other numbers != 0)

```C
int a = (2 > 3); // 0
int b = (3 > 2); // 1
```

## Logical Operators

>[!note]
> `&&` has higher precedence than `||`

```C
x = (a > b || b > c && a == b)

// is interpretted as
x = (a > b || (b > c && a == b)) // gives a different result
```

## Break and Continue

- Only break/continue from the **innermost loop**.


