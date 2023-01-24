---
tags: programmingLanguage
aliases: 
---
Date:: 2022-08-03 Wednesday
Links: [[CS2109S]]
- - -
# Python

### Main Points

Python is a weakly typed language, which means variables are not required to be assigned to a type.

Python is an interpreted language, which means **the source code of a Python program is converted into bytecode that is then executed by the Python virtual machine**. Python is different from major compiled languages, such as C and C + +, as Python code is not required to be built and linked like code for these languages. (Basically, no need compilation)

Additional Resourses:
https://docs.python.org/3/tutorial/datastructures.html

### Number

##### Common Operations

```Python
x + y      Add
x - y      Subtract
x * y      Multiply
x / y      Divide (produces a float)
x // y     Floor Divide (produces an integer)
x % y      Modulo (similar but not remainder)
x ** y     Power
x << n     Bit shift left
x >> n     Bit shift right
x & y      Bit-wise AND
x | y      Bit-wise OR
x ^ y      Bit-wise XOR
~x         Bit-wise NOT
abs(x)     Absolute value
```

Additional math functions can be found in math module:

```Python
import math
a = math.sqrt(x)
b = math.sin(x)
c = math.cos(x)
d = math.tan(x)
e = math.log(x)
```

##### Converting numbers

```Python
a = int(x)    # Convert x to integer
b = float(x)  # Convert x to float
```

```
>>> a = 3.14159
>>> int(a)
3
>>> b = '3.14159' # It also works with strings containing numbers
>>> float(b)
3.14159
>>>
```

### Conditional
- If-else statements:
```Python
if (cond):
	...
elif (cond):
	...
else:
	...
```

- && and || are replared by `and` and `or`

### Input/Output

```Python
username = input("Enter username:")  
age = int(input("Your age: "))
print("Username is: " + username)
```

### For loops

```Python
# Loop through each fruit in fruits list
fruits = ["apple", "banana", "cherry"]  
for x in fruits:  
  print(x)

# Loop through the letters in the word "banana":
for x in "banana":  
  print(x)

# range function, range(x) gives [0, x)
for x in range(6):  
  print(x) # 0, 1, 2, 3, ..., 5

# from 2 to 5
for x in range(2, 6):  
  print(x)

# increment the sequence with 3 (default is 1):
for x in range(2, 30, 3):  
  print(x) # 2, 5, 8, ...29

# Print all numbers from 0 to 5, and print a message when the loop has ended:
for x in range(6):  
  print(x)  
else:  
  print("Finally finished!")
# The `else` block will NOT be executed if the loop is stopped by a `break` statement
```

### String

There is no difference between using single (‘) versus double (“) quotes. _However, the same type of quote used to start a string must be used to terminate it_.

##### String Indexing

Strings work like an array for accessing individual characters. You use an integer index, starting at 0. 

Negative indices specify a position relative to the end of the string.

```Python
a = 'Hello world'
b = a[0]          # 'H'
c = a[4]          # 'o'
d = a[-1]         # 'd' (end of string)
```

You can also slice or select substrings specifying a range of indices with `:`.

```Python
d = a[:5]     # 'Hello'
e = a[6:]     # 'world'
f = a[3:8]    # 'lo wo'
g = a[-5:]    # 'world'
```

##### String Operation

```Python
# Concatenation (+)
a = 'Hello' + 'World'   # 'HelloWorld'
b = 'Say ' + a          # 'Say HelloWorld'

# Length (len)
s = 'Hello'
len(s)                  # 5

# Membership test (`in`, `not in`)
t = 'e' in s            # True
f = 'x' in s            # False
g = 'hi' not in s       # True

# Replication (s * n)
rep = s * 5             # 'HelloHelloHelloHelloHello'
```

More:
```Python
s.endswith(suffix)     # Check if string ends with suffix
s.find(t)              # First occurrence of t in s
s.index(t)             # First occurrence of t in s
s.isalpha()            # Check if characters are alphabetic
s.isdigit()            # Check if characters are numeric
s.islower()            # Check if characters are lower-case
s.isupper()            # Check if characters are upper-case
s.join(slist)          # Join a list of strings using s as delimiter
s.lower()              # Convert to lower case
s.replace(old,new)     # Replace text
s.rfind(t)             # Search for t from end of string
s.rindex(t)            # Search for t from end of string
s.split([delim])       # Split string into list of substrings
s.startswith(prefix)   # Check if string starts with prefix
s.strip()              # Strip leading/trailing space
s.upper()              # Convert to upper case
```

Strings are immutable → **All operations and methods that manipulate string data, always create new strings.** → O(N^2) operations.

### List

