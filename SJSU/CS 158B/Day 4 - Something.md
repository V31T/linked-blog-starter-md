
![[Pasted image 20240909193522.png]]
![[Pasted image 20240909193551.png]]
## SNMP Messages
- **GET-REQUEST**: Manager requests the value of a Managed Object 
- **GET-NEXT-REQUEST**: Manager requests the value of the next Managed Object
- **GET-BULK**: Manger requests large data
- **SET-Request**: Manager requests to update the value of one or more Managed Object
- **GET-RESPONSE**: Agent responds to the above requests
- **TRAP**: Agent notifies voluntarily manager about a Managed Object

## SNMP and TCP/IP stack
- SNMP is an application-level protocol
- "" uses UDP
- "" Agents listen to port 161 for requests from Manager
- "" Managers listen to port 162 for traps from Agent
- Weakness: there are no confirmation of messages

## Choice of UDP
- the use of UDP does raise a problem: **lost packets**
- For the simplest case of manager-initiated data requests, a manage cna handle packet loss **by polling a device until a response is received.**
- another consequence of the use of UDP is that every SNMP device needs an IP address
	- For devices acting at the IP layer and above, this is not an issue, but an Ethernet switch or hub has no need of an IP address for its basic function.
	- Devices like switches and hubs that are to use SNMP must be provided with a suitable IP interface and address

## SNMP Traps
- SNMP Traps are voluntary alert messages sent from a remote SNMP-enabled device to a central collector,, the SNMP Manager
- A trap might tell you that a device is overheating etc.
- They are used to inform an SNMP manager when an important or unusual event happens at the Agent level
- A abenefit

## ASN.1
- Abstract Syntax Notation One
- A formal language developed by CCITT and ISO
- Used to define the format of SNMP messages and managed objects (MIB modules) using an unambiguous data description format

## OID
- How to name each device attribute in a consistent manner?
- SNMP approach: **Object identifier, or OID, hierarchy**
- ITU-T developed the OID Scheme for naming anything in the world that need naming
- Names, or OIDs, consist of strings of non-negative integers
- In textual representation, these component integers are often written seperated by periods, i.e. 1.3.6.1
- the root is anonymous. Sometimes a leading dot is added to emphasize this. i.e. .1.3.6.1
- There is no intrinsic way to distinguish between internal OID nodes and leaf OID nodes. Context is essential here.

## MIB 
- resources in the network may be managed by representing these resources as **objects**
	- trying to represent resources as objects (OOP)
- each object is, essentially, a data variable that represents one aspect of the **managed object**
- The collection of objects is referred to as **Management Information Base (MIB)**
	- A schema, displays how objects are *connected to each other*
- A Management Station performs the monitoring function by retrieving the value of MIB objects
- A management Station can cause an action to take place at an agent or can change the configuration settings at an agent by modifying the value of specific variables
- defined in ASN.1syntax

- A set of definitions that associate OIDs with specific attributes
	- associates each numeric level of OIDs with a symbolic name
- Interoperability
	- object that represents a particular resource should by the same across various systems
- Common representation Format
	- SMI (Structure of management Information)
- MIB is not the actual attributes themselves
	- the set of all (OID, value) pairs is known as management database or MDB
		- think **key-value pairs** where the *OID* is the key

## SMI
- Structure of Management Information
- Identify the data type that can be used in MIB
- How resources are represented and named, including
	- MIB structure
	- Syntax and value of each object
	- Encoding of object value

## MIB EXAMPLE
![[Pasted image 20240909200000.png]]
- **NOTE**
	- the OBJECT IDENTIFIER (OID) of the internet node is .1.3.6.1 *notice how this corelates with the middle branch*
	- **REMEMBER** ONLY LEAF NODES are actually worked on, the above diagram does not actually contain any leaf nodes
![[Pasted image 20240909200323.png]]
- `::=` is SMI syntax, read as "is"
- so the first point is read as "internet's object identifier is iso 3 6 1 -> (.1.3.6.1)"

![[Pasted image 20240909200702.png]]
- **NOTES**
	- the .0 represents that it is an object of the class
	- So basically classes and their classIds are represented by some numbers and everything after that number are objects of that class

## MIB-2
- MIB-2 is defined in RFC 1213 (March 1991)
- get form slide

## cont 
![[Pasted image 20240909201211.png]]

## SNMPv1 Data Types
![[Pasted image 20240909201307.png]]
- INTEGER
- OCTET STRING
- Counter - can **ONLY** increase
- Gauge - can increase **AND** decrease
- TimeTicks - measured in centiseconds
- OBJECT IDENTIFIER
- IpAddress - an OCTET STRING of fixed length 4
- NetworkAddress
- Opaque - any other data usually represented as an OCTET STRING

## SNMP Object Syntax
```
objname OBJECT-TYPE
	SYNTAX type
	ACCESS read-write or read-only or write only
	etcetc
```

## MIB Object Example: Counter

```
ifInUcastPkts OBJECT-TYPE
	SYNTAX  Counter
	ACCESS  read-only
	STATUS  mandatory
	DESCRIPTION
			"The number of subnetwork-unicast packets delivered to a higher-layer protocol."
	::= { ifEntry 11 }
```
- the last part means this is the 11th child of the class
## MIB Object Example: Gauge and IP Address TimeTicks
get the GAUGE example from the slides
![[Pasted image 20240909201827.png]]![[Pasted image 20240909201846.png]]


## MIB-ll system group
![[Pasted image 20240909202009.png]]


## NOTE
- For scalar objects, we need a ".0" at the end to refer to the "instance" of the object
	- **remember** we are taking about the class id with a .0 at the end
	- without the .0 you are just referring to the class

![[Pasted image 20240909202455.png]]
- net-snmp for unix
- iReasoning for windows

![[Pasted image 20240909202552.png]]
 ![[Pasted image 20240909202719.png]]
 ![[Pasted image 20240909202855.png]]
- ALOT OF DEVICES USE MIB 2 so windows or unix it shouldnt really matter