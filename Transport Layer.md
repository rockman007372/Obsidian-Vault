---
tags: processed
course: CS2105
type: lecture
date:: 2022-09-10 Saturday
---
Links: [[CS2105]]
- - -

## What is the transport layer?

Transport layer delivers messages between application processes running on different hosts.

2 popular transport layer protocols: **TCP** and **UDP**.

Transport layer protocols run in hosts (computers):
- **Sender**:  Break app messages into **segments** (packets) and pass them to [[Network Layer]] → Each segment contains *source* and *dest* port number
- **Receiver**: Reassembles segments into message, passes it to [[Application Layer]]
- **Packet Switches in between**: Only check destination IP address to decide routing → Receiver is identified by *destination IP address* in packet

![[Pasted image 20220910192721.png]]

##### Transport Layer vs Network Layer
- Transport layer: resides on end hosts (computers), provide **process-to-process** communication
- Network layer: not on host,  provides **host-to-host**, best-effort and unreliable communication

## Three transport layer protocols

- [[UDP]]
- [[Reliable Data Transfer]]
- [[TCP]]


