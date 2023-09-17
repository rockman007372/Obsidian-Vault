![[Pasted image 20230910105317.png]]

>[!definition]
> A graph in which every edge has one red end and one blue end.

Its not obvious if a graph is bipartite. Hence we need to find algorithm to prove bipartiteness.

![[Pasted image 20230910105502.png]]

>[!lemma 1]
> If a graph is bipartite, it cannot contain an **odd** length cycle.

Prove: it is impossible to 2-color the odd cycle.

>[!Lemma 2]
> Let G be a connected graph.
> Let $L_0$, $L_1$ ... be the layers produced by BFS on root node s.
> Exactly **one** of the following holds:
> - No edge of G joins 2 nodes of the same layer, and **G is bipartite**
> - An edge of G joins 2 nodes of the same layer, and **G is not bipartite**

Prove (i): color odd and even layers differently
Prove (ii):

![[Pasted image 20230910110218.png]]

- Consider cycle (x, y, z): its length is 1 + (j - i) + (j - i) = 1 + 2k = odd
- Hence there is an odd length cycle => not bipartite

>[!Corollary]
> A graph G is bipartite **iff** it contains no odd length cycle.

Use this corollary to prove if a graph is bipartite or not!