Persistent HTTP 1.1 is a version of the HTTP protocol that introduced persistent connections, **allowing the client and server to reuse the same TCP connection for multiple requests and responses**. Persistent connections are also known as keep-alive connections.

In persistent HTTP 1.1, after the server sends the response to the client's request, the connection is kept open, allowing the client to send additional requests over the same connection without the need to establish a new connection each time. The server can also send additional responses over the same connection, if necessary.

Persistent connections in HTTP 1.1 can improve the performance of web applications by reducing the overhead of establishing new TCP connections for each request. This can result in faster response times and lower network usage, especially for applications that require many small requests.

HTTP 1.1 also introduced support for pipelining, which allows multiple requests to be sent over a single connection without waiting for each response. Pipelining can further improve performance by reducing the latency between requests and responses.

Characteristics:
- multiple objects per TCP connection
- Variation: **Pipelining (all objects sent simultaneously)**

![[The Application Layer 2022-08-17 01.07.20.excalidraw]]
