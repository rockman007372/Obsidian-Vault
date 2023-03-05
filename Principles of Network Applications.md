### Principles of Network Applications

*Classic structure* of network application:
-  Client-server
- Peer-to-Peer (Client download and upload at the same time)
	  
*Client-Server* Architecture: 
- Client: 
	- Initiate contacts with server
	- Request service from server
	- Implemented in browser for Web
- Server: 
	- Waits for incoming requests
	- Provides requested service to client
	- Data centers for scaling?

*P2P* Architecture:
- No server runing 24/7
- Arbitrary end systems (clients) directly communicate
- Peer request services from and provide services to other peers
- **self scalability:** new peers bring new service capacity and new service demands
- Peers are intermittenly connected and change IP addresses

What transport service does an app need?
- **Data integrity**
	- Some app requires 100% dta transfer (file transfer) while other apps can tolerate some data loss (video call)
- **Timing** (Online games need low delay)
- **Throughput** (difference vs timing?)
- **Security** (encryption, authentication)

**Application Layer Protocols** define:
- Type of messages (request/response)
- Message syntax (fields and how they are delineated)
- Message semantics
- Rules (when and how to send and respond)
- Open protocols (eg: HTTP, SMTP ? Available to everyone)
- Proprietary Protocols?

Application layer protocol **rides on** [[Transport Layer]] protocols to handle details like how to transmit messages:
- **TCP service**
	- reliable data transfer
	- flow control
	- congestion control
	- does **not** provide timing, min throughput, security
- UDP service (SHIT)