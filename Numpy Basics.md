---
tags: programming, computerScience
aliases: 
---
Date:: 2022-08-13 Saturday
Links: [[Introduction to Python]]
- - -

## Introduction
NumPy is a commonly used package for multidimensional array manipulation.

**Why Numpy:**
- In machine learning problems, large amount of data is usually present, necessitating approaches that make manipulating them easy and fast. 
- One such approach is to represent our data as multidimensional arrays before manipulating them.
- Implementation of the operations available in NumPy are often *optimised for performance*. As a result, using these operations, as opposed to iterative approaches, to manipulate elements in the array will often *lead to more performant code*.

## Basic Functions

### Import

```Python
import numpy as np
a = np.arange(5) # Note that here we use `np` instead of `numpy`
```

### Initialize NumPy Arrays

Arrays are objects in numPy that represent multidimensional arrays. Such arrays have the data type `numpy.ndarry` or `np.ndarray` for short.

Unlike Python lists, NumPy arrays  *cannot store data of different types*.

```Python
import numpy as np

a = np.array([1, 2, 3]) # Create 1D array vector
print(a.shape)          # Prints (3, ) → 1D
print(a[0], a[1], a[2]) # Prints 1, 2, 3
a[0] = 9                # Change the zeroth element to 9
print(a)                # Prints [9 2 3]

b = np.array([[1, 2, 3], [4, 5, 6]])  # Creates 2D array (matrix)
print(b.shape)                        # Prints(2, 3)
print(b[0, 0], b[1, 1], b[0, 2])      # Prints 1, 5, 3
```

We can also pre-filled arrays with a specified shape:

```Python
a = np.zeros((3, 3))        # Create 3x3 matrix with all zeros
b = np.ones(2)              # Create vector of size 2 with all ones
c = np.ones((3, 3))         # Create 3x3 matrix with all ones
d = np.full((2, 3), False)  # Create a constant array
e = np.arange(5)            # Creates a 1D array with values [0, 5)

print('Object a')
print(a)
print('Object b')
print(b)
print('Object c')
print(c)
print('Object d')
print(d)
print('Object e')
print(e)
```

```
Object a
[[0. 0. 0.]
 [0. 0. 0.]
 [0. 0. 0.]]
 
Object b
[1. 1.]

Object c
[[1. 1. 1.]
 [1. 1. 1.]
 [1. 1. 1.]]

Object d
[[False False False]
 [False False False]]

Object e
[0 1 2 3 4]
```

