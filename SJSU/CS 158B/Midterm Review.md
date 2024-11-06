## Lecture 1

Switching: the process of directing data packets between devices on the same network. Each host must have a unique MAC address and IP address. Operates at Layer-2/MAC layer/Link Layer. Maintains a "learning table" -> maps MAC addresses to the switch's physical ports; switch learns which MAC address is associated with each port and updates this table dynamically: every incoming frame ON INSERT associates the source MAC address with the ingress port and LOOKUP the destination MAC address in the table -> if found forward the frame to the port, if not found forward the frame to ALL ports(flooding), old entries are aged/purged out. TABLE OPERATIONS -> Human driven: ADD, CLEAR, DISPLAY `or` Software driven/automatic: Source Learning (add newly learned MAC address entry), Destination Lookup, Age out old entries

## Lecture 2

Routing: the process of fowarding packets between different subnetworks or **[V]LANs**. Uses **Routing Tables** to determine the best path for packets based on the destination IP address. 
ARP (address Resolution protocol): ARP is used to map IP address to a MAC address, allowing communication between devices within the same local network
Subnetwork and Classful Addressing: Subnetworks are smaller parts of a larger network, typically corresponding to LANs or VLANs. IPv4 addresses used to be organized into classes (A, B, C), but modern networks use CIDR (Classless Inter-Domain Routing) for more flexible subnetting. 
Router's role: A router forwards packets between subnetworks or VLANs, while switches forward frames within a single subnetwork.
Routing Table: contains entries for destination subnetworks, next hop IP addresses, and egress interfaces. it determines the best route based on the **Longest Prefix** method.
Planes of Operation: Data Plane: Handles packet forwarding at the hardware level. Control Plane: Manages routing information through protocols like RIP, OSPF, and BGP. It stores routing information in the **Routing Information BASE (RIB)** and selects the best route for the **Forwarding Information Base (FIB)**
VRF (Virtual Routing and Forwarding): allows multiple virtual routing instances to coexist on the same physical router, supporting logical network segmentation.
- **ARP**: Protocol that resolves IP addresses into MAC addresses.
- **CIDR**: A method for flexible IP address allocation using variable-length subnet masks.
- **Routing Table**: A table in a router that lists possible routes and the next hop for packets.
- **Longest Prefix Match (LPM)**: The method a router uses to select the most specific route for forwarding a packet.
- **Data Plane**: The part of the router responsible for forwarding packets.
- **Control Plane**: Manages routing information via protocols and determines the best path.
- **Management Plane**: Handles configuration and administration of the router.
- **VRF**: Virtual Routing and Forwarding, used for creating multiple isolated routing tables on a single router.
#### What is Routing?

Routing is the process of forwarding packets from one subnetwork to another, typically using a router. Routers make routing decisions based on a **routing table**, which contains information about the possible routes to various destination networks. The key function of routing is to ensure packets take the optimal path to their destination, often using protocols like **OSPF** or **BGP** to communicate with other routers and learn about available routes. Routing typically occurs at the **Network Layer (Layer 3)** of the OSI model.

## Lecture 4

Network Architectures: different types of entworks include **Campus Networks, Data Center Networks, Service Provider Networks, and Cloud Networks.** Each serves different purposes based on size, scalability, and the services they support.
FCAPS Model: a widely adopted Network management framework used to manage networks efficiently. **Fault Management**: detecting, isolation, and correcting abnormal operations. Configuration Management: Configure devices to ensure intended behavior. Accounting Management: Gathering data on network usage, often related to statistics and telemetry. Performance Management: Monitoring and ensuring that network performance is within acceptable levels (throughput, latency, etc.). Security Management: Keeping the network secure, managing access, and handling encryption keys.
Network management Systems (NMS): a system that integrates tools for monitoring and configuring network devices. NMS provides a single interface for managing network operations and typically includes both hardware and software components.
Network Management entity (NME): Devices (i.e routers, switches) include software devoted to network management. NMEs collect statistics, store data, and respond to commands from the Network Control Center (NCC).
Performance Monitoring: Focuses on key indicators such as availability, response time, throughput, and utilization. Performance Monitoring ensures that the network is functioning efficiently and identifies bottlenecks.
Polling and Event Reporting: Polling: a request-response interaction where the manager periodically retrieves data from the agent. Event Reporting: the agent sends data to the manager based on specific conditions, such as periodic updates or significant network events.
- **Campus Network**: A network infrastructure spread across multiple buildings, typically within a single organization like a university or corporation.
- **Data Center Network**: The network architecture within a data center that supports servers, storage, and networking devices.
- **Service Provider Network**: A large-scale network operated by telecom or internet service providers, typically spanning multiple regions or countries.
- **Cloud Network**: A network architecture that enables cloud-based services, allowing for scalable and flexible resource allocation.
- **FCAPS Model**: A network management framework comprising:
    - **Fault Management**: Detecting and addressing network failures.
    - **Configuration Management**: Ensuring devices are set up correctly.
    - **Accounting Management**: Gathering and analyzing data from network devices.
    - **Performance Management**: Monitoring and maintaining network performance.
    - **Security Management**: Managing access control and security measures.
