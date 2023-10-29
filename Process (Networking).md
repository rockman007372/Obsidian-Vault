A process is a **program** running within a host:
- Within the same host, 2 processes communicate using *inter-process communication* defined by OS (IPC)
- In different hosts, processess communicate by *exchanging messages*  according to a protocol

IP addresses are used to identify a host, but it is *not sufficient to identify processes* running in that host (due to many concurrent processes in one host).

Hence, a process is identified by **IP address** and **Port Number** (16 bit integer)

Example port numbers: HTTP server = 80,  SMTP server = 25