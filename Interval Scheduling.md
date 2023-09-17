
>[!question]
> Given list of intervals, find the subset with largest number of non-overlapping intervals.

- Leetcode: [[Non-Overlapping Intervals]] 
- Iterate throught some greedy templates/heuristics:
	- Sort by start time
	- ! Sort by finish time (only this work)
	- Sort by interval length 
	- Sort by no.conflicts
## Solution

```
jobs = sort(jobs, job => job[finish time])

A = []

for i from 1 to n:
	if jobs[i] does not overlap with A[-1]:
		A.append(job[i])

return A
```

- Time: O(nlogn) to sort
- Use contradiction to prove our solution is optimal

## Proof

![[Pasted image 20230914132934.png]]

1. Assuming S' is the optimal solution. S is our greedy solution (sort by upper bound).
2. Suppose not that S is not optimal.
3. Assuming the optimal solution and the greedy solution return the same set of jobs until job r + 1. Job $i_{r + 1}$ of S finishes before job $j_{r + 1}$ of S'. However, we can replace job j with job i in S' and the solution is still optimal. Contradict assumption.