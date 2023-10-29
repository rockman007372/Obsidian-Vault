![[Pasted image 20231024123704.png]]

- Free memory space is known as **hole**.
- **External fragmentation**: Unused holes that are individually too small for processes.
	- We can merge the holes by moving occupied partitions.
- Need to maintain info in OS and take more time to locate holes.

If we use dynamic partition, we need a **Partition Allocation Algorithm** (partition schemes):
- First-fit: take the first hole that is large enough for process
- Best-fit: take the smallest hold that is large enough
- Worst-fit: take the largest hole (why would u want this again?)

We need an efficient way to store an retrieve information about the holes and partitions.
- Standard linked-list of holes and partitions: O(N) for each insert to find hole

![[Pasted image 20231029125756.png]]

- Buddy-System (some form of binary tree)

![[Pasted image 20231029125841.png]]
