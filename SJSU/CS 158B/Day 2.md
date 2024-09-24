---
created: 2024-08-29 14:02
tags:
  - CS158B
  - SJSU
---
## Notes

### Switches:
![[Pasted image 20240924012930.png]]
- if there is a loop in the network, flooding will cause an infinite loop and packet will be passed around infinitely
	- use tree structure for multiple switch topology
- How does a frame get forwarded from A to C?
	- Switch floods packet form A to all connections 
	- Next switch also floods to all connections, which includes host C
- How does the frame get back to A from C?
	- All switches remember the destination of A, each switch has address table to route host to port, similar to routing tables 
- to communicate to switches, we need to know MAC address

### ARP
- **Address Resolution Protocol**
	- tells destination MAC address of corresponding destination IP address
	- Broadcasts to all hosts, responds in unicast with MAC address 
- ARP CACHE
	- STORES received MAC address for a short period of time
- MAPS IP address to MAC address
	- IP is environment/location dependent
	- MAC address is device dependent

### Layer Perspective
- Router only has link layer and network layer
- MAC address is level 2 address (internet layer). and IP address is level 3 address (transport layer)

### Subnetwork
- Each LAN or VLAN maps to a subnetwork
- All of them come together to make the full network
- less networks = more hosts per network, BUT more networks = less hosts per network (dependent on network bits and host bits)
	- Mask example: /8 -> 8 bits for network, 24 bits for hosts
- Broadcast -> send to all hosts
	- Example: news channel broadcasts to everyone
- Multicast -> sent to certain hosts
	- Example: subscription based sports channel requires setup for a multicast group
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXezwCaLg4XgjiQbEH22wR5IO4Wup3A9bdZb7njmH5gYKTiimLqGO7Po-avQWWWtwKv9tlAaEyPZDsEVuxy1AUDzYz5YfUIeJa-e0ZAgrUF7xR9Lr1oNrI9Ck87q-9vtgaY_XbSkOMwqDe0qq30fPhtPIi0?key=S0oeVR7u95PCI2BRcwSpAQ)

### CIDR
- Classless Inter-Domain Routing
- Allows any length mask
	- /n implies
		- n network bits
		- 32 - n host bits (128 - n for IPv6)

### Router's Job
- Multilayer switch
	- Does job of switch and router
- VLAN A host talks to VLAN B host through multilayer switch

### Routing Table
- Router maintains routing table
- Routing table consists of many entries of the following format
	- Destination subnetwork
	- Next hop IP address
	- Egress interface
	![[Pasted image 20240924013611.png]]
	- Routing table is specific to each router, and it tells you what IP to go to next in the path of getting to the destination IP
		- Router IP separate from the network (Router C IP (10.2.2.2/24) is different form the IP of the network(10.12.0.0/16))

### Longest Prefix Match
- if destination IP matches multiple entries, **choose the iP that has the most matching network bits**
![[Pasted image 20240924013829.png]]
- in this example: 192.168.82 is the destination IP of the packet, so now we want to find the IP that has the longest matching network address. In this case, 192.168.2.80/29 has the most matching network btis, so we should take the interface that leads in that direction/

### Three Planes of Work
- Data plane: forwarding IP datagrams
	- Usually in hardware
	- Usually at line rate
	- forward packets based on forwarding information base (FIB)
- Control Plane: information from other routers
	- Usually via routing protocols i.e. RIP, IS-IS. OSPF, BGP
	- receive information from other routers
	- received information from other routers
	- received info gathered in routing information base (RIB)
	- could be multiple options.routes to destination networks
	- best such route programmed in FIB
	- ![[Pasted image 20240924014328.png]]
- Management Plane: configuration of router
	- admin plane
	- usually CLI, API, or other higher level software

### VRF
- Virtual Routing and Forwarding
- Router can suppport multiple independent virtual routing and forwarding instances
- Logical segmentation between different networks onthe same routing platform
- As routing instances are independent, VRF allows overlapping subnets