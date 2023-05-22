
We can further enhance the implementation of Union-Find in [[Quick Union]] by doing path compression during the **Find operation.**

Big idea: After we traverse up to find root, make the root the parent of visited nodes.

![[Pasted image 20220616150155.png]]

![[Pasted image 20220616150206.png]]

```Java
public int find(int i) { // path compression using recursion
	if (parent[i] != i) parent[i] = find(parent[i]); 
	return parent[i]; 
}
```

Time: O(lgN) for both union and find operation