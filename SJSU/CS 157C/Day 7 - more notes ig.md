
## TODO you still need to catch up on last lecture notes u shit brain

### REVIEW
- Data distribution methods: sharding and replication
	- sharding puts different parts of the data onto different **nodes**
	- replication takes the same data nd copies it over multiple nodes
		- master-to-slave replication
		- peer-to-peer replication
	- you can use either or both of sharding and replication
- ^^ The above information relates to **consistency** problems

## Peer to peer replication
data can be accessed on any **server/node**
- ride over node failures without losing access to data
- easily adding nodes to improve performance
- complication - cosistency
	- concurrent writes update the same record (two replicas representing the same data) at the same time
- how to deal with write insonsistency
	- for a write request, the replicas coordinate to ensure to avoid a conflict at teh cost of netowrk traffic
	- cope with an inconsistent write, for example, by merging inconsistent writes

## replication methods for cassandra and mongodb
decision to make when system is developed.
- cassandra uses **peer-to-peer**
	- peer-to-peer improves availability over consistency
	- Whiteboard example: 
		- 4 nodes, each node contains the same data
		- if consistency level = 2
			- check only 2 nodes, synchronize/consildate data between the 2 nodes and then return the data
			- this is quiock because data only needs to be checked from 4 nodes
			- this is the same idea as isolation level in **RDBMS**
				- higher isolation level = stronger lock => higher latency
	- when it comes to writing data
		- note inplace write: find data and then write
			- bad for cassandra
		- cassandra adopts append-orientated-write
			- new writes are just appended to the data
			- examlpe: update 10 to 20 -> 20 is appended to 10
			- inconsistency is resolved by **read-repair**
	- READ-REPAIR
		- keywords: digest, summary, repair, synchronized
		- TODO: get these notes
	- another repair method: ANTI-ENTHROPY
		- maitenance operation done by cassandra that check **every** copy to repair them
		- ![[Pasted image 20240916105443.png]]
		- 
- mongodb uses **master-slave**
	- n/a

## Video Notes

2.
### Master-save replication + shariding
multiple masters but each data itme only has a single master
![[Pasted image 20240916105916.png]]
- the master serves as the primary copy

### peer-peer-replication (RF=3) + SHarding
- oof u didnt et the piture loser

### Update Consistency
Consistency as a term has multiple dif definition (CAP vs ACID)
- write-write conflict: two people updates the same data item at the same time
- without concurrency control, there may present a lost update
- ![[Pasted image 20240916110307.png]]
- How to maintain consistency? 
	- **Pessimistic approach**: preventing conflicts from occuring - e.g. using locks
	- **Optimistic**: lets conflicts occur, but detects them and takes action to sort them out. e.g. **conditional update** (a type of optimistic approach) or saving both updates and merge them somehow (DONT USE LOCKS, instead parallelism)
	- Trade-off of concurrency control: safety (avoinding conflicts) and liveness (responding quickly to clients)
		- **SAFETY VS LIVENESS**
			- how does this differe from consistency vs latency????
- Write replication, there present more write-write conflict.
	- master-salve replication < Peer-to-Peer replication

### Read Consistency
- Logical consistency: ENsuring different but logically related items make sense together 
- Logically inconsistent read-write conflict: P has done a read in the middle of M's write
- ![[Pasted image 20240916110859.png]]
	- IMPORTANT DIFFERENT -> single server vs distributed environment
		- when u design data something something
	- in **RDBMS**, put two updates of M in a transaction, to ensure that P will either read both data items before the update or both after the update
	- in **NoSQL**,
		- Graph databases support ACID transactions.
		- Other supports atomic updates, but only within a single aggregate 
- Replication consitency: ensuring that the same data item has the same value when read from different replicas
	- ![[Pasted image 20240916111220.png]]
		- **Consistency Window**: the window when everything in the environment is consistency
- Read-your-write consistency: once you made a update, you aer guaranteed to coninue seeing the update
	- ![[Pasted image 20240916111258.png]]

### Trading off consistency for other characteristics
- trading off consistency for high performance (e.g. throughput, latency) made by applications
	- RDBMS-Isolation level
	- NoSQL systems - Turnable Consistency (used by Cassandra)
