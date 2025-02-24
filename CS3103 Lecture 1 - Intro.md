---
tags:
  - toProcess
course: CS3103
type: lecture
date: 2024-08-27 Tuesday
---

## Notes

IXP: Internet Exchange Point
- physical location through which internet infra companies connect to exchange internet traffic
- **Tier 1 networks can exchange traffic with other Tier 1 networks without paying any fees for the exchange of traffic in either direction**. In contrast, some Tier 2 networks and all Tier 3 networks must pay to transmit traffic on other networks

Internet Protocol Stack:
1. Application: HTTP
2. Transport: TCP, UDP
3. Network (Internet): IP, routing protocols
4. Link: Ethernet
5. Physical: bits on the wire (hardware)

Default gateway: 
- a device on the network that serves as access point or ip router to other networks
- usually a router or switch that routes traffic from local network to the Internet

DHCP: Dynamic Host Config Protocol
- automatically assign IP addresses to devices on a network
- When a device connects to a network, it sends a broadcast message (DHCP Discover message) to the network to request for IP addr
- How does a new device know the ip address of DHCP server? No need, just broadcast to the whole network, it will reach DHCP server

How does Ethernet know the packet received is an IP packet? Link layer header should have info about payload data type

Classful addressing vs Classless addressing?
- Classful: 
	- older method, divide IP addrs space into fixed classes (A, B, C, D, E) based on leading bits
	- Wasteful addressing: entire classes are allocated regardless of network size (a class B block has 2^16 - 2 addresses, while class C block only has 2^8 - 2)
- Classless: 
	- variable-length subnet mask (VLSM) ⇒ network prefix is any length

IP subnet addressing:
- Borrow bits from host part to divide large network into smaller subnets
- First and last subnet are unusable

Supernetting:
- Merging smaller networks into a large network w a single prefix
- Remove bits from network and add to host

Private IP address:
- not globally unique, save costs for org
- Needs a NAT (Network Address Translation) to translate private IP to public IP
- NAT router maps `<private IP, private port number>` to `<public IP, public port num>`. Public port number is basically primary key to identifies private IP.

## Summary

## Questions/Cues

1. Difference btw network identification and broadcast address?
	- **Function**:
	    - **Network Address**: Identifies the subnet and is used to route packets to the correct network.
	    - **Broadcast Address**: Allows communication with all devices on the subnet simultaneously.
	- **Address Range**:
	    - **Network Address**: The first address in the subnet, with all host bits set to zero.
	    - **Broadcast Address**: The last address in the subnet, with all host bits set to one
	- **Example**:
		- **Network Address**: For the subnet `192.168.1.0/24`, the network address is `192.168.1.0`.
		- **Broadcast Address**: For the same subnet, the broadcast address is `192.168.1.255`.
2. Why do we need MAC address if we have IP address?
	-  IP is for Network Layer. Used for routing packets accross different networks. Logical addressing, can be changed or reassigned depending on which network it is connected to.
	- MAC is for Link Layer. Used for communication within a single network segment/local network. Unique ID for each hardware, remains constant.
	- **IP Address:**
	    - When data needs to travel across the internet, it is directed by IP addresses. Routers use these IP addresses to determine the best path for the data to reach its destination.
	- **MAC Address:**
	    - Once the data reaches the final local network (e.g., your home network), the MAC address is used to deliver the data to the correct device. For instance, your router will use the MAC address to deliver data to your laptop instead of your smartphone.
3. In IP subnetting, not only are the first and last subnets unusable, but within each subnet, the first and last addresses are also unusable? => depends on questions, but we assume so
4. 

