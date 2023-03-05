## TCP Socket

Read detailed instructions to set up a TCP server [here](<https://realpython.com/python-sockets/#:~:text=Python's%20socket%20module%20provides%20an,socket()>)

When client creates socket, client TCP establishes a connection to server TCP. 
- When contacted by a client, server TCP **creates a new socket** for server process to communicate with that particular client. 
- Allows server to talk with **multiple clients individually** (1 to 1 mapping).

![[Pasted image 20220828213844.png]]

![[Pasted image 20220828213930.png]]

More detailed program flow:

![[Pasted image 20220915113204.png]]

### TCP Server

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

### TCP Client

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