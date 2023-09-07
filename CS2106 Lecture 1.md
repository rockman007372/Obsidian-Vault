---
tags: toProcess
course: CS2106
type: lecture
date: 2023-08-18 Friday
---

- Learning outcomes:
	- Learn how OS manages computational resources
	- Abstraction and interfaces provided by OS
	- Write multi-process, multi-threaded programs
	- Write system programs that utilizes POSIX system calls for process, memory, I/O management
	- self-learn advanced OS topics LMAO

- Why do we need OS?
	- higher level of abstraction
	- security and isolation
	- manage hardware resources

- Why do we want abstractions?
	- Large variation in hardware config (eg. hard disk)
	- Hardware in the same category has well defined and common functionality
	- present high level functionality to user

- Resource allocation:
	- Program execution requires multiple resources: CPU, memory, I/O devices
	- All progs should be allowed to execute simultaneously
	- Hence OS is required to arbitrate conflicting requests

- Program can misuse pc:
	- accidentally: bugs 
	- maliciously: virus, malware
	- OS controls execution of program => OS is a **control program**
		- Prevent errors and improper use of comp
		- provide security

- Modern OS:
	- Desktop: win, mac, ubuntu (linux)
	- Mobile: android, ios
	- Real-time: robots?
	- Embedded?

## Operating System: high-level view

![[Pasted image 20230820103007.png]]

- The most important part of an OS is the **kernel**
- An OS is essentially a software program:
	- Deal w hardware issues
	- Provides **system call interface**
	- Special code for interrupt handlers, device drivers (codes that interact w hardware)
- Kernel code has to be different from normal progs:
	- No use of system call (Kernel is the system)
	- Cannot use normal library
	- No normal I/O
 - Programming language to implement OS:
	 - Historically assembly
	 - Now in HLLS: C/C++
	 - Heavily hardware architecture dependent
- Common code organization:
	- Machine independent HLL
	- Machine dependent HLL
	- Machine dependent assemby code
- Challenges:
	- No one else to rely on for services
	- Debuggin is hard
	- complexity
	- enormous codebase

>[!quote]
> "we are mostly writing user programs in this mod"

[[Operating System Structures]]
[[Virtual Machines]]