
## Problems vs Instances

- A problem is an infinite set of instances $\set{I_1, I_2, I_3,...}$
- An instance is the **input** of a problem.

Example:
- An instance of Bipartite Matching is a bipartite graph ((U, V), E), and an integer k. 
- The solution to this instance is “YES” if the graph has a matching of size ≥ k, and “NO” otherwise
## Strategies

1. Simple equivalence ⇔ 
2. Special case to general case
3. Encoding with gadgets

Using these strategies, you can prove that:

3-SAT $\leq_p$  Independent Set $\equiv_p$ Vertex-Cover $\leq_p$ Set-Cover


### Simple Equivalence

Big idea: Prove that any instance of A can be converted to any instance of B, and vice versa.

Example: Prove Independent Set $\equiv_p$ Vertex-Cover 

![[Pasted image 20231106161830.png]]

An **independent set** of a graph: 
- a set of vertices where there is no edge between any 2 vertices in the set.
- Decision problem: is there an independent set of size $\geq k$?
- Search problem: what is the **maximal** independent set (max number of nodes before 2 node of an edge exist in the set)

A **vertex cover** of a graph (V, E): 
- a set of vertices such that for each edge in E, there exists at least one endpoint in the set.
- Decision problem: is there a vertex cover of size $\leq k$?
- Search problem: what is the **minimum** vertex cover (least number of nodes to "cover" every edge)


>[!strategy]
> To prove Independent Set $\equiv_p$ Vertex-Cover, we prove S is an independent set iff V - S is a vertex cover.

### Reduction from Special Case to General Case

Big idea: Prove that any instance of A can be reduced to a particular instance of B. Then prove that that B instance has an answer ⇔ that A instance has an answer.

Example: prove Vertex-Cover $\leq_p$ Set-Cover

Set-Cover:
- Given a set $U$ of n elements
- Given a collection of $S_i$ subsets of U
- Given an integer k
- Is there a collection of subsets such that $|collection| \leq k$ and the union of these sets is $U$?
- In other word, what is the minimum number of subsets such that the union is $U$?

>[!Strategy]
> Given **any instance** of a vertex cover, we can construct an instance of a set-cover whose size equals the vertex cover instance.

An instance of a vertex cover problem is a graph (V, E) and k. These are the **inputs** to the problem.

1. Create a set-cover instance:
	- U = E = all the edges in the graph.
	- $S_{v}= \set{ (u, v) \in E }$ = set of edges incident to node v.

2. Prove there exists a vertex-cover instance of size $\leq k$ **iff** there exists a set-cover instance of size $\leq k$

### Reduction via Gadgets

Example: Prove 3-SAT $\leq_p$  Independent Set

![[Pasted image 20231107091622.png]]

Strategy: 
1. Construction of graph G of triangles. Each vectices on the triangle represent a literal in the clause. Also connect literals to its negations.
2. Prove there exists an independent set of size $|\phi| \iff$ there exists a valid assignment for $\phi$. (A valid assignment of literals such that the equation is true)