- **Network Management System (NMS)**: An integrated toolset for configuring and monitoring network devices through a unified interface.
- **Network Management Entity (NME)**: A component within network devices responsible for collecting statistics, storing data, and communicating with the Network Control Center.
- **Polling**: A method of network monitoring where the manager requests data from the agent at regular intervals.
- **Event Reporting**: A network monitoring method where the agent automatically sends updates or alerts to the manager based on certain triggers, such as a fault or a state change.
- **Service Level Agreement (SLA)**: A contract defining the expected uptime or availability of a service, typically expressed as a percentage.
- **Throughput**: The amount of data successfully transmitted through the network per unit of time.
- **Utilization**: The percentage of the total capacity of a network resource that is being used.
- **Availability**: The percentage of time a network or application is operational and accessible to users
### Problems and Solutions:

1. **Problem 1**: **Maximum Yearly Downtime for a 99.9% SLA (Service Level Agreement)**:
    - An SLA of 99.9% uptime means the network is allowed 0.1% downtime annually.
    - **Solution**: To calculate the maximum allowed downtime:
        - 99.9% uptime corresponds to 0.1% downtime.
        - In a year (365 days), 0.1% downtime is approximately 8.76 hours per year.
	- **FCAPS MODEL**: this problem highlights aspects of Fault Management and Performance Management. For instance, calculating downtime for a 99.99% SLA relates to ensuring network availability under Performance Management. The probability of failure in a computer cluster emphasizes the need for Fault Management to handle potential issues, especially in large networks.
1. **Problem 2**: **Probability of Failure in a Cluster of Computers**:
    - In a cluster of 100 computers, each with a 0.1% chance of failure, the goal is to calculate the probability that at least one failure occurs.
    - **Solution**: Use probability principles:
        - The probability of no failure = (1−0.001)100≈0.905(1 - 0.001)^{100} \approx 0.905(1−0.001)100≈0.905.
        - The probability of at least one failure = 1−0.905=9.5%1 - 0.905 = 9.5\%1−0.905=9.5%.
        - For larger clusters (e.g., 1000 computers), the probability of at least one failure increases to 63%.
    - NMS and NME: These concepts tie directly in the solutions by showing how devices and management systems must work together to minimize downtime and ensure quick responses to faults. For example, NMS would monitor uptime and alert network administrators if failures occur in cluster, supporting quick isolation and correction. 

## Lecture 5

SNMP (Simple Network Management Protocol): a protocol used for exchanging network management information between devices. facilitates network configuration, fault detection, and accounting by defining a common framework for communication between managers (who collect and analyze data) and agents (network devices being monitored). It is a vendor-neutral and works across various product types like routers, switches, and hosts.
SNMP Ecosystem: Composed of a SNMP Manager (Controls the network) and SNMP Agents (devices like routers, switches, and hubs). Management Information Base(MIB): A structured collection of objects that can be managed and monitored. 
SNMP Messages:  **GET-REQUEST**: The manager requests the value of a managed object. **GET-NEXT-REQUEST**: Retrieves the next managed object. **GET-BULK**: Requests large amounts of data. **SET-REQUEST**: The manager sets or updates values in the agent. **GET-RESPONSE**: The agent responds to the manager's requests. **TRAP**: The agent voluntarily informs the manager of important events or changes.
SNMP and TCP/IP Stack: SNMP operates as an application-level protocol over UDP. Agents listen on port 161 for requests, and managers listen on port 162 for traps.
ASN. 1 (Abstract Syntax Notation One): a formal language used to define the format of SNMP messages and managed objects. This ensures standarized, unambigious communication across network devices.
OID (Object Identifier): a hierarchical naming scheme developed by ITU-T for naming managed objects in a consistent manner across devices.
MIB (Management Information Base): a database that represents network resources as objects, organized hierarchically. Objects are identified by OID. MIB defines what data can be monitored and managed by the SNMP manager.
SMI (Structure of Management Information): Defines the syntax, structure, and encoding for managed objects in MIB. Specifies the data types used for each object in MIB. 
MIB-II: An extension of the original MIB structure, defined in RFC 1213. Includes various system, network, and protocol-related data (like IP, ICMP, TCP, UDP)
- **SNMP (Simple Network Management Protocol)**: A protocol used for managing and monitoring network devices.
- **Manager**: The component responsible for managing devices (collecting data, setting configurations).
- **Agent**: The device being monitored (e.g., router, switch) that sends data to the manager.
- **MIB (Management Information Base)**: A database structure that organizes network management objects, accessible via SNMP.
- **OID (Object Identifier)**: A hierarchical identifier used to uniquely name objects within the MIB.
- **ASN.1 (Abstract Syntax Notation One)**: The language used to define SNMP messages and managed objects.
- **TRAP**: An alert message sent from an agent to a manager, often indicating an event or change.
- **SMI (Structure of Management Information)**: Defines how objects are structured and encoded within MIB.

