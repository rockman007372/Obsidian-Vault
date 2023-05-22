
Intuitively, FD are like logic components on a circuit board. We activate the base components and subsequent components iteratively, until we cannot activate anymore.

### Formal Definition

Let $S = \set{A_1, A_2, ... A_n}$ be a set of attributes

The closure of S, denoted by $\set{A_1, A_2...An}^{+}$ is the set of attributes that can be **decided** by $A_1, A_2...An$ (either directly or indirectly)

Example: Given A -> B, B -> C, C -> D, D -> E
$\set{A}^{+} = \set{A, B, C, D, E}$
$\set{B}^{+} = \set{B, C, D, E}$
$\set{E}^{+} = \set{E}$

### Link to FD

$$Y \in \set{X}^{+} \iff (X \rightarrow Y)$$ 
This means:
- To prove that X -> Y **hold**, you just need to show that $\set{X}^{+}$ **contains** Y.
- To prove that X -> Y **does not hold**, you just need to show that $\set{X}^{+}$ **does not contain** Y.

### Link to Superkey

$$\text{A is a superkey of table R(A, B, C)}\iff \set{A}^{+} = \set{A, B, C}$$
Algorithm to find all the keys of a table:
1. Find the closure of all the subsets
2. Identify superkeys
3. Identify keys by finding minimal superkeys.

Tips:
- Always find closure of smaller subsets first => This avoids checking all the supersets as they are all superkeys
- ! If an attribute does not appear anywhere on the right-hand side of any FDs, it must be part of every key!



---
Links: [[CS2102]]