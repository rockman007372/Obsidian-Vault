- Paging scheme allows process to occupy disjoint physical memory locations.
- **Physical frame:** fixed-sized memory regions of the physical memory.
- **Logical page:** fixed-sized memory region of the process, same size as physical frame.
- The pages of a process are loaded into **any available** physical frame.
	- Logical memory space is contiguous.
	- Occupied physical memory region can be disjoined.
- We need a **Page Table** to map logical page to physical frame.

![[Pasted image 20231103172424.png]]

- To locate a value in the physical memory from its logical memory address, we need:
	- f: the physical frame number
	- Offset: the displacement from the beginning of the frame
	- Physical address = f x size of the physical frame + offset.

### Simpler translation

- We simplify the address translation calculation by:
	1. Keep frame size/page size a power of 2
	2. Physical frame size == logical frame size
- Physical address = $f * 2^{n}+ d$ 
![[Pasted image 20231103173526.png]]

- Demonstration:
![[Pasted image 20231103174043.png]]
### Fragmentation

- No external fragmentation (frame size is fixed)
- Internal fragmentation is possible:
	- Logical memory space may not be multiple of page size
	- Some pages has size smaller than physical frame ⇒ wasted space

### Implementation

>[!reminder]
> When a program (process) is under execution, the **Process Control Block** keep tracks of these information:
> - Memory context: text, data, stack, heap
> - Hardware context: GPR, PC, SP, FP... 
> - OS context: process ID, process state...

Pure software solution:
- OS stores Page Table inside PCB.
- The **memory context** of a process is precisely the Page Table (shows where to access the physical memory space that the process occupies).

Modern processors provide specialised **on-chip** component to support page.
- **Translation Look-Aside Buffer** (TLB)
- It caches the Page Table entries using a [[Fully Associative Cache]]

![[Pasted image 20231103180757.png]]

### Context-switching

- During context-switch, the TLB is flushed. Hence there is many TLB misses in the beginning of every process.
- To provide memory protection between processes, each entry of the Page Table has additional bits:
	- **Access-Right Bits**: indicate whether the page is writable, readable, executable 
		- page containing code must be readable, page containing data should be readable and writable
	- **Valid Bit**: check if a page is valid for the process to access.
		- some processes may not use the whole logical memory space, hence some pages are out-of-range
- **Page-sharing**: allows forked processes to share the same physical frame by sharing the same Page Table. Parent and child share until one tries to modify a shared page, which triggers a duplication of the page.