## Lecture 6
SNMP Composite Types: Record/Struct Type: `SEQUENCE {fieldname1 type1, fieldname2 typ2, ... }`. Array Type: `SEQUENCE OF type` where type is an object. Table: `SEQUENCE OF type` where type is a SEQUENCE. A Sequence is a collection of ordered elements, similar to a record or struct in programming: used to represent complex objects in SNMP.
SNMP TABLE: Access via Primary Key Lookup or Linear Search. Key can be a single attribute or a set of attributes (index). An SNMP table index acts as a *constraint*, disallowing two distinct rows with identical index values (only 1 row per unique index value).
	- SNMP follows Column Major
	- so the correct way is `x = fooTable[4][2]`
Columnar Objects: 2 techniques to identify: Random access technique & Serial-access technique. Each columnar object has a unique object identifier that is the same in each row.
ifTable example: a specific component within MIB-ll that contains info about interfaces on a network device.  each interface has an abstractly assigned interface number, known as ifIndex. each a single integer. (NOTE: 'if' stands for InterFace).
- question: what is the interface type (ifType) of the 2nd interface? OID of ifType = 1.3.6.1.2.1.2.2.1.3 : ifIndex = 2 (because 2nd interface) : iftype instance Identifier = 1.3.6.1.2.1.2.2.1.3.**2** 
tcpConnTable: 2d table w/ scalar-valued entries
![[Pasted image 20240925150549.png]]
:3 instances of tcpConnState, but all have the same OID. values of the INDEX object of a table are used to distinguish one row from another. Combination of OID and one set of values of the INDEX objects specifies a particular scalar object in a particular row of the table. to combine, SNMP uses concatenation.
![[Pasted image 20240925151057.png]]
- understand how the top correlates to the bottom -> just concat the row to get the instance identifier.
Table Definition and Structure: An OID prefix represents the table. Index attributes are used to uniquely identify each row/ column OIDs are created by appending integers to the table's OID prefix. The combination/concatenation of column OIDs and index values gives unique identifiers for each data point in the table
Limitations of SNMP Protocol: cannot add or delete objects dynamically, can only GET and SET
Demo part/notes: `snmpget` to interact with SNMP tables and `snmptable` to view contents
- **SNMP (Simple Network Management Protocol):** A protocol used for monitoring and managing network devices by collecting and organizing information and enabling remote control.
- **MIB (Management Information Base):** A database that stores and organizes information about managed objects within a network, defining their properties and relationships.
- **MIB-II:** An extended version of the original MIB defined in RFC 1213, providing standardized objects for managing network elements like interfaces, IP, ICMP, TCP, and UDP.
- **OID (Object Identifier):** A unique identifier used to name and locate objects in the MIB, represented as a hierarchical sequence of numbers.
- **Scalar Object:** A single-instance object in the MIB that represents a single value, such as the maximum number of TCP connections.
- **Composite Object:** An SNMP object that consists of multiple fields or elements, defined using SEQUENCE types like arrays or records.
- **SEQUENCE:** A construct in ASN.1 (Abstract Syntax Notation One) used to define structured records or lists of elements in SNMP objects.
- **SNMP Table:** A structure in the MIB consisting of multiple rows and columns, similar to a database table, where each row represents an instance and each column represents a specific attribute.
- **Index:** An attribute or set of attributes used to uniquely identify a row in an SNMP table, such as `ifIndex` in the `ifTable`.
- **Columnar Object:** A type of object in SNMP tables representing multiple instances of a variable across different rows, identified by a combination of the column OID and the index value.
- **ifTable:** A table in MIB-II providing information about network interfaces on a device, including attributes like `ifIndex`, `ifType`, and `ifSpeed`.
- **ipRouteTable:** A table in MIB-II containing information about the IP routing table, such as destination, next hop, and route metrics.
- **tcpConnTable:** A table that provides information about active TCP connections, with columns like `tcpConnLocalAddress`, `tcpConnLocalPort`, `tcpConnRemAddress`, and `tcpConnRemPort`.
- **GET Operation:** An SNMP operation used to retrieve the value of a specific object from an SNMP agent.
- **SET Operation:** An SNMP operation used to modify the value of a specific object on an SNMP agent, provided the permissions allow it.
- **SNMP Agent:** A software component running on a network device that maintains the MIB and responds to SNMP queries from an SNMP manager.
- **SNMP Manager:** A system or software application that communicates with SNMP agents to monitor and manage network devices.
- **RFC (Request for Comments):** A formal document from the Internet Engineering Task Force (IETF) describing standards, protocols, procedures, and guidelines for the Internet, such as RFC 1213 for MIB-II.

