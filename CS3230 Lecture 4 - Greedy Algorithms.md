---
tags: toProcess
course: 
type:
date: 2023-09-05 Tuesday
---
### Interval Schedule

>[!question]
> Given list of intervals, find the subset with largest number of non-overlapping intervals.

- Related leetcode equivalent: [[Non-Overlapping Intervals]] and [[Merge Intervals]]
- iterate throught some greedy template/heuristics:
	- Sort by start time
	- ! Sort by finish time (only this work)
	- Sort by interval length 
	- Sort by no.conflicts
- Use contradiction to prove our solution is optimal
### Interval Partitioning

>[!question]
> Find the minimum number of classrooms to schedule all lectures so that so lecture overlap in the same room at the same time.

- depth = max number of overlapping lessons
- key observation: ??
- Algorithm:

```
sort by start time of lecture
pq = {}
iterate through the lectures:
	if there is a room avail:
		assign lecture to room
	else:
		add another room to PQ and assign lecture to it
```

- did not understand this

### Scheduling to Minimize Lateness

- Explore some strategies:
	- earliest deadline first
	- ...
	- ...
- Come up with some common heuristic and find counter-example if possible
- Then analyse algo using proof by contradiction.
- Prove by **structural bound**

### Optimal Caching




## Summary

## Questions/Cues

