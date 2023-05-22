---
tags: processed
course: CS2100
type: lecture 
date: 2022-08-21 Sunday
---
Links: [[CS2100]]
- - -
## Notes
### 1. Arrays

```C
#define MAX 5
int numbers[MAX]; // declare array

int nums[MAX] = {0, 1, 2, 3, 4}; // Can initiate array

int nums[] = {6, 8, 9} // No need to specify size, array will assume based on no. elemetents

int nums[5] = {1, 2, 3} // since size is specified, array will fill in empty cells: [1, 2, 3, 0, 0]

for (int i = 0; i < MAX; i++) {
	scanf("%d", &numbers[i]); // Need to pass reference WHEN SCAN
}
```

#### Arrays and Pointers
When an array name `a` appears in an expression, it refers to the *address of the first element* (`a[0]`) of that array → Array name is pointer! → Array is passed ard by reference!

 Remember that when a pointer is incremented, it increments by the number of **bytes** the particular **data type**  it points to occupies in memory.

Similarly, the *address* of each entry in the array is *separated by the number of bytes of the data type stored*. For example: The data type stored in array is of `int` type, hence it takes up 4 bytes (32 bits) to reach the next address  (each array entry takes up 4 bytes).

```C
int a[3]
printf("%p\n", a);          // ffbff724
printf("%p\n", &a[0]);      // ffbff724
printf("%p\n", &a[1]);      // ffbff728, increase by 4 bytes 
&a[1] == (&a[0] + 1);       // true → next address is 4 bytes from the previous address

char c[] = "hello";
char *p = c;               // 0x7ffc6bf77f02
p++;                       // 0x7ffc6bf77f03, increase by 1 bytes

int nums[] = {1, 2, 3};
int *p = nums;             // 746e62d0
p++;                       // 746e62d4, increase by 4 bytes

```

>[!Important]
>**Each address identifies a single byte (eight bits)** of storage. Data larger than a single byte may be stored in a sequence of consecutive addresses.

#### Array Assignment
```C
int source[N] = {1, 2, 3};
int dest[N];
dest = source; // THIS DOES NOT WORK!!!

// To cpy elements, we use for loop!
for (int i = 0; i < N; i++) {
	dest[i] = source[i]
}

// Can you alias array in C?

```

Why can **NOT** we **directly assign** an array to another array
- An array name is a **fixed pointer**; It points to the first element of the array, and this cannot be altered.
- In the code above, we try to alter `dest` so it points somewhere!

We can also use `<string.h>` library function `memcpy()` to copy array.

#### Array Parameters in Functions
Array name is a pointer, hence it is passed by reference to the function → Can modify directly.

```C
int sumArray(int [], int); // function prototype

int main(void) {
	int val[3] = {1, 2, 3};
	return sumArray(val, 3);
}

int sumArray(int arr[], int size) {
	int i, sum = 0;
	for (i = 0; i < size; i++) {
		sum += aarr[i];
	}
	return sum;
}
```

![[Arrays, Strings and Structures 2022-08-21 03.38.09.excalidraw]]

Function prototype: name is not required

```C
int sumArray(int arr[], int len);
int sumArray(int [], int); // same 
```

Since array is a pointer, alternatively we can **pass it as a pointer** as well:

```C
int sumArray(int *, int);

int sumArray(int &arr, int size) {

}
```

#### Modifying Array in a Function

To modify an external variable from a function, we have to pass the address of the variables into the function. EG: `func(&v)`

But since an **array name is already a pointer**, there is no need to pass its address to the function → function can modify the content of any array it receives.

---

### 2. Strings
We can turn an *array of characters* into a `String` by adding a null character `\0` at the end of the array → Without this termination char, a lot of functions wont work!

Differentiate btw `0, '\0', and '0'` :
- The first two of these are the same thing; they just represent an `int` with value `0`.
- `'0'`, however, is different, and represents an `int` with the value of the '0' character, which is `48`.

We can use string functions by including `<string.h>` to manipulate strings.

```c
char str[6];

str[0] = 'e';
str[1] = 'g';
str[2] = 'g';
str[3] = '\0';

// str = ['e', 'g', 'g'], length = 3

// initialise string
char fruit_name[] = "apple";
char fruit_name[] = {'a', 'p', ..., '\0'}; // equivalent as above

// not an string, no termination!!
char chars[4] = {'a', 'b', 'c', 'd'}; // just a char array
```

#### Strings I/O

Read String from stdin:

```C
// Method 1:
fget(str, size, stdin); // read at most size - 1 char, or until new line \n is detected

// Method 2:
scanf("%s", str);
```

Print string to stdout (monitor):

```C
// Method 1:
puts(str); // terminate w new line

// Method 2: WORSE
printf("%s\n", str); // have to add new line manually
```

On interactive input, fgets() also reads in the *newline character*:
- If user input `eat` and press enter:  str = `[e, a, t, \n, \0]`
- We have to replace `\n` with `\0`:

```C
char str[size];
fgets(str, size, stdin);
int len = strlen(str);
if (str[len - 1] == '\n') {
	str[len - 1] = '\0';
} 

// THIS WILL ALSO CHANGE THE LENGTH OF THE STRING
```

Example code: 
```C
#include <stdio.h>
#include <string.h>

int main() {
    
    char str[10];
    
    fgets(str, 10, stdin);
    
    int len = strlen(str);
    if (str[len - 1] == '\n') {
	    str[len - 1] = '\0';
	    printf("fuck"); 
    }

	puts(str);
    
    return 0;
}
```

