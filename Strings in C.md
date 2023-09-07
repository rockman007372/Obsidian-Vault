We can turn an *array of characters* into a `String` by adding a null character `\0` at the end of the array. Without this termination char, a lot of functions wont work!

The null character `'\0'` is a character with an ASCII value of `0`. It is not the same as the digit character `'0'`, which has an ASCII value of `48`. 

```c
char str[6];

str[0] = 'e';
str[1] = 'g';
str[2] = 'g';
str[3] = '\0';

// str = ['e', 'g', 'g'], length = 3

// 2 ways to initialise string
char fruit_name[] = "apple";               // using string literals
char fruit_name[] = {'a', 'p', ..., '\0'}; // array initialiser

// not an string, no termination!!
char chars[4] = {'a', 'b', 'c', 'd'}; // just a char array
```

When you define a string literal in C using double quotes, such as `"hello"`, the compiler automatically appends a null character at the end of the string. This means that the actual array of characters representing this string in memory is `{'h', 'e', 'l', 'l', 'o', '\0'}`.

When working with strings in C, it’s important to remember to include space for the null character when allocating memory for a string. For example, if you want to store a string with `n` characters, you need to allocate an array of size `n+1` to hold the string and its null terminator.

We can use string functions by including `<string.h>` to manipulate strings.
## Strings I/O

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

## String Functions

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