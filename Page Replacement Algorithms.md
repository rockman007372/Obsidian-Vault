
We exploit [[Locality Principles|locality principles]] in our Page Replacement Algorithm to prevent thrashing:
- **Temporal Locality:** After a page is loaded to physical memory, it is likely to be accessed in near future (loops) ⇒ keep more recent pages and remove earlier pages since they probably will not be needed soon.
- **Spatial Locality:** A page contains contiguous locations that is likely to be accessed in near future (neighboring code instructions)

Common Strategies:
1. Optimal Solution - similar to [[Optimal Caching]]
2. [[FIFO Replacement]]
3. [[Least Recently Used Replacement]]
4. [[Second-Chance Replacement]]