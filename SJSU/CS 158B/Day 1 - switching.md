---
created: 2024-08-29 14:02
tags:
  - CS158B
  - SJSU
---
just normal student stuff ig

## POWERPOINT 2 NOTES

### what is switching?
- a **switch** connects few hosts
	- i.e. a switch connecting a few co-located hosts
	- a hardware ethernet switch can connect cabled devices like computers, servers, WiFi access points, PoE lighting, and IoT devices etc.
- Requires 2 assumptions
	- Each host has a unique MAC address
	- each host has a unique IP address

### Basics
- Switches operate at Layer-2 or MAC layer or Link layer
- i.e. it operates by based on the source and destination address in an Ethernet frame

### Cross-Layer Perspective
- the following diagram shows how the application data is encapsulated at different layers
- ![[Pasted image 20240924012444.png]]
![[Pasted image 20240924012456.png]]

### Transparent Learning
- A switch maintains a learning table.
	- Associative Map: address -> port
- For every incoming frame, 
	- \[Insert or Update]  Associates the source MAC address with the ingress port i.e. table[src-address] = port
	- [Lookup] Looks up the desination MAC address in the table
		- if found: forward the frame to that port
		- if not found: forward the frame to ALL the ports (i.e. flooding)
		- result = table.lookup(dst-address)
- Periodically, old entries are aged out (purged)

### MAC Address table Operations
- Human-driven
	- `ADD` a static MAC address entry
	- `CLEAR` MAC address(es) [with different filters]
- Software-driven or Automatic
	- Source learning: add a newly learned MAC address entry
	- Destination Lookup
	- Age out old entries