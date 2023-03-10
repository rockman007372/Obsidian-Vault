## Uninformed Search Strategies

- Little to no info abt the search space is available
- All we know is **how to generate new states** and **recognize a goal state**
- Some stategies:
	1. BFS
	2. Uniform-cost search
	3. DFS
	4. Depth-limited search
	5. Iterative deepening search

#### Breadth First Search
- See more at [[Breadth First Search]]
- Expand *shallowest unexpanded* nodes.
- Implementation: frontier is a **FIFO queue**

Properties:
- Complete: **YES** if b is finite 
- Time: $1 + b + b^2 + b^{3} + \cdot\cdot\cdot + b^{d} + b(b^{d}-1)= O(b ^ {d + 1})$ 
	- d is the depth of the shallowest goal node
	- This is basically the number of nodes: O(N)
	- ![[Problem-Solving Agents in AI 2022-08-20 12.50.29.excalidraw]]
- Space: $O(b ^ {d + 1})$ 
	- In worst case, every node *at depth d + 1* of the search tree are in the fringe/frontier
	- **Dependent on when goal checking is done** → If goal test is done before pushing nodes to queue, space is reduced to $O(b^d)$, because we do not have to store and check the **last level**
- Optimal:
	- **Yes** (*only if step cost is identical, VERY IMPORTANT*), as cost only increases as we go deeper, and we only go deeper if the previous depth did not yield goal node
	- Else, path to the shallower goal states which we must first visit can be higher than the deeper goal state

>[!Important]
> **Space is a bigger problem than time** → Hence we need Iterative Deepening Search to solve space!

