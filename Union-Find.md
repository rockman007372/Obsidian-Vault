2022-06-16 14:15
Tags: [[Data Structure and Algorithm]] 
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   
### Definitions
A data structure for the purpose of finding and combining (union) connected components efficiently.

Example - Maze problems:
![[Pasted image 20220616141859.png||600]]

- Union(A, B): connect 2 objects A and B
- Find(C, D): are C and D in the same connected component? 
- Connectivity is transitive.

Union-Find class in JAVA: [[Disjoint Set]]

### Quick Find
Idea: 
+ Each object has a component identifier
+ Find: check if same component id
  
![[Pasted image 20220616143245.png||600]]

+ Union: go through the component id array to update the same component ids to the target id

![[Pasted image 20220616143352.png||600]]

Time:
+ Find operation: O(1)
+ Union operation: O(n)

### Quick Union 
Idea: 2 objects are in the same component if they are in the same tree (check if same root)

![[Pasted image 20220616143721.png]]

![[Pasted image 20220616143756.png]]

Time: 
+ Find and Union: O(n)
+ Bad performance, tree is not flat, union is expensive
+ Worse case: Linear union

### Weighted Union 
Idea: Maintain weight in the root of each connected component. When we union 2 objects, we connect the tree of lower weight to the tree of higher weight.

![[Pasted image 20220616144802.png]]

Result is a much flatter tree:

![[Pasted image 20220616144823.png]]

Time:
+ Both Union and Find: O(logN)
+ Use [[Induction]] to prove: 
``` 
A tree of height k will have size of at least 2^k nodes 
=> A tree of size N will have height of at most logN
```
+ Traversing the tree to search and union only takes O(logN).

Notes: 
+ Some prefer Union-by-Rank, Union-by-Height(?)
+ Same idea: height only increases when size/rank/weight double

### Path Compression - During Find
After we traverse up to find root, make the root the parent of visited nodes.

![[Pasted image 20220616150155.png]]

![[Pasted image 20220616150206.png]]

```Java
public int find(int i) { // path compression using recursion
	if (parent[i] != i) parent[i] = find(parent[i]); 
	return parent[i]; 
}
```

Time: O(lgN) for both union and find operation

### Weighted Union with Path Compression (MOST OPTIMIZED)
Almost constant time for both Find and Union

Final amortized time complexity is O(α(n)), where α(n) is the inverse Ackermann function, which grows very slowly.

Worst case run time is still O(lgN), but if we call m such calls consecutively, amortized run time is O(α(n)).

![[Pasted image 20220616150324.png]]