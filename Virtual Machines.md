
Motivation for VM:
- What if we want to run several OS on the same hardware at the same time?
- How to do we test and debug OS?

Definition:
- A software emulation of hardware
- **Virtualization** of underlying hardware
- Normal OS can then run on top of VM

- VM are created and managed by **Hypervisor**
	- There are 2 types of Hypervisors
	- Type 1 hypervisor OS: Provide **individual** VMs to guest OS
	- Type 2 hypervisor OS: **Run in host OS** => Guest OS runs inside VM

Type 1:

![[Pasted image 20230820105048.png]]

Type 2:

![[Pasted image 20230820105115.png]]


