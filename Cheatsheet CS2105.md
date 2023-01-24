# How Is Internet Data Transmitted

### The Internet
- The Internet is a network of connected computing devices.
	- Such devices are **hosts/end systems**
	- Hosts run network **applications** (Zoom, Telegram?)
	- Hosts communicate over links
  
### Network Edge vs Network Core
- *Network Edge*: where normal users access the Internet
	- Hosts access the Internet through access network (ways to access the internet)
	- When you subscribe to ISP (Internet Service Provider), you get a *modem* which connects home network to ISP network. You also get a *router* to set-up home network (eg: connect all home devices, set up firewall services...)
	- In school you connect to NUS network through WIFI or cables.

- *Network Core*: An array of interconnected routers. Belong to some big company.
	- Routers are like *mini specially designed computers* used to forward data in the network.
	- Routers have many ports where you can plug in many cables.
- How is data transmitted through network?
	- Circuit Switching
	- Packet Switching

### How is Data Transmitted?
- **Circuit Switching**: Used in traditional telephone network.
	- End-end resources allocated to and reserved for call between source and dest.
	- Call set-up required.
	- Circuit-like performance (Guaranteed)
	- No sharing of circuit → Not enough circuit, cannot use network

- **Packet Switching**: Used by the Internet.
	- Data is broken into smaller chunks = packet of *length L bits*
	- When receivers receive all the packets, they are *combined and restored*.
	- Packets are sent as a sine/cosine waves.
	- *Transmission rate R* (Link capacity or link bandwidth): How fast does it take to transmit the bits.
	- eg: Bandwidth = 1 GBPS (Gigabits per Second)
	- Packet transmission delay = time needed to transmit L-bit packet into link = $\frac{L \text{ (bits)}}{R \text{ (bits per sec)}}$
	- Packets are passed from one router to the next, across linkes from source to dest
	- *Store and forward*: entire packet must arrive at a router before it can be transmitted to another router  on the next link.
	- Why? Router needs to receive and verify the integrity of the whole packet before transmitting! If corrupted packet, discard it.
	- End-to-End delay *with a router in between* = total delay from source to dest = $2 * (L / R)$ where R is the rate of delay. Without middle router, delay = $L / R$.
	- How do routers determine source-destination route taken by packets?  → **Routing algorithm**
	- **Addressing**: each packet needs to carry source and destination info
- Who own the Internet? Each ISP has their own networks which connect to each other to form the Internet. Internet is not owned by a single org. The *Internet is a network of networks*, organized into Autonomous System, each is owned by an organization.

### Delay, Loss and Throughput

Packet *queue* in router buffers: Packets wait to be sent out by a router in a FIFO (First In First Out) manner. 
- Queue has finite capacity
- What if packet arrival rate exceeds departure rate? Packets can be discarded by routers and lost in the network → *Network overflow*

Packets (propagated as waves) can be corrupted by noise waves (routers detect corrupted waves and interpret 1 as 0 for example)

**Four** sources of packet delays:
- **Nodal processing** delay: check bit errors (protect packet integrity), very short (<msec) before sending to the queue (*neglibigle*)
- **Queuing** delay: time waiting in the queue (*negligible*)
- **Transmission** delay: 
	- packets are sent bits by bits into the wire
	- Tranmission delay = time to push ALL bits into the wire (time between the first and the last bit)
	- Independent of distance 
	- delay = $L / R$, where L is the number of bits and R is the transmission rate.
- **Propagation** delay: every bit is transmitted as a wave 
	- delay = $d / s$ 
	- d: length of physical link, s is propagation speed in medium

![[Pasted image 20220808143222.png]]

Fewer users → queue and processing delay are faster → Queue and processing delays are *variables* dependent on number of users.

**Throughput**: How many bits can be transmitted per unit time.
- Measured for end-end communication (*inclusive of delays*)
- Link capacity (bandwidth) is meant for a specific link, *usually greater than throughput*

$$Throughput = \frac{\text{total bits}} {\text{total time}}$$

# The Application Layer

### Principles of Network Applications
- *Classic structure* of network application:
	- Client-server
	- Peer-to-Peer (Client download and upload at the same time)
	  
- *Client-Server* Architecture: 
	- Client: 
		- Initiate contacts with server
		- Request service from server
		- Implemented in browser for Web
	- Server: 
		- Waits for incoming requests
		- Provides requested service to client
		- Data centers for scaling?

- *P2P* Architecture:
	- No server runing 24/7
	- Arbitrary end systems (clients) directly communicate
	- Peer request services from and provide services to other peers
		- **self scalability:** new peers bring new service capacity and new service demands??
	- Peers are intermittenly connected and change IP addresses

