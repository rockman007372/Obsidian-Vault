---
tags: processed
course: CS2109S 
type: lecture
date: 2022-08-28 Sunday
---
Links: [[Problem-Solving Agents in AI]], [[CS2109S]]
- - -

What are [[Search Strategies]]?

## What is Uninformed Search?
- Little to no info abt the search space is available
- All we know is **how to generate new states** and **recognize a goal state**
- Some stategies:
	1. [[Breadth First Search]]
	2. [[Uniform-Cost Search]]
	3. [[Depth First Search]]
	4. [[Depth-Limited Search]]
	5. [[Iterative Deepening Search]]

## Repeated States and Graph Search

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
