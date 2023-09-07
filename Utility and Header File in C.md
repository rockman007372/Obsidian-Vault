>[!summary]
>Header file is akin to an **interface** while utility file is akin to a **concrete class** implementing that interface in Java.

In C programming, **header files** contain declarations of functions, variables, and other constructs that can be shared between multiple source files. [They are included in a source file using the `#include` preprocessor directive](https://www.geeksforgeeks.org/header-files-in-c-cpp-and-its-uses/) [1](https://www.geeksforgeeks.org/header-files-in-c-cpp-and-its-uses/). This allows the compiler to check for correct usage of the constructs declared in the header file and helps to avoid errors such as using an undeclared function or variable.

A **utility file** typically refers to a source file that contains definitions of utility functions or other constructs that are used by multiple source files in a program. These definitions are separate from the main source code of the program and can be compiled into a library for reuse in other programs.

The use of header and utility files helps to **organize code** into modular, reusable components and makes it easier to maintain and update large programs. By separating declarations and definitions into different files, it is possible to **change the implementation of a function or variable without affecting other parts of the program that use it**.