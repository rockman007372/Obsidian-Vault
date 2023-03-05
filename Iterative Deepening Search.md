- Core idea: DFS simulating BFS
- This is a general strategy used in combination with DFS tree search that finds the best depth limit. 
- The algorithm does this by gradually increasing the depth (first 0, then 1, then 2, and so on) until a node is found. 
- This occurs when the depth limit reaches _d_, the depth of the shallowest goal-node. Iterative deepening **combines the benefits of DFS and BFS**.

![[Pasted image 20220820153317.png]]

 ![[Problem-Solving Agents in AI 2022-08-20 15.41.09.excalidraw]]

## Properties

**Complete:** Yes, no depth limit, reach goal node eventually if it exists.

**Time Complexity:** $O(b ^ d)$
- zero level is searched d + 1 times, 1st layer is searched d  times, 2nd layer is searched (d - 1) times....
- This can seem wasteful because states are generated multiple times. But it turns out this is not too costly, this is because in a search tree with the same (or nearly the same) branching factor at each level, *most of the nodes are in the bottom level* and hence dominate the upper level in time complexity.$$(d+1)b^{0} + db^{1}+ (d - 1)b^{2}+ ... + b^{d} = O(b ^ d)$$


**Space:** O(bd) 
- max size of stack at anytime - NOT O(bm)!

**Optimal**: Yes **only if step costs are all identical**

## Compared to BFS

![[Pasted image 20220820155246.png]]

⇒ Does better because other nodes at depth d are not expanded.

## Compared to DFS

![[Pasted image 20220820155637.png]]

⇒ Overhead (The amt of repeated work we have to search) is not that bad!

>[!Note]
> In general, ID-DFS is the preferred uninformed-search method when the search space is large and the depth of the solution is not known.
