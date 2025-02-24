RAII ensures that **resources (memory, files, sockets, etc.) are acquired in a constructor and released in a destructor**.

### **How RAII Works**

- When an object **is created**, it **acquires** a resource.
- When the object **goes out of scope**, the destructor **automatically releases** the resource.
- This ensures **exception safety** and **prevents memory leaks**.

### **Example: Managing Heap Memory**

Without RAII:

```c
void func() {
    int* ptr = new int(5);
    // ... do something ...
    delete ptr; // Must remember to delete (risk of memory leak!)
}
```

With RAII:

```C
void func() {
    std::unique_ptr<int> ptr = std::make_unique<int>(5);
    // No need to manually delete
} // ptr is automatically deleted when func() ends

```
