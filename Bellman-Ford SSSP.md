---
tags: DataStructure, SSSP
date: 2022-08-03 Wednesday
---
Tags: [[SSSP]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   

## Usage

- Find the shortest distance between 2 nodes
- Find the shortest distance between a source and every other node
- Detect negative weight cycles

## Triangle Inequality

The algorithm is derived from the triangle inequality:

$$D(S, C) \leq D(S, A) + D(A, C)$$

## Algorithm

![[Pasted image 20220803141631.png]]

1. Initially, assign the estimates of every node to Infinity.
2. Let the estimate of the source be 0.
3. Relax every edge of the graph in random order.
4. Repeat for V - 1 iterations

```java

/** Updates the current estimate (minimum distance) of a node to the source, by making used of Triangle Inequality. */
void relax(int u, int v) {
	if (dist[v] > dist[u] + weight(u, v))
		dist[v] = dist[u] + weight(u, v);
}

n = V.length;
for (i = 0; i < n - 1; i++) {
	for (Edge e : graph) {
		relax(e)
	}
}
```

Note: 
- We can terminate early if one iteration does not change any estimates.
- Runtime: O(EV)
- Space: O(V) to keep `estimate` array

## Why must we iterate V - 1 times?

![[Pasted image 20220803142438.png]]
- After 1 iteration, the node *on the shortest path* that is one hop away has the correct estimate.
- After 2 iterations, the node *on the shortest path* that is 2 hop away has the correct estimate (by building on the previous 1-hop node)
- Hence, after at most n - 1 iterations, all the nodes must have the correct estimated distance from the source.


Key property: If P is the shortest path from S to D, and X is on path P, then P is also the shortest path from S to X.

>[!invariant 1]
> After n iterations, the n<sup>th</sup> node from the source on the **SHORTEST PATH TREE** has the correct estimate. 

>[!invariant 2]
>After n iterations, all the nodes **AT MOST** n hops away from the source have the correct estimate.
>
>![[Pasted image 20220803142317.png]]
>
> This does not mean EVERY node n-hop away from source has correct estimate at n iteration! (Dependent on order of relax) 

Since the correct estimate can only be found by relaxing every edge in the correct order (Breadth First Search order away from the source), we must relax for V - 1 iterations to ensure correctness.

## Special cases

- Bellman-Ford **cannot work** for negative weight edges due to **negative weight cycle** (as estimate will keep decreasing after every iteration) → Bellman-Ford can detect negative weight cycle by checking if estimates still change after V iterations.
- For unweighted graphs, just use [[Breadth First Search]].


- - -
See also: [[Path with Maximum Probability]]