- **Application Layer Protocols** define:
	- Type of messages (request/response)
	- Message syntax (fields and how they are delineated)
	- Message semantics
	- Rules (when and how to send and respond)
	- Open protocols (eg: HTTP, SMTP ? Available to everyone)
	- Proprietary Protocols?

- Application layer protocol **rides on** [[Transport Layer]] protocols to handle details like how to transmit messages:
	- **TCP service**
		- reliable data transfer
		- flow control
		- congestion control
		- does **not** provide timing, minimum throughput, security
	- UDP service (SHIT)

### HTTP (IMPORTANT)
- **Uses TCP as transport service**
	- Client initiates TCP connection to server
	- Server accepts TCP connection request from client
	- HTTP messages are exchanged btw *browser* (client) and *Web server* over TCP connection.
	- TCP connection closed.
- **2 versions:** 
	- *Non-Persisten HTTP 1.0* 
		- 1 object per TCP connection
		- connection is closed after one object is downloaded
		- downloading multiple objects require multiple connections
		- Variation: **Multiple simultaneous TCP**
	- *Persistent HTTP 1.1*
		- multiple objects per TCP connection
		- Variation: **Pipelining (all objects sent simultaneously)**
- **RTT**
	- RTT is the time for a packet to travel from client to server and back
	- Non-persistent HTTP response time = 2 * RTT + file transmission time.

![[Pasted image 20220817020108.png]]

### Cookies
- HTTP messages contain cookie header field
- Cookie file is kept on **user**'s host, managed by browsers
- Cookies are processed by back-end database at Web **servers**

![[Pasted image 20220817021408.png]]

Conditional GET:

![[Pasted image 20220817021653.png]]

### DNS
Two ways to identify a host:
- Hostname: http://www.example.org/
- IP address: 93.184.216.34

**DNS** (Domain Name System) translates between Hostname and IP address.

A client must carry out a DNS query to determine the IP address of the corresponding server name prior to the connection (before it can establish TCP connection and send HTTP request)

Mapping between Hostnames and IP addresses are stored as **R**esource **R**ecord (RR)

> RR format: (name, value, type, ttl)

Some common types in RR format:
- type = A
	- **name** is hostname
	- **value** is IP address
- type = NS
	- **name** is domain (nus.edu.sg)
	- **value** is hostname of authoritative name server for this domain
- type = CNAME
	- **name** is alias name for some real name (eg: www.nus.edu.sg)
	- **value** is real/canonical name (mgnzsqc.x.incapdns.net)
- type = MX
	- **value** is name of *mail server* associated with the **name**

Hierarchy: Root servers → Top-level Domain server → Authoritative Servers
- **Root servers:** Divided into 13 root zones based on geography
- **Top-level Domain servers:** responsible for com, org, net, edu, … and all top-level country domains, e.g., uk, sg, jp
- **Authoritative servers:** Organisations' own DNS servers, providing *authoritative hostname to IP mappings* for the org's named hosts

![[Pasted image 20220828203453.png]]

#### Local DNS server
- Does not strictly belong to hierarchy
- Each ISP (Intenet Service Provider) has one local DNS server - AKA "default name server".
- When a host makes a DNS query, query is *sent to its local DNS server* → Retrieve name-to-address translation from *local cache* → If answer is not found, local DNS asts as proxy and forward query into hierarchy.
- Once a name server learns mapping, it caches mapping
	- Cached address can be out-of-date
	- Cached entries expire after **Time-To-Live (TLL)** runs out.
	- If name host changes IP address, may not be known internet-wide until TLL expires.
- DNS runs over **UDP** → Fast

### Socket 
- A process is identified by **IP address** and **Port Number** (16 bit integer)
- Socket is the **software interface** between app process and transport layer protocol.
	- Process sends/receives messages to/from its sockets
	- Applications (Processes) treat the Internet as a blackbox, sending and receiving messages through sockets.
- **2 types** of sockets:
	- **UDP**: unreliable datagram socket
	- **TCP**: reliable, byte stream-oriented socket

### UDP Socket
![[Pasted image 20220828212548.png]]
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
clientAddress = serverSocket.recvfrom(2048) 

# Echo message back to client
serverSocket.sendto(message, clientAddress) 

serverSocket.close()
```

#### UDP Client
```python
# client, server on the same host 
from socket import * serverName = 'localhost' 

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

### TCP Socket
- When contacted by a client, server TCP **creates a new socket** for server process to communicate with that particular client. 
- Allows server to talk with **multiple clients individually** (1 to 1 mapping).

![[Pasted image 20220828213844.png]]

![[Pasted image 20220828213930.png]]

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

## Transport Layer

### UDP
UDP adds very little service on top of IP
- Multiplexing at sender:  gather data, form packages, pass to IP
- De-multiplexing at receiver: receive packets, dispatch to the right processes
- Checksum: Check for bits error

