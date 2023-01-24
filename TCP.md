---
tags: 
aliases: 
date:: 2022-09-22 Thursday
---
Links: [[Transport Layer]]
- - -

## Characteristics
- Point-to-point: One sender, one receiver
- **Connection**-oriented: Handshaking before sending app data
- Full duplex service: Bidirectional data flow in the same connection
- Reliable, in-order byte stream: Use sequence numbers to label bytes
- A TCP connection (socket) is identified by a 4-tuple: 
	- `(srcIPAdddr, srcPort, destIPAdress, destPort)`
	-  Receiver uses all 4 values to direct data segments to the appropriate socket

![[Pasted image 20220922181409.png]]

- TCP send and receiver data in **buffers** → Dont have to discard out-of-order packets

![[Pasted image 20221002122122.png]]

- How much app-layer data can a TCP segment carry depends on **MSS** (Maximum segment size) → MSS is **NOT** inclusive of TCP headers

## TCP header format

![[Pasted image 20220922181847.png]]

Components:
- Sequence number: the byte number of the **first** byte of data in the segment
- ACK number: the byte number of the **next** byte of data expected by the receiver
- TCP ACKS are up to the first missing byte in the stream → **Cumulative ACK**

![[Pasted image 20220922182139.png]]

## TCP Echo Server
- **Bidirectional** data flow in the same TCP connection
- Continuously echoing the message received while sending new data

![[Pasted image 20220922182857.png]]

## TCP ACK generation **at receiver**

![[Pasted image 20220922184147.png]]

| Event                                                                                                | Action                                                                                     |
| ---------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| Arrival of **in-order** segment with expected sequence no. All data up to expected seq no. are ACKEd | Delayed ACK: wait up to 500ms for the next segment. If no next segment, send ACK           |
| Arrival of **in-order** segment with expected seq no. One other segment has ACK pending.             | Immediately send single **cumulative** ACK, ACK-ing both segment                           |
| Arrival of **out-of-order** segment with higher than expected seg. number.                           | Immediately send **duplicate ACK**, indicating sequence no. of the **next** expected byte |
| Arrival of segment that partially or completely fills the gap.                                       | Immediately send the next ACK, either at the next gap or the most recent segment           |
                        
![[Pasted image 20220922184413.png]]

## TCP Timeout Value
- Too short: Unneccessary retransmission
- Too long: Unresponsive to pkt loss
- Ideally timeout is just longer than RTT → Unfortunately, RTT varies

## TCP Fast Retransmission
- Event: If the sender receives 4 ACKs of the same segment, it supposes the segment is lost
- Action: Resend the segment before the timer expires → Responsive to segment loss
![[Pasted image 20220922184810.png]]

## Establising and Ending TCP Connection

Before client and server can exchange app data, must establish 3-way handshake:
![[Pasted image 20220922185006.png]]

Client and Server take turns to close connection:
![[Pasted image 20220922190516.png]]