More info [here](https://numpy.org/doc/stable/user/basics.creation.html#arrays-creation)

### Indexing

Accessing the value of an element in a NumPy array is similar to that of lists in Python. However, observe that in the following, instead of doing something like `a[i][j]`, we have `a[i, j]`.

```Python
import numpy as np

a = np.array([[1, 2, 3], [4, 5, 6]])
print(a[0, 0])                       # Prints 1
print(a[1, 2])                       # Prints 6
```

### Slicing

```Python
import numpy as np

a = np.array([[1, 2, 3, 4], [4, 5, 6, 7]])

print(a[0, 1:3])                            # Prints [2, 3]

print(a[:, 1:3])                            # Prints [[2 3]   
                                            #         [5 6]]
```

Do be careful of aliasing.  Modify a shallow copy can change values of the original array.

```Python
b = a                                       # Aliasing
b[0, 0] = 5
print(a[0, 0])                              # Prints "5"
```

**Integer Array Indexing**: Using an integer array to index the numpy
```python
import numpy as np

a = np.array([[1, 2, 3], [4, 5, 6]])

print(a[:, [0, 2]])                   # Prints [[1 3]
                                      #         [4 6]]

print(a[[1, 0], [1, 2]])              # Prints [5 3]
# This means we are returning a[1, 1] and a[0, 2]

# Example: return the centroid of each sample based on the labels (map sample to cluster) and clusters (map cluster to centroid)
centroids = clusters[labels]
```

**Boolean Array Indexing**: Using a boolean array to index
```python
import numpy as np

a = np.array([4, 3, 1, 5, 10])

desired_indices = a > 3

print(desired_indices)           
# prints [ True False False  True  True]        

print(a[desired_indices])        
# Selects values in `a` that are
# greater than 3; prints [ 4  5  10 ]

# Shortform:
b = a[a > 3]

```

### Reshape
Follow this [link](https://www.codingem.com/numpy-reshape-minus-one/) for in-depth tutorial.

### Element-wise Operation

```Python
x = np.array([[1,2],[3,4]])
y = np.array([[5,6],[7,8]])

print(x + y)                   # Prints [[ 6  8]
                               #         [10 12]]

print(x * y)                   # Prints [[ 5 12]
                               #         [21 32]]
```

**Note:** This is element-wise operation, not matrix operation!

### NumPy NaN

NaN is short for **Not a number**. It is used to represent entries that are undefined. It is also used for representing missing values in a dataset.

NaN is a special floating-point value which cannot be converted to any other type than float.

```Python
import numpy as np

arr = np.array([1, np.nan, 3, 4, 5, 6, np.nan])

print(arr)
```

Output: `[ 1. nan  3.  4.  5.  6. nan]`

Some operations on NaN:

```Python
print(arr.sum()) # nan
print(arr.max()) # nan
```

We have to use some special functions that **ignore nan**:

```python
np.nansum(arr) # 19.0
np.nanmax(arr) # 6.0 
```

### Axis

![[Pasted image 20220817150856.png]]

```python
import numpy as np

a = np.array([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])

# [
#   [[1, 2], [3, 4]],
#   [[5, 6], [7, 8]]
# ]

print(np.sum(a, axis=0))      # Prints [[ 6,  8],             
                              #         [10, 12]]

print(np.sum(a, axis=1))      # Prints [[ 4,  6],
                              #         [12, 14]]

print(np.sum(a, axis=2))      # Prints [[ 3,  7],
                              #         [11, 15]]
```

### Broadcasting

Broadcasiting allows us to apply arithmetic operations to arrays with **different shapes**. 

Imagine the smallers arrays being "stretched ;)" to accomodate the dimensions of the bigger array.

```python
import numpy as np

a = np.array([[1, 2, 3], [4, 5, 6]])

b = np.array([[0, 1, 2]])

c = np.array([[0, 1, 2], [0, 1, 2]])

d = np.full((2, 3), 5)

print(a + b)                           # Prints [[1 3 5]
                                       #         [4 6 8]]
                                       # Equivalent to a + c

print(a + 5)                           # Prints [[ 6,  7,  8],
                                       #         [ 9, 10, 11]]
                                       # Equivalent to a + d
```

![[Pasted image 20220817154025.png]]

When operating on two arrays, NumPy compares their shapes element-wise. It starts with the trailing (i.e. rightmost) dimensions and works its way left. Two dimensions are compatible when:
1.  they are equal, or
2.  one of them is 1

```Python
Image  (3d array): 256 x 256 x 3
Scale  (1d array):             3
Result (3d array): 256 x 256 x 3
```

```C
A      (4d array):  8 x 1 x 6 x 1
B      (3d array):      7 x 1 x 5
Result (4d array):  8 x 7 x 6 x 5
```

### Numpy.newaxis 

We use `np.newaxis` to add dimension to array:

![[Pasted image 20220816233452.png]]

`None` is also allowed because `numpy.newaxis` is merely an alias for `None`.

```python
In [1]: import numpy

In [2]: numpy.newaxis is None
Out[2]: True
```

Suppose we want to create a 3x2 matrix from a (3, ) matrix and (2, ) matrix:

```python
a = np.array([4, 5, 6])
b = np.array([1, 2])
c = a[:, None] + b[None, :]     
# create 3 x 1 and 1 x 2 matrices

print(c)                        # Prints [[5 6]
                                #         [6 7]
                                #         [7 8]]
```

Alternatively, we can use `reshape` , and *NOT transform b at all*:

```python
c = a.reshape((3, 1)) + b
```

### Matrix Multiplication

To perform matrix multiplication on two NumPy arrays, we use the syntax `@`. In particular, if we want to multiply array `A` and `B`, we will do `A @ B`.

The specifics of this operations is as follow:
- if A and B are both 2D, they are multiplied like conventional matrices.
- if one of them is N-D, with N > 2, that matrix is treated as a stack of matrices. Broadcasting will be done where necessary.

```Python
'''
a = matrix of size 2 x 3 x 4
b = matrix of size 4 -> Broadcast: 1 x 1 x 4

a @ b -> matrix multiplication is done on axis 2
'''
```

