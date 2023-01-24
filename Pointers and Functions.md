---
tags: processed
course: CS2100 
type: lecture
---
Date:: 2022-08-19 Friday
Links: [[CS2100]]
- - -
# Pointers and Functions

## Questions/Cues
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
## Notes

### 1. Pointers 
- C is a lower end of high-level programming languages
	- It has **pointers** → direct memory access
	- It has **bit manipulation operators** → bitwise operations
- A variable occupies some space in the computer memory known as an address. 
- Refere to address using `Address operator`:  `&`
- Addresses use **byte** as the smallest unit → A unit in memory spans 8 bits.

![[Pointers and Functions 2022-08-27 07.52.59.excalidraw||400]]

```C
int a = 69;
printf("Address of a = %p\n", &a); # Hexadecimal format
```

#### 1.1 Pointer Variable

A pointer variable is a variable **containing the addresss** of another variable.

![[Pasted image 20220827075713.png]]
![[Pasted image 20220827075729.png]]


#### 1.2 Declaring a Pointer and Assign Values
```C
// 2 ways to declare a pointer

int a;
int *a_ptr; // Read from right to left: a_ptr is a pointer pointing towards an integer 
a_ptr = &a;

int a;
int *a_ptr = &a

// IMPORTANT: THIS IS NOT THE SAME AS ABOVE AND NOT LEGAL
double a;
double b = &a;
```


#### 1.3 Accessing Value Through Pointer  

We can access the variable pointed to by the pointer using `indirection/dereferencing operator *` 

```C
int a = 100;
int *a_ptr = &a;

printf("address: %p\n", a_ptr); // some address
printf("value: %d\n", *a_ptr); // 100

*a_ptr == a; // return true / 1
```

#### 1.4 Incrementing a Pointer  

When we increment an address, we move to the next consecutive address not occupied by the current variable.

Hence, the number of bytes incremented depends on the type of variable (and the number of bytes it occupies).

```C
int a;
int *ap = &a;

ap;   // ffbff0a4
ap++; // ffbff0a8, + 4 bytes (a is of type int)
```

>[!Important]
>**Each address identifies a single byte (eight bits)** of storage. Data larger than a single byte may be stored in a sequence of consecutive addresses.

#### 1.5 Common Mistake

```C
int *a; // pointer not pointing to any variable
*a = 123;
// This will result in Segmentation Fault (core dumped??)
```

#### 1.10 Why Do We Use Pointers?

Some purposes:
- Pass the *addresses of variables to function* so the functions can modify the variables outside of it.
- Pass the address of the *first element of an array* to the function so it can access all the remaining elements of the array.

### 2. Functions

#### Library Functions
Must be imported using `#include <library>`
To link to Math Library, we have to add tag `-lm` during compilation.

```
$ gcc -lm MathFunction.c
```

#### User-defined function

Only difference in C: You have to declare **Function Prototype**
- Declared on top before the main function
- Names of parameters are *optional*
- Without it, you get warning messsage from compiler
- Why warning: compiler assumes `int` as default return type for functions

```C
#include <stdio.h>
#include <math.h>
#define PI 3.14159

double circle_area(double); // FUNCTION PROTOTYPE

int main(void) {
    rim_area = circle_area(d2) – circle_area(d1);
    volume = rim_area * thickness;
    printf("Volume of washer = %.2f\n", volume);
    return 0;
}

// This function returns the area of a circle
double circle_area(double diameter) {
    return PI * pow(diameter/2, 2);
}
```

#### Pass by Value vs Pass by Reference
All parameters and variables in a function are local to the function (**scope rule**).

In other programming languages like Java, arguments from a function caller are *passed by value* to a function's parameter, hence shit like this wont fly:

```C
// This func will not swap the values of any variable passed to it.
// Only the local var a and b are swapped
void swap(int a, int b) {
  int temp = a;
  a = b;
  b = temp;
}

int a = 1;
int b = 0;
swap(a, b); // Pass by value
```

However in C, we can use pointers so that arguments are *passed by reference* to the function!

```C
void swap(int *ptr1, int *ptr2) {
  int temp = *ptr1; 
  *ptr1 = *ptr2; 
  *ptr2 = temp;

}

int a = 1;
int b = 0;
swap(&a, &b); // Pass by reference
```

Function can return a pointer:

```C
int *pointer(int *a_ptr) {
	return a_ptr;
}

int *p;
int *d = pointer(p);
```
## Summary