```Python
arr = [1, 2, 3]     # Creates a list
print(arr[2])       # Accesses the element at index 2 (0- indexed); prints 3
print(arr[-1])      # Accesses the element at the last index ; prints 3
arr[1] = 'foo'      # Re - assigns the value at index 1 to 'foo'
arr.append(4)       # Adds a new element 4 to the end of the list
x = arr.pop()       # Removes and returns the last element
y = arr.pop(1)      # Removes and returns the element at index 1
print(x, y)         # Prints '4 foo'
arr = [ None ] * 3  # Creates the list [None, None, None]
print(arr)

# we can slice the list:
arr = [1, 2, 3, 4, 5] # Creates a list
print(arr[1:3])       # Prints [2, 3]
print(arr[2:])        # Prints [3, 4, 5]
print(arr[:3])        # Prints [1, 2, 3]
arr[2:] = [5]        
print(arr)            # Prints [1, 2, 5]

# tuples are immutatable list
t = (1 , 'cool')                  # Declares a tuple containing two elements
print (t[0], t[1], sep=" ... ")   # Prints "1 ... cool "


# get the size of list
print(len(arr)) # 3

```

##### Common fatal error

```python
i = [1, 2, 3, 5, 8, 13]
j = []
k = 0

for l in i:
    j[k] = l    # IndexError: list assignment index out of range
    k += 1
```

I get an error message that says `IndexError: list assignment index out of range`, referring to the `j[k] = l` line of code. Why does this occur? How can I fix it?

**ANS:**
`j` is an empty list, but you're attempting to write to element `[0]` in the first iteration, which doesn't exist yet.

Use `append` instead, to add a new element to the end of the list:

```python
for l in i:
    j.append(l)
```

Of course, you'd never do this in practice if all you wanted to do was to copy an existing list. You'd just do:

```python
j = list(i)
```

Alternatively, if you wanted to use the Python list like an array in other languages, then you could pre-create a list with its elements set to a null value (`None` in the example below), and later, overwrite the values in specific positions:

```python
i = [1, 2, 3, 5, 8, 13]
j = [None] * len(i)
#j == [None, None, None, None, None, None]
k = 0

for l in i:
   j[k] = l
   k += 1
```

>[!Important]
> The thing to realise is that a `list` object will not allow you to assign a value to an index that doesn't exist.

### Aliasing

Varibles pointing to the same object (same reference).
We can use `is` to check if 2 variables are aliases.

The == operator compares the **equality** of two objects (same value), whereas the Python `is` operator checks whether two variables point to the same object in memory (same reference).

```Python
a = [1, 2, 3]
b = [1, 2, 3]

print(a == b) # True
print(a is b) # False

c = a         # Now , c points to the same object as a
print(a == c) # True
print(a is c) # True
```

To do a **shallow copy:**

```Python
a = [1, 2, 3]
c = a.copy()
c[0] = 'hello'
print(a) # Prints [1, 2, 3]
print(c) # Prints ['hello', 2, 3]

# Another way to do a list shallow copy:
b = list(a)
```

To do a **deep copy:** we use `copy.deepcopy(...)`

```Python
import copy

print('Shallow copy')
a = [[1, 2], [3, 4]]
b = a.copy() # Performs a shallow copy of variable a
b[0][0] = 5  # Modifies both a and b
print(a)     # Prints [[5, 2], [3, 4]]
print(b)     # Prints [[5, 2], [3, 4]]

print('Deep copy')
x = [[1, 2], [3, 4]]
y = copy.deepcopy(x) # Performs a deep copy of variable x
y[0][0] = 5          # Modifies y only
print(x)             # Prints [[1, 2], [3, 4]]
print(y)             # Prints [[5, 2], [3, 4]]
```

### Swapping Variables

```Python
a = 1
b = 2
a, b = b, a # No need to use temp variable
print(a) # Prints 2
print(b) # Prints 1
```

### Lambda Function

```Python 
def increment_by_one(x):
    return x + 1
print(increment_by_one(2108))   # Prints 2109

# or we can use lambda (anonymous) function
print((lambda x : x + 1)(2108)) # Prints 2109
```

### Map

```Python
a = [1, 2, 3, 4]
b = []

for i in range(len(a)):
    b.append(a[i] + 1)

c = list(map(lambda x : x + 1, a)) # Equivalent to for loop above

print(b == c)                      # Prints True
```

>[!important]
>As `map` is an iterator, we need to call `list` if we want the result to be returned as a list.

We can also pass more than 1 lists into map:

```Python
a = ["hello", "bye"]
b = ["world", "cat"]

c = list(map(lambda x, y: x + y, a, b))
print(c) # Prints ['helloworld', 'byecat']
```

### Filter

```Python
a = [1, 2, 3, 4]
filtered_1 = []
for i in range(4):
    if a[i] % 2 == 0:
        filtered_1.append(a[i])

filtered_2 = list(filter(lambda x : x % 2 == 0, a)) # Equivalent as for loop above
print(filtered_1 == filtered_2)                     # Prints True
```

### [[Numpy Basics]]
