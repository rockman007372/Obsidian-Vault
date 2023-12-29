Combine [[Paging Scheme]] and [[Segmentation Scheme]] to map logical memory of a process to physical memory.

Basic idea:
- Each segment in the logical memory of process (code, data, heap, stack) is now composed of several pages instead of a contiguous memory region.
- Segment can grow by allocating new pages then add entries to its **Page Table**

![[Pasted image 20231104093451.png]]

![[Pasted image 20231104093552.png]]

Note:
- Out-of-range error is checked by comparing the logical address's **page number** vs **number of pages inside the Page Table** at the moment
- Offset can never be out of range (When offset increases beyond frame size, page number is incremented by one)