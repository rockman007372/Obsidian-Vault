---
tags: processed
course: CS2105
date: 2022-08-22 Monday
---
Links: [[Application Layer]]
- - -

- HTTP = HyperText Transfer Protocol
- It is a Web's **application layer protocol**
- Client-server model, where a client (such as a web browser) sends a request to a server (such as a web server), and the server responds with data or information
- **Uses TCP as transport service**
	- Client initiates TCP connection to server
	- Server accepts TCP connection request from client
	- HTTP messages are exchanged btw *browser* (client) and *Web server* over TCP connection.
	- TCP connection closed.
- **2 versions of HTTP:** 
	- [[Non-Persistent HTTP 1.0]]
	- [[Persistent HTTP 1.1]]
- [[RTT]] (Round-Trip Time) is an important concept to measure latency in HTTP.

## HTTP Message Format

### HTTP Request message

![[Pasted image 20220817020432.png]]

![[Pasted image 20220817020648.png]]

- Some methods: 
	- GET: Get webpage
	- POST: upload input in a form
	- HEAD: leave requested object, just ask for headers?
	- PUT: uploads file in entity body to path specified in URL field
	- DELETE: delete file in URL field

### HTTP Response message

![[Pasted image 20220817020929.png]]

- Sample status code: 
	- 200 OK
	- 301 Moved Permanently
	- 403 Forbidden
	- 404 Not Found

## Practice Questions
*Question 1*
A Web server contains 1 HTML file of size 10 bytes and 2 images of size 20 bytes each. Client is connected to server via a direct link of 100bps. RTT is 100ms. How much time does it take for clients to download the webpage via *non-persisten, non-parallel HTTP*?

![[The Application Layer 2022-08-17 02.21.04.excalidraw]]
ANS: 4.6s

*Question 2*
Same, but using *persistent HTTP with Pipelining*

![[The Application Layer 2022-08-17 02.26.14.excalidraw]]