#### Uniform-cost Seatch
- Expand unexpanded nodes with **lowest path-cost** `g(n)`
- Imprementation: Frontier = **priority queue ordered by path cost g**
- *Equivalent to BFS if step costs are all equal*, else it is a **variant** of  [[Dijkstra's Algorithm]]
- **Difference** from Dijkstra: We check whether a node is a goal state (**goal check**) after we pop it from PQ. In Dijkstra, we do not do goal check anywhere (It's simply a SSSP algorithm).

Properties:
- Complete: **yes**, if step cost ≥ ε > 0
	- Assuming that the branching-factor _b_ is finite, and that the step costs are >= ϵ where ϵ is some small positive-number. 
	- If the second assumption does not hold, it can get stuck in an infinite loop if there is a path with an infinite sequence of zero-cost actions (i.e., a sequence of **NoOp** actions - **only in tree search**). Completeness is therefore guaranteed provided the cost of every step exceeds some small positive-constant ϵ.
	- Negative edge cost can result in a negative weight cycle.
- Time:
	- ![[Problem-Solving Agents in AI 2022-08-20 16.25.55.excalidraw|300]]
	- b is the branching factor and C* is the total cost of the optimal solution
	- Why: Every action costs at least ϵ, so there are a total of $C^{*} / ϵ$ steps (level) to reach the goal state. *Every time we reach a node, we expand at most b nodes*. Just like BFS, in the worst case we also have to check every node. Total = 1 + b + b^2 + ... + b^(C/ε) 
- Space: Same - $O(b^\frac{C*}{ε})$, max number of nodes in the PQ at the last level (frontier)
- Optimal: **Yes**, node expanding in *increasing orders of g(n)*
	- Basically, when a node `n` is selected for expansion, the optimal path to that node has been found (Greedy algorithm)
	- Why? Assume `n` is expaned, yet there exists another frontier node `n'` on the optimal path from the start node to `n`. By definition, `n'` would have a lower `g`-cost than `n` and would have been selected first. Since step-costs are non-negative, paths will never get shorter as nodes are added.

#### Depth First Search
- See [[Depth First Search]]
- Expand **deepest unexpanded** nodes
- Implementation: Frontier = **stack**

Properties:
- Complete: **No**
	- **WHY:** fail in infinite-depth spaces and spaces with loops → Must limit the depth + avoid repeating states along the path 
	- Complete in finite space
- Time: $O(b^m)$ = $1 + b + b^2 + ... + b ^{m}$ 
	- Terrible if m (max depth) is much larger than d (least depth)
	- If solutions are dense yet depth is low, may be much better than BFS (*EG: RUBIK CUBE SOLVING*)
	- Equals O(N) where N is no. nodes
- Space: O(b * m) - linear space, very space efficient
	- **Why:** m = the length of the longest path. For each node, you have to store all b siblings so that you know which sibling to explore next after completing a branch → for m nodes down the path, must store its b sibling per node. 
- Optimal: **NO**
	- **WHY:**  Even when step costs are equal, DFS is still non-optimal, because the deepest goal node may be reached first and incurs greater cost.
	- ![[Problem-Solving Agents in AI 2022-08-27 18.30.06.excalidraw||300]]

#### Depth-limited search
DFS but with a depth limit l before we stop searching → **Problem:** Stop before reaching result -> **Uncomplete search algo**

-   **Completeness**: No if _l_ < _d_ (but also incomplete in general).
-   **Time**: *O(b<sup>l</sup>)*
-   **Space**: _O(bl)_
-   **Optimality**: Non-optimal when _l_ > _d_ (theres a more optimal node on the right) 

![[Problem-Solving Agents in AI 2022-08-20 14.45.22.excalidraw]]

#### Iterative Deepening Search (DFS simulating BFS)
- This is a general strategy used in combination with DFS tree search that finds the best depth limit. 
- The algorithm does this by gradually increasing the depth (first 0, then 1, then 2, and so on) until a node is found. 
- This occurs when the depth limit reaches _d_, the depth of the shallowest goal-node. Iterative deepening **combines the benefits of DFS and BFS**.

![[Pasted image 20220820153317.png]]

 ![[Problem-Solving Agents in AI 2022-08-20 15.41.09.excalidraw]]

- Properties:
	- **Complete**: Yes, no depth limit, reach goal node eventually if it exists.
	- **Time Complexity**: $O(b ^ d)$
		- zero level is searched d + 1 times, 1st layer is searched d  times, 2nd layer is searched (d - 1) times....
		- This can seem wasteful because states are generated multiple times. But it turns out this is not too costly, this is because in a search tree with the same (or nearly the same) branching factor at each level, *most of the nodes are in the bottom level* and hence dominate the upper level in time complexity.
		- $(d+1)b^{0} + db^{1}+ (d - 1)b^{2}+ ... + b^{d} = O(b ^ d)$
	- **Space**: O(bd) - max size of stack at anytime - NOT O(bm)!
	- **Optimal**: Yes **only if step costs are all identical**
	  
- Compared to BFS:
![[Pasted image 20220820155246.png]]
⇒ Does better because other nodes at depth d are not expanded.

- Compared to DFS:
![[Pasted image 20220820155637.png]]
=> Overhead (The amt of repeated work we have to search) is not that bad!

> **In general, ID-DFS is the preferred uninformed-search method when the search space is large and the depth of the solution is not known.**

#### Repeated States
To deal with loops / repeated states, **memoize visited nodes** using an efficient data structure (eg: [[HashSet]]).

>[!important]
>Memoize the state/node before pushing into the frontier to prune even more nodes! 

Example: Graph BFS search for the cannibal problem


```python

class BFS:

    @staticmethod
    def graphSearch(m, c):
        MIS, CAN = m, c
        
        actions = [
            [2, 0], 
            [1, 0], 
            [0, 2], 
            [0, 1], 
            [1, 1]]

        boat = 1
        path = ()
        root = [m, c, boat, path]

        frontier = [root]
        visited = set()
        visited.add((m, c, boat))

        while frontier:
            new_frontier = []

            for node in frontier:
                m, c, boat, path = node

                # print((m , c, boat))
                
                # goal check
                if m == 0 and c == 0:
                    return path

                # Expand node to neighbors
                for act in actions:
                    newPath = path + (tuple(act),)
                    if boat == 1: # if boat on left
                        neighbor = [m - act[0], c - act[1], 0, newPath]
                    else: # if boat on right
                        neighbor = [m + act[0], c + act[1], 1, newPath]

                    # Check condition before pushing neighbor into frontier
                    newM, newC, newBoat,_ = neighbor


                    if (newM >= 0 and newM <= MIS and newC >= 0 and newC <= CAN):

                        if (newM == 0 or newM >= newC): # check left side

                            if (MIS - newM == 0 or MIS - newM >= CAN - newC): # check right side
                                
                                if (newM, newC, newBoat) not in visited:
                                    new_frontier.append(neighbor)
                                    visited.add((newM, newC, newBoat))

            frontier = new_frontier

        return None # reach here means no goal, infinite loop since no visited set


print(BFS.graphSearch(7, 6))

```

Framework: Tower Of Hanoi

```python
def hanoi(n):
    def is_goal(node):
        state, steps = node
        return state == ((),(),tuple(range(1,n+1)))

    def expand(node):
        state, steps = node
        left,middle,right = state
        result = []

        if left != () and (middle== () or left[0]<middle[0]):
            result.append(((left[1:],(left[0],)+middle,right),steps + ("L->M",)))
        if left != () and (right== () or left[0]<right[0]):
            result.append(((left[1:],middle,(left[0],)+right),steps + ("L->R",)))
        if middle != () and (left== () or left[0]>middle[0]):
            result.append((((middle[0],)+left,middle[1:],right),steps + ("M->L",)))
        if middle != () and (right== () or right[0]>middle[0]):
            result.append(((left,middle[1:],(middle[0],)+right),steps + ("M->R",)))
        if right != () and (left== () or left[0]>right[0]):
            result.append((((right[0],)+left,middle,right[1:]),steps + ("R->L",)))
        if right != () and (middle== () or middle[0]>right[0]):
            result.append(((left,(right[0],)+middle,right[1:]),steps + ("R->M",)))
        return result
    
    queue = []
    initial_state = ((tuple(range(1,n+1)),(),()),())
    queue.append(initial_state)
    seen = set()
    
    while queue:
        current = queue.pop(0)
        #print(current)
        if is_goal(current):
            return current[1]
        else:
            for move in expand(current):
                state, steps = move
                if state not in seen: # check duplicate here, no need to push
                    seen.add(state)
                    queue.append(move)
    return False
```
