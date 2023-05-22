A decent implementation of [[Union-Find]], based on the tree data structure of [[Quick Union]]. Under this implementation, all operations have O(lgN) run time.

Idea: 
- Maintain weight in the root of each connected component. 
- Low → High: When we union 2 objects, we connect the tree of lower weight to the tree of higher weight.

![[Pasted image 20220616144802.png]]

Result is a much flatter tree:

![[Pasted image 20220616144823.png]]


## Time complexity

Both Union and Find: O(logN). Traversing the tree to search and union only takes O(logN).

Big idea: We want to compress the tree as much as possible. The tree's height/depth increases only if the number of nodes doubles.

Use [[Induction]] to prove: 

``` 
A tree of height k will have size of at least 2^k nodes 
=> A tree of size N will have height of at most logN
```

>[!note]
> + Some prefer Union-by-Rank, Union-by-Height(?)
> + Same idea: height only increases when size/rank/weight double