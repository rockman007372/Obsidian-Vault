---
tags:
  - toProcess
course: CS3103
type: lecture
date: 2024-08-28 Wednesday
---

## ARP

ARP (Address Resolution Protocol):
- map IP address to a physical MAC address in a local area network
- used for devices on a network to communicate with each other using Ethernet or other network tech
- example:
	- device A wants to communicate with B on the same local network. A needs to know B's MAC addr, associated with B's IP
	- A broadcasts an ARP request packet to local network, asking whoever has B's IP address to send its MAC address
	- Only B will respond with an ARP reply packet back to A, allowing A to update its ARP table (cache mapping of IP to MAC address)
	- A sends info directly to B using its MAC address.

ARP Request and Reply headers:
- Hardware type (2 bytes): ethernet or wireless lan
- Protocol type (2 bytes): IPv4, IPv6
- Hardware address length (1 byte)
- Protocol address length (1 byte)
- Operation code (2 bytes)

In ARP request packet, the target hardware address is 0x0

Proxy ARP:
- A router/host that allow 2 devices on 2 different subnet to communicate
- The proxy will responds to ARP request with its own MAC address. It will route the incoming packets based on destination IP.

ARP request made to non-existent host: requests made with increasing time intervals until giving up

A host can send ARP requests to all addresses inside ARP cache to refresh content ⇒ introduce traffic

**Gratuitous** ARP requests: host sends ARP requests for its own IP addr
- detect if an IP address has been assigned
- update ARP caches of other devices in the network abt its IP-MAC mapping

ARP vulnerability:
- ARD does not authenticate ARP requests and replies
- stateless ⇒ ARP replies can be sent w/out a corresponding request
- a node receiving ARP packet (both request and reply) MUST update its local ARP cache if the receiving node alr has an entry for the IP address of the source.

ARP Spoofing (ARP Poisoning):
- Vulnerability: stateless, no authentication ⇒ any device on the network can respond to an arp request with a fake MAC address
- Exploit: attacker sends falisified ARP messages onto the network to associate their MAC adddress with the IP address of a popular device (default gateway to the internet for eg).

Dynamic ARP Inspection:
- Switches check ARP packets against trusted dbase before allowing them to pass (switches are invisible to device on the network)
- Ports that connect to end-user devices (like computers or IP phones) are considered untrusted. ARP packets from these ports are inspected by DAI to verify their legitimacy.
- **Binding Table**: DAI uses a database called the DHCP Snooping Binding Table (or ARP inspection table) to verify ARP packets. The table is usually populated by DHCP snooping, which records the IP-MAC mappings as devices obtain IP addresses from the DHCP server.
	- When an ARP packet is received on an untrusted port, DAI checks the IP and MAC address in the ARP packet against the entries in the binding table.

Neighbor Discovery Protocol (NDP) in IPv6:
- Allow for multicasting: only devices interested in receiving a multicast packet will receive

Software-defined network:
- network architecture that separates control plane (makes decision abt where traffic is sent) from the data plane (actually forward traffic to selected destination)
- traditionally, both planes are integrated in networking devices (routers and switches) ⇒ decoupling allows more programmable network management
- The controller is the brain of the SDN. It serves as a centralized management entity that dictates how the network behaves by controlling the flow of data. 
- Traditionally, ARP is decentralized (each device maintaining its own ARP cache and resolving IP-to-MAC address mappings independently). 
	- In SDN environment, ARP can be centralized, managed by the SDN controller ⇒ SDN controller can validate all ARP requests and responses for legitimate mappings.

ARP is encapsulated inside an Ethernet frame ⇒ ARP is level 2 protocol, part of payload for Ethernet frame.

## Dynamic Host Config Protocol (DHCP)

DHCP allows allocation of IP from a pool through:
- static config (indefinite time)
- automatic config (indefinite time)
- dynamic config (for specific duration)
	- DHCP server loans IP addr for a limited time
- DHCP is an Application Layer protocol, ride on UDP
- Server waits on UPD port 67, client communicates on UDP port 68

### How It Works:

- **Step 1: DHCPDISCOVER**:
    - The client (which doesn't yet have an IP address) sends a broadcast message called a **DHCPDISCOVER** from UDP port 68, targeting UDP port 67, to discover available DHCP servers on the network.
    - There may be multiple DHCP servers on the network
    - Servers will retrieve an available IP addr from dbase and **PING** it in local network to validate availability
- **Step 2: DHCPOFFER**:
    - A DHCP server that receives the **DHCPDISCOVER** responds with a **DHCPOFFER** message. The server sends this message from UDP port 67 to UDP port 68, offering an IP address and other configuration settings (length of leases....) to the client.
- **Step 3: DHCPREQUEST**:
    - The client receives the **DHCPOFFER** and, if it wants to accept the offered IP address, sends a **DHCPREQUEST** message back to the server, again using UDP port 68 to UDP port 67.
	- DHCPREQUEST is broadcasted to all DHCP servers, even for servers whose offer was not requested ⇒ know which IP is available
	- Can also use DHCPREQUEST to renew lease
- **Step 4: DHCPACK**:
    - The server acknowledges the request by sending a **DHCPACK** message from UDP port 67 to UDP port 68, confirming the IP address assignment and any additional network settings.
    - Client then send 3 ARP probles and 1 Accouncement ARP for its new IP ⇒ gratuious ARP requests

DHCP relay agent:
- a router that knows the IP address of DHCP server
- request is broadcasted til it reaches DHCP relay agent, where the request is unicast to DHCP servers only
- DHCP servers recognize request is coming from Router and not client => send unicast reply to router instead of broadcasting

> There are some info on DHCP packets in the slides!

DHCP Snooping:
- prevent rogue DHCP servers from assigning IP
- Just monitor the DHCP packets 



## Summary

## Questions/Cues

1. In a ARP protocol, how does device A know IP of device B?
	1. Netword admin? know beforehand

2. Who assign IP address to a device connecting to a network?
- In a network, your computer's IP address is typically assigned by one of the following methods:
	 1. **Dynamic IP Address Assignment (DHCP)**:
		- **DHCP Server**: The most common method for assigning IP addresses in a network is through a **Dynamic Host Configuration Protocol (DHCP)** server. When a device connects to the network, it sends a request to the DHCP server.
		- **DHCP Process**: The DHCP server assigns an available IP address from a predefined range (called a DHCP pool) to the device, along with other necessary network configuration details like the subnet mask, default gateway, and DNS servers.
		- **Lease Time**: The IP address is usually leased for a specific period. When the lease expires, the DHCP server may assign the same or a different IP address to the device.
	2. **Static IP Address Assignment**:
		- **Manual Configuration**: In some cases, especially in enterprise networks or for servers, IP addresses are assigned manually by a network administrator. This is known as static IP addressing.
		- **Permanent IP**: The IP address remains constant unless manually changed by the administrator. This is often used for devices that need a consistent address, like servers, printers, or network devices.

3. How does DHCP relay agent know the IP of source if source is not assigned an IP yet?
	1. they just broadcast to the network

