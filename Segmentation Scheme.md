- The logical memory space of a process has different segments: code, data, heap, stack.
- Since heap and stack grow dynamically, it is challenging to place the whole process in a **contiguous** physical memory space (how much can heap grow? how much can stack grow?)
- Idea: store the segments in **disjoint** physical memory locations.

![[Pasted image 20231103183528.png]]

### Implementation

- Each logical segment is mapped to a contiguous physical memory region, identified by a **base** and a **limit**.
- Each logical segment is identified by a segment id.
- A logical address is given as `<Segment id, Offset>`
	- Segment id → base, limit
	- Physical address = base + offset
	- if offset > limit, invalid access.

![[Pasted image 20231103184007.png]]

Pros:
- Allow segments to grow/shrink independently
- Can be protected/shared independently

Cons:
- Can cause external fragmentation (after process is removed, it leaves behind these small holes where the segments were, but cannot be merged)