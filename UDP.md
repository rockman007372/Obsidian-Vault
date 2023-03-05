---
tags: CS2105 
aliases: 
Date: 2022-09-22 Thursday
---
Links: [[Transport Layer]]
- - -

UDP (User Datagram Protocol) is a protocol used for sending and receiving datagrams over a network. 

It is a connectionless protocol that does **not** guarantee reliable delivery of data, does not provide flow control, and does not implement congestion control. 

UDP is often used for applications that require low latency and can tolerate some data loss, such as real-time audio and video streaming, online gaming, and DNS.


UDP adds very little service on top of IP
- Multiplexing at sender:  UDP gathers data from different processes, form packets and pass them to IP
- De-multiplexing at receiver: UDP receive packets, dispatch to the right processes.
- Checksum: Check for bits error

##### How does UDP handle de-multiplexing:
- **UDP receiver** checks destination port number in segment
- Directs segment to **UDP socket** with the same port number
- IP datagrams (segments) from different sources with the **same destination port number** will be directed to the same UDP socket at destination.

##### Why UDP?
- No connection establishment
- Simple: No connection state
- Small header size
- No congestion control → **Faster** transmission

##### UDP Header
![[Pasted image 20220910193731.png]]

##### UDP Checksum
Goal is to detect bit error during transmission. Sender compute checksum value and add to UDP header. Receiver compute checksum of received segment and **compare** with checksum header field to detect errors.

![[Pasted image 20220910194008.png]]