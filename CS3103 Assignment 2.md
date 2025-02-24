### Question 1

1a)
![[Pasted image 20240913190751.png]]

IP address: **103.243.175.98**

The server is (not) hosted inside NUS.

1b)

![[Pasted image 20240913194110.png]]

The 2 mail servers are 
- 84-101.comp.nus.edu.sg at **137.132.84.101**
- 84-102.comp.nus.edu.sg at **137.132.84.102**

### Question 2

`#openssl`

![[Pasted image 20240913200024.png]]

`#EHLO gmail.com`

![[Pasted image 20240913200158.png]]

`#AUTH LOGIN` and crafting email

![[Pasted image 20240913204144.png]]

Email received:

![[Pasted image 20240913204229.png]]

### Question 3

HTTP Request line:
![[Pasted image 20240913204622.png]]

- Host: The server host where the request is sent to (varlabs.comp.nus.edu.sg)
- user-agent: The client making the request (browser type, version, operating system, and sometimes the application). In this case, the agent is curl running version 7.58.0.
- accept: The content types that the client is able to process and prefers to receive from the server. It helps the server to determine the most appropriate response format (e.g., HTML, JSON, XML, plain text). In this case, the client accept any MIME type (Multipurpose Internet Mail Extensions).

HTTP response status line:

![[Pasted image 20240913204713.png]]

- server: the software running on the server that handles the request (nginx version 1.10.2)
- date: date and time at which the server produces the response.
- content-type: the MIME media type of the resource in the response. In this case, it is an HTML document.
- content-length: the size of the response body in bytes (186B in this case).
- last-modified: The date and time the requested resource was last modified.
- etag: a unique identifier assigned to a specific version of a resource. It’s used for **cache validation** and helps clients determine if a resource has changed since the last time it was requested.
- accept-ranges: a marker used by the server to advertise its support for **partial requests** from the client for file downloads. The value of this field indicates the **unit that can be used to define a range**. 
- x-content-type-options: a security feature that prevents browsers from interpreting files as a different MIME type than what is specified in the Content-Type header. In this case,`nosniff` prevents MIME type sniffing.
- x-frame-options: a security feature that controls whether a browser should be allowed to render a page in a `<frame>`, `<iframe>`, `<embed>`, or `<object>`. It helps prevent clickjacking attacks. In this case, the value`SAMEORIGIN` dictates that the only pages/frames from the same origin as the ancestor frames can be displayed.
- cache-control: controls how, for how long, and under what conditions the response can be cached. `max-age=300` means the response remains fresh (reusable for other requests) until _300_ seconds after the response is generated.
- strict-transport-security:  informs browsers that the site should only be accessed using HTTPS, and that any future attempts to access it using HTTP should automatically be converted to HTTPS.
	- `max-age=315360000` means that browser will remember the site is accessible by HTTPS only for 315360000 seconds.
	- `includesubdomains` means this HTTPS-only access is applies to all of the site's subdomains as well.
- set-cookie: send a cookie from the server to the user agent, so that the user agent can send it back to the server later. 
	- `path=/` means the cookie will be sent with requests to all paths on the domain (i.e., it’s available site-wide).
	- `Secure`  means that the cookie will only be sent to the server over HTTPS.
	- `HttpOnly` makes the cookie inaccessible to JavaScript running on the client side.

### Question 4

HTTP/2: Takes 222ms to download all objects and load page. 
![[Pasted image 20240913212045.png]]

HTTP/3: Takes 219ms to download all objects and load page.
![[Pasted image 20240913212232.png]]

Hence, HTTP/3 is only slightly faster than HTTP/2. 

Which is faster and why?
- HTTP/3 is faster than HTTP/2
- because **HTTP/3** uses **QUIC (Quick UDP Internet Connections)**, a transport protocol that runs over **UDP (User Datagram Protocol)** which is much faster than **TCP (Transmission Control Protocol)** which HTTP/2 relies on.

Why is HTTP3 faster than HTTP1? 
- HTTP/1 relies on TCP, which requires a 3-way handshake (SYN, SYN-ACK, ACK) to establish a connection. This adds to a fixed initial RTT overhead before any actual data transfer begins.
- HTTP/3 uses QUIC, which integrates connection setup and TLS encryption into **a single handshake process**. This can reduce RTT significantly because it consolidates what would be multiple round trips in HTTP/1 into one or even zero round trips with cached connection data.
##### Report

ChatGPT prompts:
- Why is HTTP/3 faster than HTTP/2?
- Why not adopt QUIC? Why are we still using TCP?
- Does this advantage of HTTP3 applies for smaller payload (e.g. fetching a single file) compared to HTTP1 or 2?
- What is head of line blocking and how does QUIC solve it?

I used ChatGPT for a quick high-level summary of the features of HTTP/3, and why is is considered better than HTTP/2. While ChatGPT is pretty decent at summarizing key features, it does a pretty poor job at explaining them on more technical grounds, instead resorting to generic phrases and ideas that do not value-add. Therefore, I also complemented it with my own Google search of the key features to gain a more detailed understanding of the features of HTTP3 and QUIC. For example, ChatGPT did not explain well what HOL blocking is and how QUIC solves it. After Googling, I stumbled accross multiple StackOverflow forums and Medium articles with detailed explanation and even visual illustrations of these concepts, making me understand them more deeply. Therefore, I believe ChatGPT is excellent at introducing concepts and surface-level ideas, but to gain a deeper understanding one must do their own research and internalize the content carefully. 

As I did more research about QUIC, I also stumbled accross strong opinions from network engineers against its adoption. For example, they believe the transmission time improvement from reducing the number of network handshakes is too negligible to justify disrupting the current long-standing and robust transport layer. Furthermore, they believe the transport layer is not the bottleneck for slow page load time, but due to bad network infrastructure and poor web development practices. Lastly, QUIC runs on UDP, which is stateless, which makes it difficult for provision, secure and troubleshoot. 