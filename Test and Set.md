
```python
TestAndSet Register, MemoryLocation
```

1. Load the content at address `MemoryLocation` into register
2. Stores a 1 into `MemoryLocation`

These 2 operations are performed in **one single operation** / atomic. This prevents unsynced operations due to interleaving processes.

Pseudo-code of implementing CS using TestAndSet:

```C
void enterCS(int *Lock) {
	while (TestAndSet(Lock) == 1); // if lock content == 1, wait
}

void exitCS(int *Lock) {
	*Lock = 0; 
}
```