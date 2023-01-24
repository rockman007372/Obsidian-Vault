---
tags: process
course: CS2105
type: lecture
---
Date:: 2022-08-07 Sunday
Links: [[How Does The Internet Work]] - [[CS2105]]
- - -

## Notes
### The Internet
- The Internet is a network of connected computing devices.
	- Such devices are **hosts/end systems**
	- Hosts run network **applications** (Zoom, Telegram?)
	- Hosts communicate over links
- 1.01 billions hosts rn on the Internet
  
### Network Edge vs Network Core
- *Network Edge*: where normal users access the Internet
	- Hosts access the Internet through access network (ways to access the internet)
	- When you subscribe to ISP (Internet Service Provider), you get a *modem* which connects home network to ISP network. You also get a *router* to set-up home network (eg: connect all home devices, set up firewall services...)
	- In school you connect to NUS network through WIFI or cables.
	- **WIFI** (Wireless LAN), restricted by distance
	- **Wide-area Wireless Access** (NOT Wifi): such as 4G, provided by ISP
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
	- **Transmission rate R** (**Link capacity** or link **bandwidth**): the **ideal** rate of transmitting bits - how many bits transmitted in one second?
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
See [[Delays, Loss and Throughput]]

### Summary
- Internet is a packet-switching network
- User A, B... 's packets share network resources
- Resources are used on demand
- Congestion can happen, Internet is slow and some packets may be lost.


## Questions

Q1. Difference between bandwidth and latency?
- Latency is the time taken to travel end to end - basically delay
- Bandwidth is the total amount of data travelled in one second from end to end → Transmission rate / link bandwidth
- Latency says nothing about of bandwidth. You can travel very fast from A to B, but if the bandwidth is low, bits are not transmitted into link fast enough.