Tags: [[Data Structure and Algorithm]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
A data structure for the purpose of combining (union) and finding **connected components** efficiently.

Example: Maze problems

![[Pasted image 20220616141859.png||600]]

- Union(A, B): connect 2 objects A and B
- Find(C, D): are C and D in the same connected component? 
- Connectivity is transitive.

>[!help]
> Union-Find class in JAVA: [[Disjoint Set]]

## Implementations

1. [[Quick Find]]
2. [[Quick Union]]
3. [[Weighted Union]]
4. [[Path Compression]]
5. [[Weighted Union with Path Compression]] - most optimized