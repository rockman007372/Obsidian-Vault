---
tags: 
course: CS2105
---
Date:: 2022-08-08 Monday
Links: [[How Is Internet Data Transmitted]]
- - -

### Loss and Corruption
Packet *queue* in router buffers: Packets wait to be sent out by a router in a FIFO (First In First Out) manner. 
- Queue has finite capacity
- What if packet arrival rate exceeds departure rate? Packets can be discarded by routers and lost in the network → *Network overflow*

Packets (propagated as waves) can be corrupted by noise waves (routers detect corrupted waves and interpret 1 as 0 for example)

### Delays
**Four** sources of packet delays:
- **Nodal processing** delay: check bit errors (protect packet integrity), very short (<msec) before sending to the queue (*neglibigle*)
- **Queuing** delay: time waiting in the queue (*negligible*)
- **Transmission** delay: 
	- packets are sent bits by bits into the wire
	- Tranmission delay = time to push ALL bits into the wire (time between the first and the last bit)
	- Independent of distance 
	- delay = $L / R$, where L is the number of bits and R is the transmission rate.
- **Propagation** delay: every bit is transmitted as a wave 
	- delay = $d / s$ 
	- d: length of physical link, s is propagation speed in medium

![[Pasted image 20220808143222.png]]

Example of questions about transmission time:
![[Roadmap 2022-08-07 18.37.27.excalidraw]]

Fewer users → queue and processing delay are faster → Queue and processing delays are *variables* dependent on number of users.

### Throughput
How many bits can ACTUALLY be transmitted per unit time.
$$Throughput = \frac{\text{total bits transmitted}} {\text{total time from end to end}}$$
- Measured for end-end communication (*inclusive of delays*)
- Link capacity (bandwidth) is meant for a **specific link**, *usually greater than throughput*.

![[Pasted image 20221110102656.png]]

- Difference between bandwidth and throughput: Bandwidth is the **maximum** amount of data that could travel end-to-end in one second, while throughput is the actual data transmitted due to non-ideal situations.

![[Pasted image 20221110100701.png]]

![[Roadmap 2022-08-07 18.43.27.excalidraw]]

### Practice Questions
##### Q1. 
Hosts A and B are connected by a direct link of 2 bps.  A sends a packet of 100 bits to B. Ignore other delay, when will B receive the packet? 
**Ans:** 50s.

##### Q2 . 
Same question, but *propagation delay over the link is 1s*.  
**Ans** : 100 / 2 + 1 = 51s.

![[CS2105 Roadmap 2022-08-08 15.10.29.excalidraw]]

##### Q3.
Now we introduce a router in between A and B. Bandwidth of each link is 2bps. Propagation delay over each link is 0.5s.
![[CS2105 Roadmap 2022-08-08 15.13.29.excalidraw]]
**Ans**: 101s
100 / 2 + 0.5 = 50.5s for the whole packet to reach the router from A.
50.5 x 2 to reach B.

##### Q4. 
*Two consecutive packets of 100 bits* sent from A to B. No router in between. Propagation delay is 1s. When will B receive both packets?

**Ans**: 201s
First bit of 2nd packet starts being sent after (100 / 2) s. 
Last bit of 2nd packet reaches after 100 / 2 + 1s.
=> Sending a 200-bit packet and 2 consecutive 100-bit packets make no difference (when 2 links have the same transmission rate maybe?)

##### Q5. 
2 packets of 100 bits, a router in between A and B. Transmission rate = 2 bps. Propagation delay = 0.5s.

**Ans**: 151s
(100/2) + (100/2 + 0.5) + (100/2 + 0.5) = 151.
![[CS2105 Roadmap 2022-08-08 15.01.51.excalidraw]]

##### Q6. 
Same as Q5. What is the throughput of transmission?
**Ans**: 200 / 151 = total bits / transmission time = 1.3 bps
=> In reality, throughput is lower than bandwidth due to delays and routers.
