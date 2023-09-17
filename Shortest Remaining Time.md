![[Pasted image 20230911154600.png]]


- Select job with shortest **remaining** (or expected) time
- Variation of [[Shortest Job First]]
- **Premptive** algo: when a new job comes, if the new job has a smaller remaining time, replace the **current** job with new job
- Starvation: if we keep queuing short jobs with short remaining time, longer jobs will never get executed.