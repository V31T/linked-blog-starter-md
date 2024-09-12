---
created: 2024-09-11 17:55
tags:
  - CS157C
  - SJSU
---
## REVIEW
- Consistency problems will always exist because of network issues
	- master slave is btter because writes can only be done to the master
	- peer to peer all can be written ttoo
		- must work on how to resolve consistency issues
- NOTE: partitioning and replication are just ways to created distributed systems
	- when database is created, we must design the systematic way the database finds data, which should match with how the data is distributed 
		- hash based and range based
		- each document (data in mongoDB) will have a shard key (one or 2 fields of document that will be defined as shard key)
			- hash based shard key -> hash is created based on shard key
				- very efficient but can NOT support ranged querries
			- range based shard key
				- preserve the values of the shard key and use it to distribute data based on the value of the shard key
				- problem: in the zipcode example, there can be hotspots where a certain zipcode is accessed the most, called a hotspot
					- **cannot be horizontally scaled**
				- but can support ranged querying
- SCHEMA Flexbility -> impendence mismatch
	- SQL -> rigid schema designed beforehand gaurantees that all data is in table form (2 dimensional) "scheme on write"
		- requires ORM to map data to objects
	- NOSQL -> very flexible, does not have a predefined schema, "schema-on-read"
- SQL has joins due to the normalization process, allows data to be distributed
	- NOSQL does NOT support JOIN
		- they are instead "key normalized"
		- able to embedd data in the same place (denormalized)

## NOTES

-focus on how key-value and document are different

MAIN NOSQL DATA MODELS
- Key-Value databases
	- Data model: a global collection of key-value pairs
	- i.e. RIAK, VOLDEMART, REDIS, AMAZON DYNAMODB, and in memory variants: MEMcacheD
	- **NOTE**
		- 
- Document Databases
	- Data model: Collection of documents often stored in a format such as JSON, XML, or YAML
	- i.e. **MongoDB**, CouchDB, Amazon DynamoDB
	- **NOTE**
		- does not support 
		- index on `attribute`
		- databases can implement multiple data models, look at Amazon DynamoDB
- Wide-Column databases
	- Data model: a tabular model where each row can have an individual configuration of columns
	- i.e. Google's bigTable, Apache Hadoop's HBase, **Cassandra**
- Graph databases
	- Data model: a netowrk of nodes and edges that connect the nodes. Both nodes and edges can have properties in a form of key-value pairs
	- i.e. Neo4j
	- **NOTE**
		- not an aggregate storer 
- Aggregate Data Models
	- Data mode: the model by which the database organizes data
	- Key-value, document and wide-column family - aggregate orientation 
Aggregate
- a collection data that is treated as a unit
- a unit for data manipulation and managment of consistency
- a natural unit for replication and sharding - easier for database to handle operating on a cluster
- easier for app programmer to work wit - impedence mismatch is resolved
	- aggregate can hold data as the database percieves data (?)
- An aggregate-orinted NoSQL system updates aggregates with atomic operations and communicates with the data storage in terms of aggregates
	- when there are multiple updates on an aggregate, all of them should be done or none
![[Pasted image 20240909110557.png]]
- **NOTE**
	- $inc = increment
	- $push = push
	- both of these changes should either be done or not done

## a relational data model for e-commerce web site
![[Pasted image 20240909110752.png]]
- **NOTE** 
	- Customer -> Orders: one to many
	- Customer -> Billing Address: one to many
	- Billing Address -> Address: many to one
		- same household families
	- Order -> Order item: one to many
	- Order Item -> Product: many to one
	- Order -> Order Payment: one to many
	- Billing Address -> Order payment: one to many
	- Order -> Address: one to one
	- SQL JOINS play a vital role in connecting all the database information together
		- One order can be associaated with many order items
		- just basic SQL review
- NOSQL implementation/approach
	- "FLATTENING" -> denormalizing data resulting in redundancy
	- Customer, Order, and OrderPayment contain Address value, resulting it  to be used 3 times
		- improves query performance in a distributed environment
- Alternate 
	- Thinking "Where to draw an aggregate boundary depends on the use cases of an application. We want to **minimize the number of aggregate to access during a data interaction**"

## Foreign Key in RDBMS vs. Referencing in MongoDB

- 1. Foreign Key Constraint
	- updates can be rejected because of Foreign Key being registered as a Constraint 
- Denormalization - whenever possible, embedding is recommended.
- Referencing 
	- 1. is NOT a Constraint
		- changing the reference to a book ID that doesnt exist, the database system will not refuse
	- 2. Does not support JOIN
		- application must describe all logic to implement JOIN
		- results in multiple 'round trip' which slows down application performance 
			- costly and is why referencing is not recommended UNLESS you are expressing a "many to many" relationship
	- Def search up more about this later

### Relational vs. Aggregate Data Model

- relational data model
	- easily look at the data in different ways
	- the database cannot use a knowledge of aggregate structure to help to store and distribute the data
	- ACID Transactino - the real point is atomicity
- Aggregate data model
	- helps greately with running on a cluster - by explicitly including aggregates. the database knows which bits of data will be manipulated together, and thus should live on the same node.
	- Atomic manipulation of multiple aggregates has to be managed in the application code. (Recently, NoSQL systems start embracing transactions. for example, MongoDB supports Multi-documents ACID transactions.)

### Key-Value and Document databases
- key-value and document databases are strongly aggregate-oriented.
- In a key-value store, the aggregate is opaque to the database
	- the value is a big blob of mostly meaningless bits
	- the aggregate can store whatever it likes
	- the value of an aggregate can be accessed as a whole based on its key
- in a document store, the database is aware of the internal structure of aggregate
	- more flexible access to an aggregate 
		- we can retrieve part of the aggregate rateher than the whole thing
		- the database acn create indexes based on the contents of the aggregate.
	- the database imposes limits onwhat we can place in it, defining allowable structure and types
