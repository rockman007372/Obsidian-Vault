---
tags: CS2105 
aliases: 
Date: 2022-09-22 Thursday
---
Links: [[Transport Layer]]
- - -

UDP adds very little service on top of IP
- Multiplexing at sender:  gather data, form packages, pass to IP
- De-multiplexing at receiver: receive packets, dispatch to the right processes
- Checksum: Check for bits error

##### How does UDP handle de-multiplexing:
- **UDP receiver** checks destination port number in segment
- Directs segment to **UDP socket** with the same port number
- IP datagrams (segments) from different sources with the **same destination port number** will be directed to the same UDP socket at destination.

##### Why UDP?
- No connection establishment
- Simple: No connection state
- Small header size
- No congestion control → Faster transmission

##### UDP Header
![[Pasted image 20220910193731.png]]

##### UDP Checksum
Goal is to detect bit error during transmission. Sender compute checksum value and add to UDP header. Receiver compute checksum of received segment and **compare** with checksum header field to detect errors.

![[Pasted image 20220910194008.png]]