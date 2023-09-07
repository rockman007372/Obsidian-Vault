- C is a lower end of high-level programming languages
	- It has **pointers** → direct memory access
	- It has **bit manipulation operators** → bitwise operations
- A variable occupies some space in the computer memory known as an address. 
- We refer to the address of a variable using the **address operator**:  `&`
- Addresses use **byte** as the smallest unit → A unit in memory spans 8 bits.

![[Pointers and Functions 2022-08-27 07.52.59.excalidraw||400]]

```C
int a = 69;
printf("Address of a = %p\n", &a); # Hexadecimal format
```

## Pointer Variable

A pointer variable is a variable **containing the addresss** of another variable.

![[Pasted image 20220827075713.png]]
![[Pasted image 20220827075729.png]]

## Declaring a Pointer and Assign Values

```C
// 2 ways to declare a pointer:

// way 1:
int a;
int *a_ptr; // Read from right to left: a_ptr is a pointer pointing towards an integer 
a_ptr = &a;

// way 2:
int a;
int *a_ptr = &a

// IMPORTANT: THIS IS NOT THE SAME AS ABOVE AND NOT LEGAL
double a;
double b = &a;
```

## Accessing Value Through Pointer  

We can access the variable pointed to by the pointer using `indirection/dereferencing operator *` 

```C
int a = 100;
int *a_ptr = &a;

printf("address: %p\n", a_ptr); // some address
printf("value: %d\n", *a_ptr); // dereferenced: 100

*a_ptr == a; // return true / 1
```

## Incrementing a Pointer  

When we increment an address, we move to the next consecutive address not occupied by the current variable.

Hence, the number of bytes incremented depends on the type of variable (and the number of bytes it occupies).

```C
int a;
int *ap = &a;

ap;   // ffbff0a4
ap++; // ffbff0a8, + 4 bytes (a is of type int, hence it occupies 4 bytes)
```

>[!Important]
>**Each address identifies a single byte (eight bits)** of storage. Data larger than a single byte may be stored in a sequence of consecutive addresses.

## Common Mistake

```C
int *a; // pointer not pointing to any variable
*a = 123;
// This will result in Segmentation Fault (core dumped??)
```

## Why Do We Use Pointers?

- Pass the *addresses of variables to function* so the functions can modify the variables outside of it.
- Pass the address of the *first element of an array* to the function so it can access all the remaining elements of the array.