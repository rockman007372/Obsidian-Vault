**Sequential Consistency (SC)** is a **memory consistency model** that ensures that the execution of operations in a **multi-threaded** program appears in a global order that **respects program order**.

🔹 **Definition (Leslie Lamport, 1979)**:

> “A multiprocessor system is **sequentially consistent** if the result of any execution is the same as if the operations of all the processors were executed in **some sequential order**, and the operations of each individual processor appear in this sequence in the **order specified by its program**.”

---

### **1️⃣ What Does This Mean?**

- Every thread **executes its instructions in order**.
- All threads observe the same **global order** of memory operations.
- The system does not **reorder** operations across different threads.

🔹 **Example (Expected Sequentially Consistent Execution)**

```C++
int x = 0, y = 0;
bool a = false, b = false;

void thread1() {
    x = 1;
    a = (y == 1);
}

void thread2() {
    y = 1;
    b = (x == 1);
}
```


📌 **Possible SC Orderings**:

1. `thread1: x = 1` → `thread2: y = 1` → `thread1: a = (y == 1)` → `thread2: b = (x == 1)`
2. `thread2: y = 1` → `thread1: x = 1` → `thread1: a = (y == 1)` → `thread2: b = (x == 1)`

📌 **Impossible in SC**:

- `a == false && b == false` (because either `x=1` or `y=1` must be seen by the other thread)

---

### **2️⃣ How Modern CPUs Violate SC**

- **Out-of-Order Execution**: CPUs **reorder** instructions to improve performance.
- **Compiler Optimizations**: The **compiler** may reorder operations if it does not see dependencies.
- **Memory Caching & Write Buffers**: Stores to memory may be **delayed** and not visible to other threads immediately.