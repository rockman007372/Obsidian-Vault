
- Need to dynamically allocate memory (acquire memory space during **execution time**)
- Need to set up a **heap memory region** in the free memory for this purpose.
- Heap grows downward dynamically. Hard to manage as it can leave holes in memory (allocate and deallocate memory spaces)
- In C, `malloc()` allows you to create memory dynamically.

```C
int main() { 
	int *a = NULL; 
	a = (int *) malloc(sizeof(int)); // address of the heap memory
	*a = 3; 
}
```