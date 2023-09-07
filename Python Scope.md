---
tags: Python
aliases: 
date: 2023-01-11 Wednesday
---

## Main Points

Based on the scope, we can classify Python variables into three types:

1.  Local Variables
2.  Global Variables
3.  Nonlocal Variables

## Python Local Variables

When we declare variables inside a function, these variables will have a local scope (within the function). We cannot access them outside the function.

These types of variables are called local variables. For example,

```python
def greet():
    # local variable
    message = 'Hello'
    print('Local', message)

greet()

# try to access message variable 
# outside greet() function
print(message)
```

**Output**

```
Local Hello
NameError: name 'message' is not defined
```

## Python Global Variables

In Python, a variable declared outside of the function or in global scope is known as a global variable. This means that a global variable can be accessed inside or outside of the function.

Let's see an example of how a global variable is created in Python.

```python
# declare global variable
message = 'Hello'

def greet():
    # declare local variable
    print('Local', message)

greet()
print('Global', message)
```

**Output**

```
Local Hello
Global Hello
```

This time we can access the message variable from outside of the `greet()` function.

**However, we can only access but cannot modify a global variable from within a function:**

```python
# global variable
c = 1 

def add():
     # increment c by 2
    c = c + 2
    print(c)

add()
```

**Output**

```
UnboundLocalError: local variable 'c' referenced before assignment
```

To modify global variable within a function, we have to use the keyword `global`

```python
# global variable
c = 1 

def add():

    # use of global keyword
    global c

    # increment c by 2
    c = c + 2 
    print(c)

add()

# Output: 3 
```

### Rules of global Keyword

The basic rules for `global` keyword in Python are:

-   When we create a variable inside a function, it is local by default.
-   When we define a variable outside of a function, it is global by default. You don't have to use the `global` keyword.
-   We use the `global` keyword to read and write a global variable inside a function.
-   Use of the `global` keyword outside a function has no effect.

## Python Nonlocal Variables

In Python, nonlocal variables are used in **nested functions** whose local scope is not defined. This means that the variable can be neither in the local nor the global scope.

We use the `nonlocal` keyword to create nonlocal variables.For example,

```python
# outside function 
def outer():
    message = 'local'

    # nested function  
    def inner():

        # declare nonlocal variable
        nonlocal message

        message = 'nonlocal'
        print("inner:", message)

    inner()
    print("outer:", message)

outer()
```

**Output**

```
inner: nonlocal
outer: nonlocal
```

In the above example, there is a nested `inner()` function. We have used the `nonlocal` keywords to create a nonlocal variable.

The `inner()` function is defined in the scope of another function `outer()`.

> [!Note] 
> If we change the value of a nonlocal variable, the changes appear in the local variable.

---
Links: [[Introduction to Python]]
