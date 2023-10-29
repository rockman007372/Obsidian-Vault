![[Pasted image 20230911153612.png]]

- Select task with the smallest total CPU time first (order by processing time) => minimizes average waiting time.
- Starvation is possible: short jobs keep getting added and being executed first.
- How to guess total CPU time for a task in advance? **Exponential Average**
#### Exponential Average

Formula:
$$predicted_{n + 1} = \alpha Actual_{n}+ (a- \alpha)Predicted_{n}$$
Where:
- $Actual_n$ = the most recent CPU time consumed
- $Predicted_{n}$ = the past history of CPU time consumed
- $Predicted_{n+1}$ = lastest prediction

>[!big idea]
> What to you value more? The *most recent* CPU time consumed by the task or *the history* of CPU time consumed by the task so far?

![[Pasted image 20230918094410.png]]