## Lecture 7

Manager-Agent Relationship: SNMP Manager: system or software application that sends requests to and receives responses from SNMP agents to monitor and manage devices. SNMP Agent: software that responds to requests from the manager, controlling access to its local MIB. relationship can be 1:M or M:M agent can b managed by multiple managers and manager can control multiple agents.
Agent Perspective and Control: Authentication Service: agent can restrict access to its MIB to authenticated managers, preventing unauthorized access. Access Policy: the agent can grant different access privileges to different mangers (read-only, read-write). Proxy Service: An agent can act on behalf of another agent, implementing authentication and access policies for the proxied agents.
Security Via Community: Community: defines a relationship between an SNMP agent and a set of managers. it controls authentication, access control, and proxy characteristics. Agents can have multiple communities each with specific access controls and privileges for different managers. Community names act as passwords, and knowing the community name allows access. 
Access Policy and Community Profile: MIB View: limtits access to a subset of MIB objects. Different communities can have different MIB views, restricting which objects are accessible. Access Mode: defines whether the community can read or write to the objects. The access mode can be read-only or read-write. Community Profile: a combination of MIB view and access mode, defining the specific rights of a community, forms the SNMP Access Policy. 
Instance Identification: each MIB object is identified by OID, though OID is sometimes not enough -> use additional identifiers like index values in a table 
GetNextRequest and Sequential Access: GetNextRequest: An SNMP operation that retrieves the next object in the lexicographical order of OIDS. usefule for when then the manager does not know the exact OID of the desired object. Sequential Access: Managers can use a series of `GetNextRequest` operations to traver an entire MIB subtree, retrieving each object in order.
GetNextRequest Motivation and Use Cases: `GEtNextRequest` is useful for iterating over objects in a MIB, especially when some objects may not be supported by the agent. It allows the manager to retrieve the next valuable object, improving efficieny.
GETBULK Operation: a more advanced operation than `getNextRequest`, `GETBULK` allows the retrieval of multiple objects in a single request, reducing the number of exchanges needed to get an entire table or subtree.
- **SNMP Manager:** The system or application that sends requests to SNMP agents to monitor and manage network devices.
- **SNMP Agent:** The software running on a network device that maintains the MIB and responds to requests from the SNMP manager.
- **MIB (Management Information Base):** A hierarchical database that defines the properties and relationships of manageable network objects.
- **OID (Object Identifier):** A unique identifier used to name and locate objects in the MIB, represented as a hierarchical sequence of numbers.
- **Community:** A relationship between an SNMP agent and a set of managers, defining authentication, access control, and proxy characteristics.
- **Authentication Service:** A service provided by the SNMP agent to restrict access to its MIB to authenticated managers.
- **Access Policy:** Rules defined by the SNMP agent that determine what access privileges each manager has to the MIB objects.
- **MIB View:** A subset of the MIB accessible to a specific community. Different communities can have different MIB views.
- **Access Mode:** Defines the level of access (read-only, read-write) a community has to the MIB objects.
- **Community Profile:** A combination of MIB view and access mode, defining the specific access rights of a community to the MIB objects.
- **Instance Identification:** The process of uniquely identifying each instance of a MIB object, particularly in tables, using OIDs and index values.
- **GetNextRequest:** An SNMP operation that retrieves the next object in the lexicographical order of OIDs, useful for traversing a MIB tree.
- **GETBULK:** An SNMP operation that retrieves multiple objects in a single request, used to efficiently access large amounts of data.
- **Proxy Service:** An agent acting on behalf of another agent, implementing authentication and access policies for proxied systems.

