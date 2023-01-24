---
tags: processed
course: CS2100
type: lecture
---
Date:: 2022-08-07 Sunday
Links: [[CS2100]] - [[Programming Language]]
Next: [[Computations in C]]
- - -
# Introduction to C

## Recitation Questions
##### Q1: Calculator
```
Write a program that:  
1. Asks for an operator, which can be “+”, “-“, “*”, “/” or “q”.  
2. If the operator is +, -, * or /, ask for two floating point numbers.  
3. Prints “Unrecognized operation” if the operator entered is not +, -, *, / or q.  
4. If the person enters ”q” the program says “Bye!” and exits. If the user enters +,  
-, *, /, the program performs the operation on the two numbers entered and  
prints the result in two decimal places.  
5. If the user did not enter “q”, go to 1.
```

```C
#include <stdio.h>

void calculator() {
  float a;
  float b;
  char oper;
    
  while (1) {
    printf("Please Enter an Operation: ");
    scanf(" %c", &oper); // THE SCANNER KEEPS READING THE PREVIOUS LINE ???
    
    if (oper == 'q') break;

    if (oper != '+' && oper != '-') {
      printf("\nUnrecogized operation wtf\n");
      fflush(stdin);
      continue; 
    }
    
    printf("Enter the first number: ");
    scanf("%f", &a);
    
    printf("Enter the second number: ");
    scanf("%f", &b);
    
    switch(oper) {
      case '+':
        printf("%.2f + %.2f = %.2f\n", a, b, a + b);
        break;
      case '-':
        printf("%.2f - %.2f = %.2f\n", a, b, a - b);
        break;
      default: 
        printf("fuck\n");
    }
    
    fflush(stdin);
  } 
  
  printf("Bye");
}

int main() {
  calculator();  
  return 0;
}  
```

##### Q2: booleans in C
```C
int a = -1, b = -1, c = 0, d;
d = ((a && b) || !c);
printf("d = %d\n", d); // return 1 (NOT TRUE, no boolean values)
```

##### Q3: Average program - Control && Loop

```
1. Prompt the user to enter unlimited valid numbers
2. Numbers are considered valid if they are in the range of 0 to 100
3. Use the number 9999 to terminate the input
4. After that compute the average of the valid numbers enter
```

```C
// Online C compiler to run C program online
#include <stdio.h>

float mean() {
    float sum = 0.0; int count = 0;
    float input = 0.0;
    printf("Enter numbers between 0 and 100 inclusive:\n");
    while (1) {
        scanf("%f", &input);
        
        if (input == 999) break;
        
        if (input >= 0 && input <= 100) {
            sum += input;
            count++;
        } else {
	        printf("Invalid");
        }
    }
    printf("Average is %.2f", count == 0 ? 0 : sum / count);
    return 0;
}

int main() {
    mean();
}
```

## Notes
### What is C

C is very fast and close to computer language (much faster than Python)

Edit -> Compile -> Execute (Just like Java, it is a [[Compile Language]])

Compile error: Error during compilation. 

Runtime error: Error during runtime, because the compiler could not catch the error.

### C vs Python

Standard C framework:
```C
preprocessor directives

main function header
{
	declaration of variables
	executable statements
}
```

Python version:
```Python
KMS_Per_MILE = 1.609 #conversion constant

def main():
	miles = float(input("Enter distance: "))
	kms = KMS_PER_MILE * miles
	print("That equals", kms, "km.")
	
	return 0

# to check if this programme is run in command line
if __name__ == "__main__":
	main()
```
Python does not have constant, only variable.
2 ways to run Python, either run in command line or import them as modules?

C version:
```C
#include <stdio.h> /* printf, scanf definitions */
#define KMS_PER_MILE 1.609 /* conversion constant */

int main(void) {
	float miles, kms;
	
	printf("Enter distance: ");
	scanf("%f", &miles);
	
	kms = KMS_PER_MILE * miles;
	
	printf("That's equals %9.2f km. \n", kms);
	
	return 0; // inform of the status of the program
}
```
To compile: `gcc MileToKm.c`

To run: `a.out`

`$ gcc DataTypes.c -o DataTypes` is used to compile C program.
`-o`option specifies name of executable file (default name is `a.out`).

