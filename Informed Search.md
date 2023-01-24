---
tags: processed
course: CS2109S
type: lecture
date: 2022-08-28 Sunday
---
Links: [[CS2109S]]
- - -
## Informed Search

An informed search strategy is one that uses problem-specific knowledge beyond the defintion of the problem itself to find solutions more efficiently than [[Uninformed Search]]. → We have some knowledge about which node is better to expand.

## Best-first Search

A Best-first Search algorithm is one where a node is selected for expansion based on an **evaluation function** `f(n)` → Expand most desirable nodes first.

Best-first is a **family** of search strategies, each with a *different* evaluation function.

Implementation: Order the nodes in frontier based on decreasing order of desirability using [[Priority Queue]].

Special cases:
- Greedy Best-first Search
- A* Search

The **choice of `f` determines the search strategy.**  (As it determines the order of expansion). Most Best-first search algorithms include a **heuristic function** `h(n)` .

>[!Definition]
> Heuristic Function `h(n)` = *estimated* cost of the *cheapest* path from the state at node `n` to a goal state.

An example of the heuristic function is $h_{SLD}(n)$ = straight line distance from n to Bucharest (The estimated shortest distance from city n to Bucharest).

## Greedy Best-first Search

Greedy Search expands the node that **appears** to be the closest to the goal. (May not be the least-cost path)

![[Pasted image 20220828113513.png]]

Properties:
- **Complete**: No
	- Yes only in finite spaces with repeated-state checking → Else can stuck in loop
- **Time**: $O(b^m)$ - may have to expand all nodes, but a good heuristic can give dramatic improvement.
- **Space**: $O(b^m)$ to keep all nodes in memory
- **Optimal**: No
	- Real cost is not the same as estimated cost!
	- ![[Informed Search 2022-08-28 11.41.41.excalidraw]]

## A* Search (BETTER)

Greedy Best-first search is **informed**, but almost always **suboptimal** and **incomplete**. Uniform Cost search is almost always **optimal** and **complete**, but **uninformed** → A* search combines the two by minimizing `f(n) = g(n) + h(n)`. The algorithm is identical to uniform-cost search except it uses `g + h` instead of `g`.

> [!Definition]
> `f(n) = g(n) + h(n)` where
> f(n) = evaluation function - estimated total cost of path through n to goal
> g(n) = cost to reach node `n` from source
> h(n) = estimated smallest cost of reaching goal node from `n`

- Idea: Avoid expanding paths that are *already expensive* → Allow fewer nodes to be popped/expanded before we reach the goal state
- Example:
	- ![[Pasted image 20220828115907.png]]
	- ![[Pasted image 20220828115923.png]]
	- ![[Pasted image 20220828120039.png]]
	- ![[Pasted image 20220828120154.png]]
	- ![[Pasted image 20220828120314.png]]
- Properties:
	- **Complete**: YES (unless there are infinitely many nodes with f $\leq$ f(G))
	- **Time**: Exponential
	- **Space**: $O(b^m)$ - may have to keep all nodes in memory → **VERY EXPENSIVE**
	- **Optimal**: YES, if heuristic is admissible or consistent.
- A* has conditions for optimality. These are **admissibility** and **consistency**.

### Optimality of A*
#### **Theorem 1:** If h(n) is admissible, A* using Tree-Search is optimal

A* search uses an **admissible** heuristic h(n).

>[!definition]
> h(n) is an admissible heuristic if $$\forall n, h(n) \leq h^{*}(n)$$ where $h^{*}(n)$ is the **true cost** from n to goal.
> 
> For example, $h_{SLD}(n)$ is an admissible heuristic because it **never overestimates** the actual road distance (any path from n to goal must be *greater or equal* to the shortest straight line distance from n to goal )

This means that `f(n)` also never overestimates the true cost of a solution along the current path through `n`. Admissible heuristics are optimistic by nature because they think the cost of solving the problem is less than it actually is.

Why does this make A* optimal?

![[Informed Search 2022-08-28 16.31.58.excalidraw]]

Hence, assuming we have C* as the real cost to reach the goal (obtimal goal):
- $A^*$ will expand all the nodes with $f(n) < C^*$
- $A^*$ will expand some nodes with $f(n) = C^*$
- $A^*$ will **NOT** expand nodes with $f(n) > C^*$ since these nodes are already too expensive given the heuristic.

Mathematical proof:
![[Pasted image 20220828163821.png]]

Assume G2 is in the frontier (already generated) and it is a subobtimal goal.

Let n be an unexpanded node also in the frontier such that n is on a shorter path to an optimal goal G.

```
f(G) = g(G) since h(G) = 0
f(G2) = g(G2) since h(G2) = 0

g(G2) > g(G) since G2 is subobtimal
⇒ f(G2) > f(G)

h(n) <= h*(n) since h is an admissible heuristic
⇒ h(n) + g(n) <= h*(n) + g(n)
⇒ f(n) <= f(G) < f(G2) (PROVEN)

Hence, n will always be expanded before G2, and G will be reached first! 
⇒ G2 will never be selected for expansion
```

