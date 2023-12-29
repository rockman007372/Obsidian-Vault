---
tags:
  - processed
course: CS4225
type: lecture
date: 2023-08-20 Sunday
---

## Cloud Computing

Utility Computing: Make computing resources as a metered service (pay as you go). Dynamically provide [[Virtual Machines]]. 

Everything as a service:
- Infrastructure as a Service: rent virtual machines
- Platform as a Service: provide hosting for web applications (in between infras and software)
- Software as a Service: Users do not have to run any code (gmail, dropbox, zoom)

Data center:
- Instead of building a super quantum computer, just cluster a bunch of normal comps
- the data center **is** the computer: think of the machines in the data center as a big **processsing unit** used to solve a problem

### Bandwidth vs Latency

![[Pasted image 20230821163708.png]]

- Bandwidth (GB/s): max amt of data that can be transmitted per unit time
- Latency (ms): time taken for 1 packet to go from source to destination (one-way) or back and forth (round-trip)
- Throughput: **actual** amt of data transmitted accross the network during some period of time (with delays taken into account). 

### Storage hierarchy

![[Pasted image 20230923103619.png]]

- One server: A single computer or hardware device.
	- DRAM: dynamic RAM (data only exists while running) 
	- Disk: Where you contain data long-term
	- Flash: Solid state drive, thumb drive
- Local Rack (80 servers)
- Cluster (30 racks)

Trade-offs: **speed vs capacity.** Larger capacity = slower access speed. 

![[Pasted image 20230923103737.png]]

>[!takeaways]
> 1. Disk has higher storage capacity then DRAM
> 2. Storage capacity increases from Local Server -> Rack -> Datacenter
> 3. Disk reads are much more expensive than DRAM (higher latency + lower bandwidth)
> 4. DRAM is more expensive than DISK

### Big ideas of Massive Data Processing in Data Centers

- Scale out, not up (horizontal > vertical scaling): combine cheaper machines
- Move processing to the data: Clusters have limited bandwidth => move the task to machine where the data is stored
- Process data sequentially, avoid random access
- Seamless scalability: if a machine takes 100 hours to process a dataset, ideally a cluster of 10 machines can do it in 10 hours.