## Lecture 8

Message Formats: SNMP Message Components: each SNMP message contains the SNMP version, community name for authentication, and a PDU (Protocol Data Unit). PDU Types:: GetRequest - Retrieves the value  of specified objects : GetNextRequest - retrieves t he the next object in lexicographical order : SetRequest: Updates the value of specified objects : GetResponse: The agent's response to a manager's request : Trap - an unsolicited message from the agent to the manager, indicating an event such as a device reboot.
PDU Timing Diagrams and Formats: PDU Timing: illustrates the sequence and timing of PDU's exchanged between SNMP managers and agents. PDU Fields: each PDU has specific fields like request ID, error status, error index, and variable bindings. 
ASN.1 PDU Definitions: Abstract Syntax Notation One (ASN.1): a standarized way to define data structures for SNMP PDU's, ensuring consistent interpretation of messages between different devices and systems. 
Variable Bindings: Multiple Object Bundling: Multiple MIB objects can be bundled into a single SNMP message. This reduces communication overhead as a manager can request or an agent can respond with multiple objects at once.
GetRequest: Request ID: a unique identifier for each outstanding request sent to the same agent, allowing the manager to track responses. Atomic Operations: the operation is atomic, meaning either all requested values are retrieved or none are. i.e. retrieving multiple attributes such as `ipRouteDest`, `ipRouteMetric1`, and `ipRouteNextHop` in one request.
Multi-Attribute GET and GETNEXT: Efficiency in Data Retrieval: a manager can request entire rows of a table by specifying multiple column OIDs. This approach speeds up the table-retrieval process, especially when the manager knows the column OIDs but not all index values. Sequential Retrieval: A series of `GetNext` operations can be used to retrieve each row of a table in a sequence.
SetRequest: Atomic Update: The `SetRequest` operation is atomic, ensuring that all updates are applied or none are. Table Updates: updating a non-index cell : adding a row - a new row with multiple attributes in one operation : Deleting a row: setting a cell's value to `invalid` to indicate a deletion.
Performing an Action: Reboot example: using a `SetRequest` to set a specific object val;ue that triggers a device action, such as rebooting a device by setting a particular object to 1.
- **SNMP Message:** A packet of data exchanged between an SNMP manager and agent containing version information, community name, and a PDU.
- **PDU (Protocol Data Unit):** The data unit used in SNMP communication, such as `GetRequest`, `GetNextRequest`, `SetRequest`, `GetResponse`, and `Trap`.
- **GetRequest:** A PDU type used by the manager to retrieve the value of one or more MIB objects.
- **GetNextRequest:** A PDU type used to retrieve the next object in the MIB hierarchy, useful for traversing tables.
- **SetRequest:** A PDU type used to set or update the value of one or more MIB objects on an agent.
- **GetResponse:** A PDU type sent by the agent in response to a `GetRequest` or `SetRequest`, containing the requested values or the status of the operation.
- **Trap:** A PDU type used by an agent to notify the manager of significant events or changes, such as a device reboot.
- **Variable Bindings:** A list of object-value pairs included in SNMP PDUs, allowing multiple objects to be queried or updated in a single message.
- **Atomic Operation:** An operation in SNMP that must be fully completed or not executed at all, ensuring data integrity.
- **ASN.1 (Abstract Syntax Notation One):** A standard notation for defining the structure of SNMP PDUs and data, ensuring compatibility across devices.
- **Table Retrieval:** The process of using SNMP operations like `GetNextRequest` to sequentially access rows and columns of data in MIB tables.
- **Multi-Attribute GET:** A method where multiple column OIDs are specified in a single `GetRequest` to retrieve several attributes of a table row at once.
- **PDU Timing Diagram:** A diagram that illustrates the sequence and timing of SNMP PDUs exchanged between a manager and agent during communication.
- **Reboot Action:** An example of using `SetRequest` to perform a specific action, like rebooting a device by setting an object value.