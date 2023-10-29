>[!problem]
> - Single-core CPU processes one job at a time.
> - Job j requires $t_j$ units of processing time.
> - Job j is due at time $d_j$.
> - If job j starts at time $s_j$, it finishes at $f_{j}=s_{j}+ t_j$
> - Lateness of job j = $l_j$ = $max(0, f_{j} - d_{j})$
> - Goal: schedule all jobs to minimize **maximum lateness**, not total lateness.

![[Pasted image 20230914140753.png]]

- Explore some strategies and find counter-examples to disprove:
	- shortest processing time first
	- smallest slack first: slack = $d_j - t_J$
	- ! earliest deadline first
- Only the last heuristic works:

>[!algorithm]
> Sort the processes based on its deadline d<sub>i</sub>.

## Proof

Big idea: Let S be a our greedy solution. Let S' be our optimal solution. We prove S' cannot do better than our greedy solution.

>[!inversion]
> An inversion is a pair of task i, j such that $d_i$ < $d_j$ but job j is scheduled before job i.

![[Pasted image 20230915105222.png]]

##### Observations

Idle time:
- There is an optimal schedule with no idle time
- Greedy S has no idle time.

Inversion:

- Greedy S does not have inversions.
- If a schedule has at least one inversion, there **must** be an inversion with a pair of adjacent jobs.
- Swapping 2 adjacent inverted jobs reduce the number of inversions by one but **does not increase max lateness.**

##### Proof

1. Let S' be the optimal solution with no idle time such that there are minimum number of inversions.
2. ! If S' has no inversion, S = S' (or S' cannot do worst than S)
3. If S' has an inversion, let i - j be an adjacent inversion
	1. Swapping job i and j does not increase max lateness 
	2. However, the no. inversions strictly decreases
	3. Contradicts definition of S' => S' cannot have inversion.