- Trading off consistency for availability vise versa in the design of NoSQL systems
	- the CAP theorem (to emphasize, this deals with the **DESIGN** of the system)

### Brewer's CAP Theorem (important)
- WIthin a large-scale distributed data system, there are three requirements to consider: **Consistency, Availabilit, Partition tolerance**. th theorem states that you can strongly suppot only **2/3** in any given system
	- **Consistency**: every read receives the most recent successful write (a system appears as if there were only one copy of the data and all operations on it are atomic)
	- **Availability**: IF you can talk to a node (non-failing node) in the cluster, the node can read and write data
	- **Partition Tolerance**: The system is functional despite network partition. 
- A distributed data system cannot give up the partition tolerance prooperty, leaving us only **two real options** to compromise on: **availability and consistency (Consistency or Availability when Partition tolerant**) 
- Cool dagram that classifies different database systems
	- ![[Pasted image 20240916112254.png]]
		- NOTE: 
			- it not strictly precise
			- not binary decision
			- trade off a little consistency to get some availability
			- practically trade off *something*

### CA Systems
- a single server system
	- single machine cant partition -> no worry about partition tolerance
	- only one node - if it is up, it is available
	- most of relation databse systems which support ACID
- A CA cluster is possible but ...
	- you likely use 2PC for distributed transactions. The system will block when a network partition occurs

## CP Systems
- Example - Master-slave replication
- all writes are done at the master  node. there may be a short read inconsistency window at slave nodes
- a non-failing slave node is considered to be unavailable because one can talk to the slave node but cannot write on it.

## AP Systems
- Example: peer-to-peer replication
- a node can take writes and reads - update and replication inconsistencies present
- How to resolve inconsistencies depdnds on the application.
	- i.e. from Amazon Dynamo paper: you are always allowed to write, even if network failures you may end up with multiple shopping carts. the check out process cna merge them into a single cart and return it

## NOte: Consistency in CAP
- CAP Consistency: aludes to atomicity and isolatioon
- in ACID: means that data does not satisfy predefined constrains

## versioning
- concurrency control methods: lock vs versioning 
- **Version Stamp** - a field that changes very time the undedrlying data in the record changes
- Basic version stamp works well for a single server or a master-slave replcaiton where you have a single authoritative source for data
- Example: conditional-update use etags of HTTP protocol
	- An etag is a version stamp for a resource
	- For each GET request for a resource, the server response with the etag of the resource in the header
	- To update a resource, submit the eetag form the last GET for the resource
	- When the update request arrives, the serve compares the etag from the client and that in the serve. the update request is refused when they mismatch
	- EXAMPLE: GET X PUT X (a basic update)
		- if get fails then put would make no sense
			- would fail if someone else updates the same data during your update
		- so system will refuse the put
		- etag is used as the versioning

## Vector stamps on Multiple Nodes
- a special form of version stemp, called vector stamp, is used in peer-to-peer NoSQL systeem
- Example: scenarios resulting in inconsistency
	- ![[Pasted image 20240916113334.png]]
- The vector stamp is a set of counters, one for each node

## VEctor stamp for peer-to-peer replication
How vector stamps are assigned? (this was my idea on reading timestamps to get the latest data)
1. each time a node has an internal update, it updates its own counter
	1. i.e. an update in the green node changes the vector of the green node to [red:43,green:55,black:12]
2. when this update is sent to other nodes to synchronize other replicas, the vector stamp of the updates goes with it.
3. When a update is received, the receiving node updates its vector stamp by taking the maximum of the recieved vector stamp and its current vector stamp
- ta < tb and only if they meet two conditions:
	- they are not equal timestamps (there exists i, ta[i] != tb[i]) and 
	- each ta[i] is less than or equal to tb[i] (for all i, ta[i] <= tb[i])
- One can tell if one version stamp is newer than another.
	- i.e. [red:1, green:2,blue:5] is newer than [red:1,green:1,blue:5]
- a write-write conflict presents if the order cant be determined.
	- i.e. [red:1, green:2, blue:5] vs [red:2,green:1,blue:5]
- a vector stamps spot inconsistencies, but doesnt resolve them, conflict resolution will depend on the domain you are working on and its applicaitons/uses

![[Pasted image 20240916114337.png]]