#### String Functions
Must use `# include <string.h>`

##### Length
```C
// Return no. charaters in s (not including \0)
strlen(s);
```

##### Compare
```C
// Compare 2 strings by ASCII values
// 0 is equal, negative is s1 < s2, positive when s1 > s2
strcmp(s1, s2);

//  Compare the first n characters of s1 and s2 -> use this for safety, because u limit number of char compared
strncmp(s1, s2, n); 
```

##### Copy
```C
// Copy the string pointed to by s2 → the array pointed to by s1
// Unsafe, because string s2 can go on forever → Hackerman
strcpy(s1, s2);

// example:
char name[10];
strcpy(name, "Matthew"); // name = [M, a, ..., e, w, \0, ?, ?]
name = "Matthew"; // does not work!! WE CANNOT ASSIGN STRINGS DIRECTLY SINCE STRING IS AN ARRAY!

// Safer version with limit n
strncpy(s1, s2, n)
```

---
### 3. Structure in Java

Basically equivalent to classes in Java → Allow grouping of heterogenous members.

![[Pasted image 20220827100729.png]]

#### Structure Type

```c
typedef struct {
	int length, width, height;
} box_t; // name of type, need a semicolon!
```

A type is not a variable, it is similar to a **Data Type** (int, float, char...)
- We are *defining a type*, not declaring a var
- NO memory allocated to a type unlike var

#### Instantiate Structure Variables

Structure variables (objects) are instances of a structure type (class).

```C
result_t resultA = {123, 53.5, 'A'};

card_t cardA = {8888, {31, 12, 2000}}; // initialize structure within structure
```

To access variables (fields), we use dot operator. Eg:  `result.grade`

To write a structure member:

```C
scanf("%d\n", &res1.grade);
```

#### Assigning Structures

Unlike an array, we can do assignment with structures
- However, this is a **pass-by-value** assignment!
- The entire structure is **copied.**

```C
result_t res1 = {69, 'B'};
result_t res2;

res2 = res1; // allowed

void print_result(result_t res) {
	// ...
}

print_result(res1); // We are copying the entire structure to res → modifying res in the function has no effect on res1
```

To pass-by-reference, we must pass the **address** of the **structure variable** to the function!
- Unlike an array, which can be passed by its name, since its alr a pointer.
- Passing an **array of structures** is a different matter!

```c
result_t res1 = {69, 'B'};
modify_result(&res1);

void modify_result(result_t *res_ptr) {
	//...
}

void change_name_and_age(player_t *player_ptr) {
  strcpy((*player_ptr).name, "Alexandra");
  (*player_ptr).age = 25;
}

```

#### Arrow Operator (→)

```C
// To acccess a variable (field) of a structure variable from a pointer:
(*player_ptr).name;


// A syntactic sugar
player_ptr->name; // equivalent

// example
void change_name_and_age(player_t *player_ptr) {
  strcpy(player_ptr->name, "Alexandra");
  player_ptr->age = 25;
}
```

## Questions/Cues
##### Q1. ARRAY REFERENCE
We have the following code fragment:

```C
int f(int *);
int main() {
	int a[] = {1, 3, 2, 5};  
	int x;
    x = f(&a[1]);

}
int f(int *p) {
	return *(p – 1)  + *(p + 1) - *(p + 2);
}
```

What value is stored in variable x above after calling function f?

Ans: -2

##### Q2. POINTERS IN STRING 
In the program fragment below, what is the string stored in "str" after calling function f?

```C
void f(char *);

int main() {  
    char str[] = “cats”;    
    f(str);  
}

void f(char *c) {  
    while(*c) {        
	    (*c)++;
	    c++;    
	}  
}
```

##### Q3. STRUCTURE AND POINTER
![[Pasted image 20220821135702.png]]

**Idea:** Array address = address of the first element.

##### Q4. Palindrome checker 

> [!Question]
> A palindrome is a series of characters that reads the same way from left to right and right to left. 
> Examples: level, rotor, kayak, Able was I I saw Elba. Notice that  capitalization does not matter.  
>
> **Part 1:**
> Write a palindrome checker in C that:
> a. Reads in a string from the user (may contain spaces and mixed capitalization)  
> b. Prints “YES it is a palindrome” if the input string is a palindrome, or “NO it is not  palindrome” otherwise.  
> c. Uses array indexes to solve this problem.  
> **Part 2:** Solve using pointers and pointer arithmetic.

```C
#include <stdio.h>
#include <string.h>
#define SIZE 1024

void palindrome_checker() {
    char str[SIZE];
    printf("Enter your words: ");
    fgets(str, SIZE, stdin);
    
    // remove enter key
    int len = strlen(str);
    if (str[len - 1] == '\n') {
	    str[len - 1] = '\0';
    }

	len = strlen(str); // new len (shorter by 1) 
	
	// check if palindrom iteratively
    int left = 0, right = len - 1;    
    while (left < right) {
        if (str[left] != str[right]) {
            printf("false");
            return;
        } 
        left++;
        right--;
    }
    printf("true");

	// Using pointers
	while (l_ptr < r_ptr) {
        if ((*l_ptr) != (*r_ptr)) {
            printf("false");
            return;
        } 
        l_ptr++;
        r_ptr--;
    }
    printf("true");
	
}

int main() {
    palindrome_checker();
}
```







