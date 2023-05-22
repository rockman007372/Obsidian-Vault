Another naive implementation of [[Union-Find]].

Idea: 2 objects are in the same component if they are in the **same tree** (check if same root)

![[Pasted image 20220616143721.png]]

![[Pasted image 20220616143756.png]]

## Time complexity

+ Find and Union: O(n)
+ Bad performance if tree is not flat, union is expensive
+ Worse case: Linear union