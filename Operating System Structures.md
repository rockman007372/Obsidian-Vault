
## Monolithic OS

![[Pasted image 20230820103923.png]]

- Kernel is one big special prgram.
- Good SE principles are still possible with modularization + separation of interfaces and implementation.
- Traditional approach taken by most Unix variants.
- Pros: Well understood and good performance.
- Cons: Highly coupled components, very complicated internal structure.

## Microkernel OS

![[Pasted image 20230820104223.png]]

- The kernel is
	- very small and clean
	- provides basic and essential facilities only such as Inter-Process Communication (**IPC**), address space management...
- Pros: 
	- more robust and extensible. 
	- better isolation and protection btw kernel and high-level services
- Cons: lower performance