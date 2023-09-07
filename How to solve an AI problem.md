---
tags: processed
course: CS2109S
type:  lecture
date: 2022-08-20 Saturday
---
Links: [[CS2109S]]
- - -

## Goals
- How to take a problem and frame it as a search problems
- Understand properties and see which search to apply

#### Romania example
- On holiday in Romania, currently in Arad.
- Flight leaves tmr from Bucharest
- Steps in solving problem:
	- Formulate **goal**: Be in Bucharest
	- Formulate **problem**: 
		- State: Various cities
		- Actions: drive between cities
	- Find **solution**: Sequences of cities to drive 

## Different problem states

- **Single state** problem: Deterministic, fully observable
	- Agen knows exactly which state will be in, solution is a sequence
- **Sensorless** problem (Conformant problem): Non-observable
	- Agent has no idea which state it is in, solution is a sequence
- **Contingency** problem: Nondeterministic and/or partially observable 
	- Percepts provide new information abt current state, often interleave search and execution
- **Exploration** problem: Unknown state space 

##### Example: Vacuum world
- 3 variables: left room status (clean or unclean), right room status, cleaner status (where is it)
- 8 discrete states (2 x 2 x 2)
- Different types of problem states:
	- **Single** State: Know which room is dirty, know the exact sequence of actions to take
	- **Sensorless**: Dont know where is dirty, suck both rooms
	- **Contingency**: Not deterministic, dont know if machine sucks well → have an if condition: `if dirty: suck, else move to next room`

## Single State Problem Formulation

A problem is defined by four items:
1. **Initial state** (at Arad)
2. **Actions** defined by *successor function* S(x) = set of action - state pairs
	-  `S(Arad) = { <Arad -> Zerind, Zerind>, ... }` 
3. **Goal** test:
	- explicit (x = "at Bucharest")
	- implicit (checkmate(x))
4. Path **cost** (additive)
	- sum of distances or no. actions executed
	- c(x, a, y) is the step cost, assumed to be $\geq$ 0

A **solution** is **a sequence of actions** leading from the **initial state to a goal state.**

#### Framing a search problem

There are **7** components:
- **states**
- **initial state**
- **actions**
- **transition model**: Given the current state and an action, generate the next state 
- **successor function**: Given the current state, generate all the neighbour states
- **goal test**
- **path cost**

Provide a mathematical description of the **transition model**, and **goal test** if possible.

#### Vacuum world State-Space Graph
**States:** Integer/ Boolean - dirt and robot location
**Actions:** Left, Right, Suck
**Goal test:** no dirt at all locations
**Path Cost:** 1 per action

#### 8-Puzzle
Move the slots so that numbers are in order

**States:** Locations of tiles (9! states)
**Actions:** Move blank space left, right, up, down
**Goal test:** when goal state is reached (consecutive numbers)
**Path cost:** 1 per move

NP-hard problem apparently

#### Robotic Assembly
**States:** real value coordinate of robot join angles, parts of the object to be assembled 
**Actions:** continuous motions of joints
**Goal test:** Complete assembly
**Path cost:** time to execute a motion?

## Tree Search Algorithm

Basic idea: Offline, simulated explorations of state space by **generating successors of already explored states**

Difference between Tree Search and Graph Search: Tree Search does **NOT** keep a hash set of visited nodes!

![[Pasted image 20220820150604.png]]

>[!important]
> We should do goal test **before** adding children nodes to frontier, not after expansion → SAVE TIME AND SPACE

#### State vs Node
- A **state** is representation of a physical configuration
- A **node** is a data structure making up the search tree. It includes state, parent node, actions, path cost g(x), depth...
- The `expand` function creates new nodes, fills in various fields and uses the `SuccessorFn` of the problem to create the corresponding states.
- 2 different nodes can *contain the same world state* if that state is generated via *2 different search paths*

![[Problem-Solving Agents in AI 2022-08-20 12.30.31.excalidraw]]

### 4. [[Uninformed Search]]
### 5. Bidirectional Search

- Simultaneously **search forward from initial state** and **search backwards from goal state**
- Stop when 2 searches meet.
- Intuition: $2 * O(b^{d/2})$ is smaller than $O(b^d)$
- Implementation issues:
	- Operators are NOT reversible: path taken backwards cannot be taken forward.
	- Many possible goal states → Solution: Construct a goal state containing the superset of all goal states
	- Check if a node appears in the other search tree? 
	- Using different search strategies for each half

Read more [here](https://iq.opengenus.org/bidirectional-search/#:~:text=Bidirectional%20Search%20is%20Graph%20Search,for%20other%20applications%20as%20well.)

---
## Summary
![[Pasted image 20220820133653.png]]

  
| **Criterion** | **BFS**            | **Uniform Cost**                            | **DFS**            | **Depth Limited**  | **ID-DFS**         | **Bidirectional**    |
|---------------|--------------------|---------------------------------------------|--------------------|--------------------|--------------------|----------------------|
|   Complete?   | Yes<sup>a</sup>    | Yes<sup>a,b</sup>                           |   No               | No                 | Yes<sup>a</sup>    | Yes<sup>a,d</sup>    |
|     Time      | *O(b<sup>d+1</sup>)* | *O(b*<sup>*$\lceil$C/ϵ$\rceil$*</sup>*)* | *O(b<sup>m</sup>)* | *O(b<sup>l</sup>)* | *O(b<sup>d</sup>)* | *O(b<sup>d/2</sup>)* |
|     Space     | *O(b<sup>d+1</sup>)* | *O(b*<sup>*$\lceil$C/ϵ$\rceil$*</sup>*)* | *O(bm)*            | *O(bl)*            | *O(bd)*            | *O(b<sup>d/2</sup>)* |
|    Optimal?   | Yes<sup>c</sup>    | Yes                                         |   No               | No                 | Yes<sup>c</sup>    | Yes<sup>c,d</sup>    |

Evaluation of tree-search strategies.
_b_ is the branching factor;
_d_ is the depth of the **shallowest** (most optimal) solution; 
_m_ is the maximum depth of the search tree; 
_l_ is the depth limit. 

Superscript caveats are as follows: 
a) complete if _b_ is finite; 
b) complete if step costs >= ϵ for positive ϵ. 
c) optimal if step costs are all identical; 
d) if both directions use breadth-first search.

##### When to use DFS vs BFS
If your tree has a very large amount of spread compared to its depth, and you're expecting results to be found at the leaves, then clearly DFS would make much more sense here as it reaches leaves faster than BFS, even though they both reach the last node in the same amount of time (work).

When a tree is very deep, and non-leaves can give information about deeper nodes, *BFS can detect ways to prune the search tree* in order to reduce the amount of nodes necessary to find your goal. Clearly, *the higher up the tree you discover you can prune a sub tree, the more nodes you can skip.* This is harder when you're using DFS, because you're prioritize reaching a leaf over exploring nodes that are closer to the root.