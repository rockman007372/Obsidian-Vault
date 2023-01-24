---
tags: processed
course: CS2105
type: lecture
---
Date:: 2022-08-15 Monday
Links: [[CS2105]]
- - -

## Practice Questions

*Question 1*: A Web server contains 1 HTML file of size 10 bytes and 2 images of size 20 bytes each. Client is connected to server via a direct link of 100bps. RTT is 100ms. How much time does it take for clients to download the webpage via *non-persisten, non-parallel HTTP*?

![[The Application Layer 2022-08-17 02.21.04.excalidraw]]
ANS: 4.6s

*Question 2*: Same, but using *persistent HTTP with Pipelining*

![[The Application Layer 2022-08-17 02.26.14.excalidraw]]

##### Lecture 3 Quizz
![[Lecture_3_qns.pdf]]

## Notes
#### ![[Network Protocols]]
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

- What transport service does an app need?
	- **Data integrity**
		- Some app requires 100% dta transfer (file transfer) while other apps can tolerate some data loss (video call)
	- **Timing** (Online games need low delay)
	- **Throughput** (difference vs timing?)
	- **Security** (encryption, authentication)

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
		- does **not** provide timing, min throughput, security
	- UDP service (SHIT)

### Web 
- A webpage typically consists of:
	- base HTML file
	- several referenced objects (png, jpeg, mp3...)
		- Each object is addressable by an **URL**: http://www.comp.nus.edu.sg/~cs2105/img/doge.jpg
		- `www.comp.nus.edu.sg/...`: host name
		- `.../~cs2105/img/doge.jpg`: path name
- See also: [[How Does Websites Work]]

### HTTP (IMPORTANT)
See [[HTTP]]

### Cookies
See [[Cookies]]

### DNS
See [[DNS]]

[How does HTTP and DNS work together](https://www.easyredir.com/blog/how-http-dns-work-together-to-make-url-redirects-happen/)

### Socket Programming
See [[Socket Programming]]

## Practice Questions
![[Lec_3_discussion.pdf]]