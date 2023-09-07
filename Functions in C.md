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

C is a **pass-by-value** language, which means that when you pass an argument to a function, **a copy of the value of the argument is passed**, not the original value itself. This means that any changes made to the argument within the function do not affect the original value outside of the function .

```C
// This func will NOT swap the values of any variable passed to it.
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

However, it is possible to simulate **pass-by-reference** behavior in C by using pointers. When you pass a pointer to a function, the pointer itself is passed by value, but it points to the original value. This means that you can use the pointer to indirectly modify the original value .

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

##### Functions that return a pointer

A **function that returns a pointer** is a function that, when called, returns a memory address of a variable.

```C
int *pointer(int *a_ptr) {
	return a_ptr;
}

int *p;
int *d = pointer(p);
```

```c
#include <stdio.h>

int* returnPointer(int *x) {
    (*x)++;
    return x;
}

int main() {
    int a = 5;
    int *b = returnPointer(&a);
    printf("a = %d, *b = %d\n", a, *b); // a = 6, *b = 6
    return 0;
}

```

##### Function Pointer

A **pointer to a function** (function pointer) is a variable that stores the memory address of a function. This allows the function to be called indirectly through the pointer.

```c
int add(int x, int y) {
	retunr x + y;
}

int main() {
	int (*fpter)(int, int); # function pointer
	fpter = &add;
	int result = (*fpter)(3, 4);
	return result;
}
```

We can return a pointer that points to a function that returns a pointer:

```c
int *(*pfptr)();

int a = 10;
int *func() {
	return &a;
}

pfptr = &func;
printf("Address of a: %p\n", pfptr());
```