##### How does UDP handle de-multiplexing:
- **UDP receiver** checks destination port number in segment
- Directs segment to **UDP socket** with the same port number
- IP datagrams (segments) from different sources with the **same destination port number** will be directed to the same UDP socket at destination.

##### UDP Header
![[Pasted image 20220910193731.png]]

##### UDP Checksum
1. Treat UDP segment as sequence of 16 bit integers
2. Apply binary addition on every integer
3. Carry will be added to the result
4. At the end, compute 1s complement by inverting all the bits

### Reliable Data Transfer

Underlying network layer may:
- *Corrupt* packets
- *Drop* packets
- Re-order packets (not considered rn?)
- Deliver packet after long *delay*

#### Different versions of RDT
![[Pasted image 20220910220417.png]]

#### RDT 2.0: Data Bit Error

![[Pasted image 20220910221028.png||700]]

#### RDT 2.1: ACK/NAK Bit Error
Fatal flaw of 2.0 is ACK and NAK can also have bit errors → Need to resend package, but do not know whether package is received or not → **Packet Sequence Number**

![[Pasted image 20220910221602.png||730]]

#### RDT 2.2: NAK-Free

Instead of sending NAK, receiver sends ACK for the last packet received OK → Receiver must explicity include sequence # of the packet being ACKed

![[Pasted image 20220910222040.png]]

#### RDT 3.0: Packet Loss
In RDT 3.0, the sender relies on **timeout** to resolve both packet loss and packet corruption! → Sender and receiver do nothing and wait for timeout.

There are **3 scenarios** for packet loss:
1. Packet is **lost** or **corrupted** → receiver does nothing, sender waits for timeout and resend
 ![[Pasted image 20220910222316.png]]
2. ACK is **lost** or **corrupted** → Sender does nothing , also wait for timeout
![[Pasted image 20220910222349.png]]
3. ACK is **delayed**:
![[Pasted image 20220910222506.png]]

RDT's performance is pretty ass, due to the stop-and-wait operation
![[Transport Layer 2022-09-10 22.29.56.excalidraw]]

### GBN 

Key features: Send multiple packets, if packet N is not received, **discard** subsequent packets after N and **resend ACK N** to signal N is not received. Once there is timeout or ACK N is received, resend packet N and all the subsequent packets in the window.

**GBN Sender:**
- Have up to N unACKed packets in pipeline
- Insert k-bits sequence number in header
- Use **[[Sliding Window]]** to keep track of unACKed packets
- Keep a timer for the oldest **unACKed** packet
- `timeout(n)`: Retransmit packet n and all subsequent packets in the window 

**GBN Receiver:**
- Only ACK packets that arrive in order 
- Discard out of order packets and ACK the *last in-order* sequence number → *Cumulative ACK*: ACK m means all packets up to m are received

![[Pasted image 20220910225503.png]]

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
- Otherwise: Ignore → WTF DO YOU MEAN

### TCP
- Point-to-point: One sender, one receiver
- **Connection**-oriented: Handshaking before sending app data
- Full duplex service: Bidirectional data flow in the same connection
- Reliable, in-order byte stream: Use sequence numbers to label bytes
- A TCP connection (socket) is identified by a 4-tuple: 
	- `(srcIPAdddr, srcPort, destIPAdress, destPort)`
	-  Receiver uses all 4 values to direct data segments to the appropriate socket
![[Pasted image 20220922181409.png]]
- TCP send and receiver data in **buffers** → Dont have to discard out-of-order packets
- How much app-layer data can a TCP segment carry depends on **MSS** (Maximum segment size) → MSS is **NOT** inclusive of TCP headers

#### TCP header format

![[Pasted image 20220922181847.png]]

Components:
- Sequence number: the byte number of the **first** byte of data in the segment
- ACK number: the byte number of the **next** byte of data expected by the receiver
- TCP ACKS are up to the first missing byte in the stream → **Cumulative ACK**

![[Pasted image 20220922182139.png]]

#### TCP Echo Server
- **Bidirectional** data flow in the same TCP connection
- Continuously echoing the message received while sending new data

![[Pasted image 20220922182857.png]]

#### TCP ACK generation at receiver

![[Pasted image 20220922184147.png]]

![[Pasted image 20220922184413.png]]

## TCP Timeout Value
- Too short: Unneccessary retransmission
- Too long: Unresponsive to pkt loss
- Ideally timeout is just longer than RTT → Unfortunately, RTT varies

## TCP Fast Retransmission
- Event: If the sender receives 4 ACKs of the same segment, it supposes the segment is lost
- Action: Resend the segment before the timer expires → Responsive to segment loss

## Establising and Ending TCP Connection

Before client and server can exchange app data, must establish 3-way handshake:
![[Pasted image 20220922185006.png]]

Client and Server take turns to close connection:
![[Pasted image 20220922190516.png]]