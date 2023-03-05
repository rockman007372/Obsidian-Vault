Non-persistent HTTP 1.0 is an early version of the HTTP protocol that was widely used in the early days of the World Wide Web. Non-persistent HTTP 1.0 is called "non-persistent" because it does not maintain a persistent connection between the client and server for multiple requests and responses.

In non-persistent HTTP 1.0, the client opens a new connection to the server for each request it makes, and the server closes the connection after sending the response. This means that each request-response cycle incurs the overhead of opening and closing a new TCP connection, which can result in slower performance and higher network usage.

Characteristics:
- 1 object per TCP connection
- Connection is closed after one object is downloaded
- Downloading multiple objects require multiple connections
- Variation: **Multiple simultaneous TCP**

![[The Application Layer 2022-08-17 00.44.52.excalidraw||]]

![[Non-Persistent HTTP 1.0 2023-03-02 16.43.04.excalidraw||500]]

