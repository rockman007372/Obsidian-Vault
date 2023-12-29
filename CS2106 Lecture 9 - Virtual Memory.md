---
tags: []
course: CS2106
type: lecture
date: 2023-11-04 Saturday
---
Basic idea:
- RAM (virtual memory) is small while hard disk (secondary memory) is spacious. Hence we cannot store all pages of processes inside RAM.
- Thus, we store process's logical memory pages in a combination of physical memory and secondary memory.
- Basic idea of mapping virtual address to physical address is unchanged. What changes is the actual physical address (whether it is in RAM or Disk)

![[Pasted image 20231105100350.png]]

Two page types:
- **Memory resident:** pages in physical memory (RAM)
- **Non-memory resident:** pages in secondary memory (Disk)

Page fault:
- Accessing a non-memory resident page, which requires reading from secondary storage and load page into physical memory.
- Analogous to **cache miss**.
- **Thrashing**: when memory access results in page fault most of the time

Implications of virtual memory:
- Amount of physical memory no longer restrict the size of logical memory address (possible for RAM to be smaller than the process size)
- Pages currently not needed can be on secondary storage to save space.
- Allow more processes to reside in memory (RAM is no longer a limit, can store pages from different processes in RAM)

Demand Paging:
- Process starts with no memory resident page (no page loaded into RAM)
- Only allocate pages to RAM when there is a **page fault.**
- Pros: Quick start-up
- Cons: Sluggish at the start. Can also affect other processes if new processes hog I/O to load pages.

## Implementations of VM

1. How to structure the page table to maximize space efficiency? [[Page Table Structures]]

2. Which old page to replace in physical memory when we load in a new page from secondary memory? [[Page Replacement Algorithms]]

3. How to distribute limited physical memory frames among processes? [[Frame Allocation Policies]]