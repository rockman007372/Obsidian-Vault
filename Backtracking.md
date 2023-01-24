---
tag: datastructure
---
2022-07-07 18:51
Tags: [[Data Structure and Algorithm]]
- - - - - - - - - - - - - - - - - - - - - - - - - - - - -   

## Practice Questions
-   [Subsets](https://leetcode.com/problems/subsets)
-   [Subsets II](https://leetcode.com/problems/subsets-ii)
-   [Permutations](https://leetcode.com/problems/permutations/)
-   [Permutations II](https://leetcode.com/problems/permutations-ii/)
-   [Combinations](https://leetcode.com/problems/combinations/)
-   [Combination Sum II](https://leetcode.com/problems/combination-sum-ii/)
-   [Combination Sum III](https://leetcode.com/problems/combination-sum-iii/)
-   [Palindrome Partition](https://leetcode.com/problems/palindrome-partitioning/)

## Main Points
> [!Defintion]
> An algorithm which incrementally builds candidates to the solution and abandons a candidate ("backtracks") as soon as it determines that the candidate cannot lead to a valid solution.

![[Pasted image 20220707191224.png]]

Faster than Brute-Force Search since the backtracking ensures unneccesary exploration is eliminated.

[[Depth First Search]] is a special form of backtracking. In DFS we visit each node once and exactly once, while in backtracking, we can continue to visit a previously visited node after we backtracked.

![[Pasted image 20220707191946.png]]
An example of backtracking.

## Pseudo Template
```Python
def backtrack(candidate):
    if find_solution(candidate):
        output(candidate)
        return
    
    # iterate all possible candidates.
    for next_candidate in list_of_candidates:
        if is_valid(next_candidate):
            # try this partial candidate solution
            place(next_candidate)
            # given the candidate, explore further.
            backtrack(next_candidate)
            # backtrack
            remove(next_candidate)
```

Key points:
-   Overall, the enumeration of candidates is done in two levels: 
	- 1)  At the first level, the function is implemented as recursion. At each occurrence of recursion, the function is one step further to the final solution.  
	- 2)  At the second level, within the recursion, we have an iteration that allows us to explore all the candidates that are of the same progress to the final solution.

-   The backtracking should happen at the level of the iteration within the recursion. 
  
-   Unlike brute-force search, in backtracking algorithms we are often able to determine if a partial solution candidate is worth exploring further (_i.e._ `is_valid(next_candidate)`), which allows us to *prune the search zones.* This is also known as the constraint, _e.g._ the attacking zone of queen in N-queen game. 
  
-   There are two symmetric functions that allow us to mark the decision (`place(candidate)`) and revert the decision (`remove(candidate)`).

## Example to apply template

###### Sudoku
>[!Rule]
>The main idea of the game is to fill a grid with only the numbers from 1 to 9, while ensuring that each row and each column as well as each sub-grid of 9 elements does not contain duplicate numbers.

![](https://assets.leetcode.com/uploads/2019/03/31/sudoku_solver.png)
_Fig 2. Sudoku Game_

We break down on how to apply the backtracking template to implement a sudoku solver in the following.

- [1]. Given a grid with some pre-filled numbers, the task is to fill the empty cells with the numbers that meet the constraint of Sudoku game. We could model the each step to fill an empty cell as a recursion function (_i.e._ our famous `backtrack()` function).

- [2]. At each step, technically we have 9 candidates at hand to fill the empty cell. Yet, we could filter out the candidates by examining if they meet the rules of the Sudoku game, (_i.e._ `is_valid(candidate)`).

- [3]. Then, among all the suitable candidates, we can try out one by one by filling the cell (i.e. `place(candidate)`). Later we can revert our decision (_i.e._ `remove(candidate)`), so that we could try out the other candidates.

- [4]. The solver would carry on one step after another, in the form of recursion by the `backtrack` function. The backtracking would be triggered at the points where *either the solver cannot find any suitable candidate* (as shown in the above figure), or *the solver finds a solution to the problem*. At the end of the backtracking, we would enumerate all the possible solutions to the Sudoku game.