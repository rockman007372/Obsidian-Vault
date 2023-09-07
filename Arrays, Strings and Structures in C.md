---
tags: processed
course: CS2100
type: lecture 
date: 2022-08-21 Sunday
---
Links: [[CS2100]]
- - -

## Content

1. [[Arrays in C]]
2. [[Strings in C]]
3. [[Structure in C]]

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