#### **Theorem 2:** If h(n) is consistent, A* using Graph-Search is optimal

**Consistent Heuristic** is a stronger condition that is required only for applications of A* to graph search.

It is a form of general triangle inequality.

>[!definition]
> A heuristic is consistent if for every node `n`, every successor `n'` of n generated by any action a, $$h(n) \leq c(n, a, n') + h(n')$$
> One way to prove a heuristic is consistent is to prove heuristic never decreases by more than the cost of 1 move:$$h(n) - h(n') \leq c(n, a, n')$$

![[Pasted image 20220828164839.png]]

>[!Important] 
>If a heuristic is consistent, it is also admissible
>[Proof](https://cs.stackexchange.com/questions/63481/how-does-consistency-imply-that-a-heuristic-is-also-admissible)

Consistency vs Admissible?
- **In a tree**, the same goal node can never be reached from a different path, or else it will form a cycle → We need an **admissible** heuristic because once we reached the lowest-cost goal node, we will never explore **different** higher-cost goal nodes (since admissible heurisitic demands that the true cost to these other nodes will be greater than the lowest cost we found).
- **In a graph**, the same goal node can be reached through different paths! Hence, we need **consistent** heuristics to make sure extending the path will always lead to greater costs, hence there is no point extending → When a node `n` is selected for expansion, the optimal path to that node has been found!!

## Finding Heuristics

 How do we come up with a good heuristics? → **Relaxed problem!**

A problem with fewer restrictions on its actions is called a **relaxed problem**. 

This makes the state-space for the relaxed problem a _supergraph_ of the original state-space, because the removal of restrictions creates additional edges (i.e., there are more ways we can transition from one state to another since restrictions are removed). 

Any optimal solution in the original problem is, by definition, also a solution in the relaxed problem; but the relaxed problem may have _better_ solutions if the added edges provide short-cuts. Hence, _the cost of an optimal solution to a relaxed problem, is an admissible heuristic for the original problem_ (since it can _never_ overestimate). 

Also, since the derived heuristic is an exact cost for the relaxed problem, it must obey the triangle inequality and is therefore *consistent*. Why? Reason using consistent heuristic formula!

Example: *8-Puzzle game* 
- $h_{1}(n)$ = number of misplaced tiles
- $h_{2}(n)$ = total Manhattan distance (Number of squares away from desired location for each tile)

![[Pasted image 20220828172130.png]]

The heuristics _h1_ (misplaced tiles) and _h2_ (Manhattan distance) are fairly-good heuristics for the 8-puzzle problem. Looking at them closely, they are perfectly-accurate path-lengths for _simplified_ versions of the puzzle. 

For the first one, the rule is changed so that a tile could teleport anywhere instead of just to the adjacent empty square. Then, _h1_ gives us the exact number of steps in the shortest solution. 

If we changed the rule further such that we could move the tile one square in any direction, even to an occupied square, then _h2_ gives us the exact number of steps in the shortest solution. 

Using these heuristics, we can **prune** away paths that are less likely to be fruitful.

Not all admissible heuristics are equal! In the above example, `h2` is a better heuristic (h2 **dominates** h1) because `h2(n) >= h1(n)` for all n.

![[Pasted image 20220828172524.png]]

Another example: *Travelling saleman Problem*
- Original problem: Find the shortest tour visiting n cities exactly once Complexity: NP-complete 
- Relaxed problem: Find a tree with the smallest cost that connects the n cities (minimum spanning tree)
![[Pasted image 20220828173927.png]]

What if you have multiple heuristics? → Find **max** of all of them!
`h(n) = max(h1(n), h2(n), ...)`

## Memory-bounded Search

A* generally runs out of memory before it runs out of time.

Other best-first strategies keep the good properties on A* while trying to reduce memory consumption: 
- Iterative Deepening A* (IDA*)
- Recursive Best-First search (RBFS) 
- Memory-bounded A* (MA*)
- Simple Memory-bounded A* (SMA*)

Big idea is: **PRUNING**

## Iterative Deepening A* Search
Recall that we use [[Iterative Deepening Search]] to reduce the exponential space for BFS (which is a special form of uniform-cost search) to linear space!

Similarly, we can use **Iterative Deepening A* Search** to reduce space!
- Instead of using depth for cutoff, we use the f-cost (g + h)
- Remember the best f-value that exceed the cutoff.

## Recursive Best-first Search
- Keep track of 2nd best f-value seen thus far → Save space of storing every single children in PQ!
- Parent node keeps track of best f-value for children
- Backtrack when we end up at a node with *children worst than the 2nd best f-value* seen thus far

Criticism: Can be too stringy with memory - linear space severely underutilize memory

## Simplified Memory-bounded A*
- As long as memory is sufficient, we keep going
- At some point when memory is full:
	- Drop the nodes with the worst f-value
	- Update the parent quality of best path on dropped subtree??

## Local Search 

In many problems, *path to the goal is irrelevant* (e.g. 8 queens problem). What we usually care about is the final solution (goal state is solution). Hence, we don't need to store the path to the solution, but can simply *explore the solution space* to either maximize/minimize the objective function.
- The state space is a set of *complete configurations*
- An **evaluation function h** must be available that measures the quality of each state → In the 8 queens problem, h = number of non-attacking queens
- Main Idea: Start with a random initial configuration and *make small, local changes* to it that improve its quality
- Why use Local Search over Classical Search?
	- Low memory requirement
	- Effective even in extremely large state spaces
	- Sometimes there is no solution - just want to minimize constraint violations.

## Hill Climbing Search
![[Pasted image 20220906162559.png]]

![[Pasted image 20220906163624.png]]

This is a simple search algorithm that simply loops and moves in the direction of increasing value (uphill). It will terminate when it reaches a peak (i.e., a point where none of the neighbors have a higher value). This algorithm is also known as **greedy local search**. Unfortunately, hill climbing will get stuck for the following reasons:

-   **Local maxima**
-   **Ridges** (sequence of local maxima that is very difficult for greedy algorithms to navigate)
-   **Plateaux** (flat area).

![[Pasted image 20220906163659.png]]


There are variations to get around these difficulties:

-   **Stochastic hill climbing** chooses at *random* from *among the uphill moves*; the probability of selection can vary with the steepness of the uphill move. This usually converges more slowly than steepest ascent, but in some state landscapes, it finds better solutions.
-   **First-choice hill climbing** implements stochastic hill-climbing by *generating successors randomly until one is generated that is better than the current state*. This is a good strategy when when a state has many (e.g., thousands of) successors, hence cannot wait until all uphill moves are generated.
-   **Random-restart hill climbing**: The above algorithms are incomplete; they often fail to find a goal when one exists because they can get stuck on a local maxima. In random-restart, we conduct a *series of hill-climbing searches* from randomly-generated initial states until a goal is found.

## Simulated Annealing Search
The regular hill-climbing algorithm _never_ makes "downhill" moves towards states with a lower value (or higher cost). Hence, it is guaranteed to be incomplete.

A purely-random walk would allow us to move both uphill and downhill, but is very inefficient. How could we combine the two? We can do this with **simulated annealing**. 

The innermost loop of the simulated-annealing algorithm is quite similar to hill climbing, except instead of choosing the _best_ move, it chooses a _random_ move. If the move improves the situation, it is always accepted. 

Otherwise (i.e., if the move is "bad"), the algorithm accepts the move with some probability less than 1. The probability decreases exponentially with the "badness" of the move (i.e., the amount of ΔE by which the evaluation is worsened), and also decreases as the "temperature" _T_ goes down. 

This means that "bad" moves are more likely to be allowed at the start when _T_ is high, and they become more unlikely as _T_ decreases. If the _schedule_ lowers _T_ slowly enough, the algorithm will find a global optimum with probability approaching 1.

## Local Beam Search

>[!analogy]
>Hill-climbing — “…trying to find the top of Mt. Everest in a thick fog while suffering amnesia.” 
>Local beam search — Doing this with several friends, each of whom has a short-range radio and an altimeter.

The **local beam search** algorithm keeps track of _k_ states rather than just one state: 
-  It begins with _k_ randomly-generated states. 
-  At each step, all successors of all _k_ states are generated. If any one of those is a goal, the algorithm halts. Otherwise, it selects the _k_ best successors from the complete list and repeats. 

![[Pasted image 20220923143309.png]]

This may look like we are simply running _k_ random restarts in parallel. However, in random-restart each search process runs independently of the others. _In a local beam-search, useful information is passed among the parallel search-threads_. This means the algorithm abandons unfruitful searches and moves towards the area where most progress is being made.

## Genetic Algorithm
- Inspired by Darwin’s theory of natural selection 
- Each state is seen as an individual in a population 
- A **genetic algorithm** applies **selection and reproduction** operators to an initial population 
- The aim is to generate individuals that are most successful, according to a given **fitness function** 
- It is basically a **stochastic local beam search**, but with successors generated from pairs of states  (instead of choosing k best successors)
- Local maxima are avoided by giving a nonzero chance of reproduction to low-scoring individuals

## Summary
![[Pasted image 20220828180308.png]]

## Questions/Cues
- Recursive best first search? Iterative deepening A*?
- Depth first search is a special case of Best first search? → Yes, when we set `f(n) = -depth(n)`
- Uniform Cost Search is special case of A* Search? → Yes, when `f(n) = g(n)` or `h(n) = 0`
- What happen if we run beam search with k = 1? → turn into the Hill Climbing Search algo
- What happen if we run simulated annealing with T = infinity? → turn into a random walk algo, where a successor is chosen randomly from the set of all successors.