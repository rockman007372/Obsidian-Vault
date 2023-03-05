## 2 Modes of Data Transmission

### Circuit Switching
**Circuit Switching**: Used in traditional telephone network.
- End-end resources allocated to and reserved for call between source and dest.
- Call set-up required.
- *Circuit-like* performance (Guaranteed)
- No sharing of circuit → Not enough circuit, cannot use network

### Packet Switching

**Packet Switching**: Used by the *Internet*.
- Data is broken into smaller chunks = packet of *length L bits*
- When receivers receive all the packets, they are *combined and restored*.
- Packets are sent as a sine/cosine waves.

**Transmission rate R** (**Link capacity** or **bandwidth**): the **ideal** rate of transmitting bits - how many bits transmitted in one second?
- eg: Bandwidth = 1 GBPS (Gigabits per Second)
- Packet transmission delay = time needed to transmit L-bit packet into link  $$\frac{L \text{ (bits)}}{R \text{ (bits per sec)}}$$
- Packets are passed from one router to the next, across links from source to dest

**Store and forward**: entire packet must arrive at a router before it can be transmitted to another router  on the next link.
- Why? Router needs to receive and verify the integrity of the whole packet before transmitting! If corrupted packet, discard it.
- End-to-End delay *with a router in between* = total delay from source to dest = $2 * (L / R)$ where R is the rate of delay. 
- Without middle router, end-to-end delay = $L / R$.
- How do routers determine source-destination route taken by packets?  → **Routing algorithm**
- **Addressing**: each packet needs to carry source and destination info

## Who owns the Internet? 
Each ISP has their own networks which connect to each other to form the Internet. Internet is not owned by a single org. The *Internet is a network of networks*, organized into Autonomous System, each is owned by an organization.