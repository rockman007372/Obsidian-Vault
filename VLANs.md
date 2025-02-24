LAN/Subnet:
- Devices within LAN connected to a network of switches to each other
- LANs connect to each other through a network of Routers

VLAN:
- Device can connect to the same virtual network without being in the same physical network
	- Devices in the same VLAN can communicate directly with each other using Layer 2 (Data Link Layer) switching.
- Segment different virtual networks within a single physical network
	- Each VLAN acts as a separate broadcast domain, isolating traffic between VLANs to improve security, reduce congestion, and better organize the network.

![[Pasted image 20240911122529.png]]

>[!note]
> 1. Device in the same VLAN must have the same subnet id!
> 2. Devices in different VLAN need a router to communicate despite being connected to the same physical switch network

"Router on the stick" view of VLAN:

![[Pasted image 20240911123031.png]]

A trunk connects one switch to another. This allows device in the same VLAN to communicate through a network of switches.

## VLAN table

- Table maintains a mapping `<VLAN id, Switch interface/port>`

## Frame Tagging

- Places a unique id in the header of each frame as it is forwarded thoughout the network backbone
- VLAN traffic between switches is tagged (**802.1q**) to identify VLAN membership

![[Pasted image 20240911123544.png]]

- First switch (Ingress) adds tag and last switch (Egress) removes tags 
- Intermediate switches do not recompute VLAN id, use this info to route packets to relevant VLANs?

## VLAN implementation

- Created by software running on Layer 2 switches.
- 2 methods to implement:
	1.  **Static: Port-based**
		- Assign physical ports on the switch to VLAN
		- Use VLAN Management Software or CLI to manually configure switches
	2. **Dynamic VLAN**
		- MAC-based (most popular)
			- MAC determines which VLAN it is in
			- Whenever a device connects to a port of a switch, the switch assigns the port with the right VLAN based on the device's MAC address.
		- Layer-3 Based
			- VLAN membership is determined by Protocol Type Field (IP vs IPv6) and IP subnet field in Layer-3 (Network layer) packets
## Switch ports

A **switch port** is a physical or logical interface on a network switch where devices, such as computers, servers, printers, or other networking devices, can connect to the network

Port Types:
- **Access Ports**: Connects end devices to the switch and is assigned to a single VLAN. It carries traffic for one VLAN only.
- ! **Trunk Ports**: Used to connect switches to each other or to other network devices like routers. Trunk ports carry traffic for multiple VLANs using tagging protocols like IEEE 802.1Q.
- **Hybrid Ports**: Can function as both access and trunk ports, handling multiple VLANs with specific configurations.

## Dynamic VLAN (MAC-based)

- Switch ports can automatically determine a user’s VLAN assignment based on MAC / physical address
- When a new device is connected to a port, the switch dynamically configures the port with the right VLAN
	- As a device enters the network, the switch that it is connected to queries (using, VLAN Query Protocol) a database on the VLAN Configuration Server for VLAN membership.
- Dynamic VLAN memberships (a table mapping MAC to VLAN) are created through VLAN management software (VMS) or manually using the CLI

## Dynamic VLAN (layer-3-based)

- VLAN membership is based on Layer 3 information, this has nothing to do with network routing and should not be confused with router functions. 
- IP addresses are used only as a mapping to determine membership in VLAN's. No other processing of IP addresses is done.

## Managing VLANS Network Wide

VLAN Trunking Protocol (VTP):
- Layer 2 client/server messaging protocol
- maintains VLAN config consistency within a VTP domain
	- VTP allows you to create, modify, and delete VLANs centrally on a **VTP centralized server switch**, and these changes are automatically propagated to other switches in the VTP domain.

VTP domain:
- All the routers/switches that are interconnected with trunks and share the same VTP domain name

Switches can be in 3 modes:
- VTP **server**: configure VLANs for the entire domain, advertise VTP configs to other switches and sync based on advertisements received over trunk links
- VTP **client**: cannot configure
- VTP **transparent**: do not participate in VTP, only forward VTP advertisements

## Switches Architecture

Traditional 3-tier architecture vs 2-tier Leaf-spine architecture