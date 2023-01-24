---
tags: processed
course: CS2105
date: 2022-08-28 Sunday
---
Links: [[Application Layer]]
- - -

## Process
A process is a **program** running within a host:
- Within the same host, 2 processes communicate using *inter-process communication* defined by OS
- Processes in different hosts communicate by *exchanging messages*  according to the protocol

IP addresses are used to identify a host, but it is *not sufficient to identify processes* running in that host (due to many concurrent processes in one host)

#### Addressing Processes
- A process is identified by **IP address** and **Port Number** (16 bit integer)
- Example port numbers: HTTP server = 80,  SMTP server = 25

## Sockets
Socket is the **software interface** between app process and transport layer protocol.
- Process sends/receives messages to/from its sockets
- Applications (Processes) treat the Internet as a blackbox, sending and receiving messages through sockets.
- Comprised of a set of [[API]]s

![[Pasted image 20220828212153.png]]

**2 types** of sockets:
- **UDP**: unreliable datagram socket
- **TCP**: reliable, byte stream-oriented socket

### UDP

In UDP: No connection is established btw client and server
- Client explicitly attaches destination IP address and port number to each packet
- Server extracts sender IP address and port number from the received packet.
- No live connection between server and client (unlike TCP)
- Many clients sockets mapped to 1 single server socket

![[Pasted image 20220828212548.png]]

![[Pasted image 20220828213420.png]]

#### UDP Server
```python
from socket import * 

serverPort = 2105 

# create a socket 
serverSocket = socket(AF_INET, SOCK_DGRAM) 

# bind socket to local port number 2105 
serverSocket.bind(('', serverPort)) 
print("Server is ready to receive message") 

# extract client address from received packet message with buffer = 2048 bytes
message, clientAddress = serverSocket.recvfrom(2048) 

# Echo message back to client
serverSocket.sendto(message, clientAddress) 

serverSocket.close()
```

#### UDP Client
```python
# client, server on the same host 
from socket import * 

serverName = 'localhost' 

serverPort = 2105 

clientSocket = socket(AF_INET, SOCK_DGRAM) # SOCK_DRGAM, not STREAM!! 

message = input('Enter a message: ') 

# send msg to server address - must encode msg to bytes
clientSocket.sendto(message.encode(), (serverName, serverPort)) 

# receive message from server - must decode msg to string
receivedMsg, serverAddress = clientSocket.recvfrom(2048) 
print('from server:', receivedMsg.decode()) 

clientSocket.close()
```

### TCP

Read detailed instructions to set up a TCP server [here](<https://realpython.com/python-sockets/#:~:text=Python's%20socket%20module%20provides%20an,socket()>)

When client creates socket, client TCP establishes a connection to server TCP. 
- When contacted by a client, server TCP **creates a new socket** for server process to communicate with that particular client. 
- Allows server to talk with **multiple clients individually** (1 to 1 mapping).

![[Pasted image 20220828213844.png]]

![[Pasted image 20220828213930.png]]

More detailed program flow:
![[Pasted image 20220915113204.png]]

#### Server
```Python
from socket import * 

serverPort = 2105 

# Create the first welcome socket to coordinate other sockets by listening to clients' connection request
serverSocket = socket(AF_INET, SOCK_STREAM) # → Take in byte stream! 

serverSocket.bind(('', serverPort)) 

serverSocket.listen() # Listen to incoming TCP request
print('Server is ready to receive message') 

connectionSocket, clientAddr = serverSocket.accept() # return a NEW SOCKET to communicate with the client socket 

message = connectionSocket.recv(2048) # buffer = 2048 bytes

connectionSocket.send(message) # No need address

connectionSocket.close()
```

#### Client
```Python
from socket import * 

serverName = 'localhost' 
serverPort = 2105 

clientSocket = socket(AF_INET, SOCK_STREAM) 
clientSocket.connect((serverName, serverPort)) # Establish a TCP Connection with server 

message = input('Enter a message: ')

clientSocket.send(message.encode()) # no need to attach client server name and port number

receivedMsg = clientSocket.recv(2048) 

print('from server:', receivedMsg.decode()) 

clientSocket.close()
```

### Comparison
In TCP, two processes communicate as if there is a pipe between them. The pipe remains in place until one of the two processes closes it. 
- When one of the processes wants to send more bytes to the other process, it simply writes data to that pipe. 
- The sending process **doesn’t need to attach a destination IP address and port number** to the bytes in each sending attempt as the logical pipe has been established (which is also reliable).
- IP and port number are still required, just that they are handled by the the TCP sockets and not programmers.  

In UDP, **programmers** need to form UDP datagram packets explicitly and attach destination IP address / port number to every packet.
