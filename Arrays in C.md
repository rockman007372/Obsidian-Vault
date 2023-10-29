
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
When an array name `a` appears in an expression, it refers to the *address of the first element* (`a[0]`) of that array → Array name is pointer! → Array is passed ard "by reference"!

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

Why can we **NOT directly assign** an array to another array
- An array name is a **fixed pointer**; It points to the first element of the array, and this cannot be altered.
- In the code above, we try to alter `dest` so it points somewhere!

We can also use `<string.h>` library function `memcpy()` to copy array.

#### Array Parameters in Functions

Array name is a pointer, hence array can be passed "by reference" to the function. This allows the function to access and modify array elements directly.

```C
int sumArray(int [], int); // function prototype

int main(void) {
	int val[3] = {1, 2, 3};
	return sumArray(val, 3);
}

int sumArray(int arr[], int size) {
	int i, sum = 0;
	for (i = 0; i < size; i++) {
		sum += arr[i];
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

int sumArray(int *arr, int size) {

}
```

#### Modifying Array in a Function

To modify an external variable from a function, we have to pass the address of the variables into the function. EG: `func(&v);`

But since an **array name is already a pointer**, there is no need to pass its address to the function → function can modify the content of any array it receives.

---