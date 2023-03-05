Socket is the **software interface** between app processes and transport layer protocol. It is like the link between application layer and transport layer.
- Process sends/receives messages to/from its sockets
- Applications (Processes) treat the Internet as a blackbox, sending and receiving messages through sockets.
- Comprised of a set of [[API]]s

![[Pasted image 20220828212153.png]]

**2 types** of sockets:
- [[UDP Socket]]: unreliable datagram socket
- [[TCP Socket]]: reliable, byte stream-oriented socket

## Comparison Between UDP and TCP Socket

In TCP, two processes communicate as if there is a pipe between them. The pipe remains in place until one of the two processes closes it. 
- When one of the processes wants to send more bytes to the other process, it simply writes data to that pipe. 
- The sending process **doesn’t need to attach a destination IP address and port number** to the bytes in each sending attempt as the logical pipe has been established (which is also reliable).
- IP and port number are still required, just that they are handled by the the TCP sockets and not programmers.  

In UDP, **programmers** need to form UDP datagram packets explicitly and attach destination IP address / port number to every packet.

## Difference between UDP and UDP socket

UDP is a network protocol used for sending and receiving datagrams, while a UDP socket is a programming interface that allows applications to create endpoints for sending and receiving UDP datagrams..