---
tags: 
aliases: 
date: 2022-09-22 Thursday
---
Links: [[Transport Layer]]
- - - 
## Introduction

How to build a reliable transport layer protocol on top of unreliable communication ([[Network Layer]])?

Underlying network layer may:
- *Corrupt* packets
- *Drop* packets
- Re-order packets (not considered rn?)
- Deliver packet after long *delay*

End-to-end RDT should:
- guarantee delivery and correctness of packet
- deliver packets in the order they are sents

![[Pasted image 20220910220109.png]]

## Finite State Machine (FSM)
![[Pasted image 20220910220232.png]]

## Different versions of RDT
![[Pasted image 20220910220417.png]]

### RDT 1.0: Perfectly Reliable Channel
![[Pasted image 20220910220723.png]]

### RDT 2.0: Data Bit Error

Packages may have bit errors over unreliable network transfer → Use **checksum** and **ACK/NAK** 

It follows **Stop-and-wait** protocol: Sender sends one packet at at ime, then waits for receiver response

![[Pasted image 20220910221028.png||700]]

### RDT 2.1: ACK/NAK Bit Error

Fatal flaw of 2.0 is ACK and NAK can also have bit errors → Need to resend package, but do not know whether package is received or not → **Packet Sequence Number**

![[Pasted image 20220910221602.png||730]]

### RDT 2.2: NAK-Free

Instead of sending NAK, receiver sends ACK for the **last packet received OK** → Receiver must explicity include sequence # of the packet being ACKed

![[Pasted image 20220910222040.png]]

### RDT 3.0: Packet Loss

To handle packet loss, we can implement a **timeout** for sender:
- Sender waits an amount of time for ACK
- If ACK not received by timeout, resend the packet.

In RDT 3.0, the sender relies on **timeout** to resolve both packet loss and packet corruption! Hence sender and receiver do nothing and wait for timeout.

There are **3 scenarios** for packet loss:
1. Packet is **lost** or **corrupted** → receiver does nothing, sender waits for timeout and resend
 ![[Pasted image 20220910222316.png]]
2. ACK is **lost** or **corrupted** → Sender does nothing , also wait for timeout
![[Pasted image 20220910222349.png]]
3. ACK is **delayed**:
![[Pasted image 20220910222506.png]]

RDT's performance is pretty ass, due to the stop-and-wait operation
![[Transport Layer 2022-09-10 22.29.56.excalidraw]]

## Pipelined Protocol

Instead of sending 1 packet and wait, we can send multiple yet-to-be-acked packets. This neccessitates more resources in exchange for greater transmission speed:
- Range of sequence numbers must be increased
- Buffereing at sender/receiver to order packets

There are 2 generic forms:
- **Go-Back-N** (GBN)
- **Selective Repeat** (SR)

### GBN 

Key features: Send multiple packets, if packet N is not received, **discard** subsequent packets after N and **resend ACK N** to signal N is not received. Once there is timeout or ACK N is received, resend packet N and all the subsequent packets in the window.

**GBN Sender:**
- Have up to N unACKed packets in pipeline
- Insert **k-bits sequence number** in header where $k = lg(N)$
- Use **[[Sliding Window]]** to keep track of unACKed packets
- Keep a timer for the oldest **unACKed** packet
- `timeout(n)`: Retransmit packet n and all subsequent packets in the window 

**GBN Receiver:**
- Only ACK packets that arrive in order 
- Discard out of order packets and ACK the *last in-order* sequence number → *Cumulative ACK*: ACK m means all packets up to m are received

![[Pasted image 20220910225503.png]]

GBN can be time-wasting, if most the packets received are out of order and hence discarded:

![[Pasted image 20220910225405.png]]

### Selective Repeat

We will keep out-of-order packets in **buffer**, and will reorder it once all the in-order packets are received.

Sender maintains a **timer** for **each** unACKed packet → When timer expires, retransmit only the unACKed packet.

![[Pasted image 20220922173544.png]]

![[Transport Layer 2022-09-22 17.36.25.excalidraw]]

**Sender:**
- If there is an available sequence number in window, send packet! (Send until window is full)
- Keep a timer for each packet → Resend packet `n` if time runs out + reset timer
- Upon receiving `ACK(n)` in window `[sendbase, sendbase + N]`:
	- Mark pkt `n` as received
	- If `n` is the smallest unACKed pkt, advance **window base** to the **next unACKed sequence number**

**Receiver:**
- For `packet(n)` in `[rcvbase, rcvbase + N + 1]`:
	- Send `ACK(n)`
	- If packet is out-of-order: Buffer
	- If in-order: Deliver all the buffered packets in order, **advance window** to the **next not-yet-received packet**
- For packet `n` in `[rcvbase - N, rcvbase - 1]`:
	- `ACK(n)`  must have already been sent!
- Otherwise: Ignore, do not send any ACK