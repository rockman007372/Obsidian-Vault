
>[!question]
> Find minimum number of classrooms to schedule all lectures so that no two occur at the same time in the same room.

- depth = max number of overlapping lessons
- key observation: number of classroom needed >= depth
- question: is it true that min number of classrooms = max no. overlapping lectures?

## Algorithm

```
sort lecture intervals by its start time 
pq = {}
iterate through the lectures:
	if there is a room avail:
		assign lecture to room
	else:
		add another room to PQ and assign lecture to it
```

- How to know if a room is available? if the new lecture's start time > old lecture's end time in the same room.
- How to identify the potentially empty classroom? Return the classroom whose lecture's end time is the earliest => Use a Min [[Priority Queue|PQ]], ordered by ending time.
- Time: O(nlogn)

## Proof

1. Let d = number of classrooms that the greedy algorithm allocates.
2. Classroom d is opened because we needed to schedule a job, say j, that is incompatible with all d-1 other classrooms.
3. ! Since we sorted by start time, all these incompatibilities are caused by lectures that start no later than sj.
4. Thus, we have **d lectures overlapping** at time $s_j + \epsilon$.
5. Since there are d overlaps,  all schedules use >= d classrooms. Cant do better than d.