### von Neumann Architecture

RAM ([[Random Access Memory]]) is the memory where programmes and variables are stored.

von Neumann describes the computer consisting of 3 components:
- Central Procressing Unit (CPU)
	- Registers
	- A control unit containing an instruction register and program counter
	- An arithmetic/logic unit (ALU)
- Memory
	- Stores both program and data in [[Random Access Memory|RAM]]
- I/O devices (Input/Output)
  
![[Pasted image 20220808121724.png]]

### Variables

Data used in a program are stored in variables

Every variable has a **name**, **data type** and contains a **value** which could be modified.

Each variable also has an **address**.

Without initialization, the variable contains an **unknown value** (Cannot assumed to be zero!).

```C
int main(void) {
	int count;
	count = count + 1 // error
	return count;
}
```

### Data Type

- Basic data types in C: (no `boolean`  and `string`!)
	- `int`: 4 bytes - 32 bits
	- `float`: 4 bytes
	-  `double`: 8 bytes (better precision, but slower execution, more memory used)
	- `char`: 1 byte.
		- 8-bit integer used to store a single character in ''
		- Each char is mapped to a number in ASCII table.

```C
// this program checks the memory size of each of the basic data types - in BYTES
#include <stdio.h>

int main(void) {
	printf("Size of int (in bytes): %d\n", sizeof(int)); // 4
	printf("Size of float (in bytes): %d\n", sizeof(float)); // 8
	return 0;
}
```

- Basic principle in C: **Everything is a number.**

- A programming language can be either *strongly typed* or *weakly typed*.
	- *Strongly typed*: every variable to be declared with a data type. (C, Java, Pascal)
	- *Weakly typed*: the type depends on how the variable is used. (Python, Javascript)

- Variables in C can be typecasted: `int y = (int) 1.1 // y = 1`

### Program Structure
- A basic C program has 4 main parts:
	- Prepocessor directives
		- `#include <stdio.h>`
		- `#include <math.h>`
		- `#define PI 3.142`
	- Input: through stdin (using `scanf`) or file input.
	- Compute: through arithmetic operations and assignment statements.
	- Output: through stdout (using `printf`) or file output.

### Preprocessor Directives
- The C preprocessor provides the following:
	- Inclusions of header files
	- Macro expansions
	- Conditional compilation
- *Inclusion of header files:*
	- `#include <stdio.h>` allows us to use input/output functions like scanf() and printf()
	- `#include <math.h>` to use mathematical functions (need to compile with `-lm` option, else compilation error).
	- `#include <string.h>` for string functions.
- *Macro expansions*
	- One of the uses is to define a macro for a constant value
	- Eg: `#define PI 3.142 // declare a constant`

```C
#define PI 3.142

int main(void) {
	...
	areaCircle = PI * radius * radius; 
	// preprocessor replaced all instances of PI with 3.142 
	// before passing the program to the compiler
}
```

**DO NOT** put semicolon `;` at the end of `#define PI 3.142;` because C will replace all instances of PI as `3.142;` 

### Input/Output
```C
int age;
double cap;
printf("What is ur age? ");
scanf("%d", &age); 
// %d is for integer
// &age is for the address of the variable

printf("Whats ur cap? ");
scanf("%lf", &cap);

printf("You are %d years old, ur cap is %f\n", age, cap);

// another way to obtain input
scanf("%d %lf", &age, &cap);
```
- `age` refers to the value in the variable age
- `&age` refers to the address of the memory cell where the value of age is stored. (**Only used for scanf**)
- `%d` is an example of *format specifiers*. They are placeholders for values to be displayed or read.
  
  ![[Pasted image 20220809012222.png]]

- You can specify the width of output in `printf()`:
	- `%5d`to display an integer with width of 5, right justified
		- eg: 123 →`_ _ 1 2 3`
		- `%8.3f` to display a real number in the width of 8, with 3 dp

- Example of  `escape sequence`:
![[Pasted image 20220809012530.png]]

```C
printf("hello "world"") // will give an error
printf("hello \"world"\") // will give double quote
printf("%5%") // will give 5% ???
```

---
## Other links
[[Computations in C]]
[[Control Structure in C]]


