![[Pasted image 20231024123704.png]]

- Free memory space is known as **hole**.
- **External fragmentation**: Unused holes that are individually too small for processes, but can be merged by moving occupied partitions.
- Need to maintain info in OS and take more time to locate holes.

If we use dynamic partition, we need a **Partition Allocation Algorithm**:
- First-fit: take the first hole that is large enough for process
- Best-fit: take the smallest hold that is large enough
- Worst-fit: take the largest hole (maximize the size of the remaining hole, reduce external fragmentation)

We need an efficient way to store an retrieve information about the holes and partitions:
1. Standard **linked-list** of holes and partitions: O(N) for each insert to find hole ![[Pasted image 20231029125756.png]]

2. [[Buddy-System]] (some form of binary tree) ![[Pasted image 20231029125841.png]]
3. Bitmap: Each bit represents a byte in memory. Bit is 1 if byte is occupied.