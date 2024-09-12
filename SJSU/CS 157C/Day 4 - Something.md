---
created: 2024-09-11 17:55
tags:
  - CS157C
  - SJSU
---
Review:
- there is a tradeoff between concurrency and isolation
- durability
	- write ahead transaction log
		- before data is changed there is a log that is created
- Limitations of RDMS specifically when it comes to large amounts of data
	- volume, variety, verocity, v-
	- scalability and impedence mismismatch
		- scalability -vertically or horizantolly 
			- vert => the server itself will get buffed
				- limitation -> can only get buffed so much
			- horizontally => increase capacity of the server by adding more servers/computers
				- more server => distributed system -> transaction are distributed
					- maintaining ACID on distributed systems is VERY expensive
					- a lot of netowkr communication to ensure a 2PC commit
						- takes a lot of time
							- voting phase and commit phase
						- with failure even more time loss
							- coordinator can wait for ever and could never end if one or more parts fail and never return anything
		- impendence mismatch
			- the way db percieves data and the way application percieves data is different
				- some layer in between must be used ot communicate -> ORM
					- costly
					- mapping code is sometimes very hectic

NOTES:
- characteristics of NOSQL Systems
	- characteristics related to distributed databases and distributed systems
		1. Scalability
			1. nosql runs on clusters to ensure high scalability
		2. Replication and eventual consistency
		3. replication methods (master-slave, peer-to-peer)
		4. partitioning (sharding)
			1. partitioning and sharding mean the same technique, sharding is just mongo terminology, partitionin is the general term
		5. high performance data access
	- Characteristics related to data models and query languages
		6. Schema flexibility: schema-on-read (as compared to schema-on-write (schema should be explicitly defined before being created and should be followed) in RDBMS)
			1. schema-on-read -> structure of data is implicit, schema does not need to be defined before implementation
				1. means new data/attributes can easily be added and implemented into the schema
		7. less powerful query languages 
			1. nosql does not support JOIN operations
1. SCALABILITY
	- Vertical 
		- expanding the storage and computing power of existing nodes/servers/computers
	- Horizontal (employed by NoSQL systems)
		- the distributed database system is expanded by adding more nodes for data storage and processing
2. Replication and Eventual Consistency
	- Data is replicated over multiple nodes in a transparent mannner to support low latency, high availability, and rad throughput
	- with replication, writes must be applied to every copy of the replcicated data with potential insonsistency among reads
		- note: replication does NOT increase write-throughput
	- Eventual consistency: all updates will propagate through all of the replicas in distributed system, but this may take some time. Eventually, all replicas will be consistent 
	- EXAMPLE: Benefits of Replication 
		- replication alone does not divide data
		- replication can latency improve read-throughput
		- replicating data causes write-overhead
			- in oder to support sstrong consistency, all copies must be completed before update is put through
			- there is an inconstistency window (time period after 1 copy is updated until the rest of the copies are updated)
				- attempting to read data during this window will lead to consistency problems
			- in order to support strong consistency (everyone reads the same data) the user must wait 
				- so tradeoff between consistency and latency
			- BUT if there is no further write on the data, the data will EVENTUALLY be consitent 
3. Replication Method
	- Master-slave replication
		- a master handles the master copy. All writes are applied to the master copy while slaves synchonize with the mater and may handle reads
	- Peer-to-Peer replication
		- all the replicas have equal weight and they can all accept reads and writes
		- more prone to consistency problems
	- EXAMPLE:
		- master to slave
			- one line of communication
			- single point of value
				- if master fails, the entire system can not support write operations
					- called "single-point failure problem"
			- Used by MongoDB
		- peer-peer
			- multiple lines of communication between peer to peer nodes
				- more consistency issues
			- used by Cassandra
			- multiple points of value
				- if a node fails, the entire system can still support write operations
					- = more "availability"
		- summary 
4. Partitioning (Sharding)
	- REMEMEBR: Replication copies data across multiple data VERSUS Partitioning that divides data into dif partitions and distributes these partitions accross multiple servers
	- Partitions are defined in such a way that each piece of data belongs to exactly one partiton 
	- IN MongoDb, each individual partition is refered to as a shard
	- Each partition is held on a seperate database server instance, serving as a small database on its own
	- Partitioning data to support horizontal scability 
		- : for queries that operate ona  single partition, so query throughput can be scaled by adding more nodes 
	- this is a key technique to improve horizontal scalability
		- each partitions improves write and read throughput
	- EXAMPLE: to show how each shard serves as a mini-database
		- collection of partitions
			- partition1 -> talks to where server1 (contains partition1)
			- partition2 -> talks to server2 (contains partition2)
		- an increase partitions/serveers will allow for higher arrival rates
		- ![[Pasted image 20240904112306.png]]
			- sharding increase both read and write throughput
	- Hash-based partitioning versuse range-based paritioning
		- when application asks for data
		- must understand parition(shard) key
			- say you have some collection that consists of documents (attributes: id, name)
				- all the data within document will not be seperated but different documents can be located in different servers
				- you can define which field(s) that will be used to declare the partition key
					- say we use id and name to declare parition key
			- hash-based
				- each server contains a range of hash values that can be stored within that server
					- hashes the value of the partition key and stores in the server that contains the hash value
			- range-based
				- ranged query
					- can access a range of data
					- accessing a wide range that takes multiple servers
						- idek
				- say our documents store a zipcode function
				- we can set the partition key to zipcode
				- range-based will store based on the direct range of zipcodes
					- if zipcode become popular and is access a lot is called a hotspot
						- horizontal scaling
				- ^ fix these notes
6. Schema Flexbility
	- it is not required to have a schema in most of the NoSQL systems
	- Freedom and flexbility to store daat (as compared to schema-on-write)
	- Can deal with semi-structured and self describing data (e.g. JSON and XML)
	- A schema-less database shifts the schema into the application code that accesses it. In application codes, there should present a set of logics to identify the structure to manipulate (schema-on-read)
7. Less Powerful Query Languages
	- SQL offers a rich set of DDL, DML, and DCL comands
		- used for application to access normalized data from various angles
	- NoSQL system provides a high level query language, but  queries themsleves in NoSQL are not as powerful as SQL query language. For example, the joins need to be implemented in the application programs
![[Pasted image 20240904114450.png]]

