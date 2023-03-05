## UDP Socket

In UDP: No connection is established btw client and server
- Client explicitly attaches destination **IP address** and **port number** to each packet
- Server extracts sender IP address and port number from the received packet.
- No live connection between server and client (unlike TCP)
- Many clients sockets mapped to 1 single server socket

![[Pasted image 20220828212548.png]]

![[Pasted image 20220828213420.png]]

### UDP Server

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

### UDP Client

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