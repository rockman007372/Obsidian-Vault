---
tags: 
aliases: 
date: 2022-09-22 Thursday
---
Links: [[Transport Layer]]
- - - 

Motivation: How to build a reliable transport layer protocol on top of the unreliable [[Network Layer]], which may:
- *Corrupt* packets
- *Drop* packets
- *Re-order* packets 
- Deliver packet after long *delay*

End-to-end RDT should:
- guarantee delivery and correctness of packet
- deliver packets in the order they are sents

![[Pasted image 20220910220109.png]]

Different RDT protocols:
- [[RDT versions]] (Stop-and-wait)
- [[Pipelined Protocol]]