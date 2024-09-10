---
created: 2024-08-29 14:02
tags:
  - CS157C
  - SJSU
---
AFTER EACH CLASS SHE WILL POST LECTURE SLIDES AND PRERECORDED LECTURE VID

FUNDAMENTALS
- 2 key topics
	- strength of relational system
	- limitations of relational system, specifically for big data
		- to learn how nosql overcomes the limitation

Relational Databases
- 7/10 top database software is relational
- essential skill is to choose the right database solution that matches that right problem

Value of RD
- rigid
	- relation schema
		- defines relation name, attributes and domain name
	- structured data 
	- app logic becomes simple
	 - SQL can describe a table-oriented operation at high level
- SQL
	- feature rich and uses simple declarative syntax
	- powerful
	- easy to use - basic syntax
	- JOIN operations are very pog
		- NoSQL does not support join operation
			- because very expensive 
	- Declarative Vs Imperative
		- answering why join is important to SQL and not included in  NoSQL
		- Imperative Language:
			- how to do something, sequence of steps to achieve a task (e.g. Java)
				```User[] user = new User[100];
				for (int i = 0; i < User.length; i++) {
					if (user == anotheruser) {
						print; }
					}
				```
					- programmer must include all the steps
		- Declarative Language
			- what needs to be done (i.e. SQL)
				```SELECT name FROM User WHERE id == 1001;```
			- describes sequence ig
		- a SQL query is the same as a compiler
			- database is saved on disk
			- operation is done on memory
				- database system has a dedicated memory space called the buffer
					- so that the operations can be ran in memory
			- depending on size of buffer and database size
				- buffer can be too small
					- leading to multiple page loading
				- i.e. ```SELECT name FROM User WHERE id == 1001;```
					- called Full Scan
		- Full Scan vs index Scan
			- creation of index is apart of the database design
			- index is used when application accesses something very frequently
				- persisted as a B tree
			- i.e. id set as index and will be loaded into the buffer
				- so instead of loading entire user data to the buffer, we just load the id to the memory 
			- index is just primary key i.g.
	- Why is join necessary
		- normalization is necessary to get rid of redundant data
		- query can compose data from multiple tables and join on a specific attribute
	- What is Normalization?
		- reduce redundancy within individual tables to build a clear relationships among tables to void unnecessary duplication and maintain data integrity
			- update/delete anomalies
		![[Pasted Graphic.png]]
			- update anomaly: updating the movie name will not update the star name
			- remove anaomaly: removing GWW will completely remove VL/star data existence 
				- instead use foreign keys
				- star data will be replaced with keys that point to the star data, so instead you will be deleting pointers instead of the actual data
				￼![[Pasted Graphic 2.png]]
				- join operations make it possible to access both data
		- something about why nosql is good with distribution
			- join 
	- DEnormalization
		- important when data is being accessed together frequently
	- normalization designer does not care how data is access by the application
		- designer must examine data access pattern of the application
			- and make indexes based off of it
	- instead in nosql database modeling
		- when data is saved/distributed the designer must examine the data access pattern of the application
			- i.e. book and author; the designer will save book and author data together (within same table (?))
	EXAMPLE
	￼![[Pasted Graphic 3.png]]
		- left is SQL
			- join on AuthorID to retrieve data on both title of book and its author
		- right is NoSQL
			- note how author data is embedded into the book data because they are accessed together a lot
			- although data is redundant, since the data is very related/accessed together a lot, it is okay/ allows performance increase	
		
- Transaction - ACID properties (why does NoSQL support ACID)
	- atomicity - all or nothing, no partial failure
		- about changes made by a transaction
		- in mongoDB, ensures atomicity by IDK DIDNT GET
			- now supports multi transactional operations
	- consistency - data moves from one correct state to another correct state
		- consistency in relational
			- columns only store values of a particular type
			- pk nad unique keys are unique
			- check constraints are satisfied
			- foreign key (aka referential integrity) constraints are satisfied
			- in an app that transfers funds, the consistency prop ensures that the total value of funds is …………
			- is about when transaction writes/modifies data, before transaction database must be correct, and after database must be correct
		
	- isolation - concurrent transations wil not become entagled with each other
		- higher isolation means higher concurrency
		- ensures serializability of concurrent execution of transactions - operations may be interleaved
			- serializability
				- i.e. Transaction with 2 operations
					transacation 2 with 2 more operations
				- serial execution means T1 is completely done then T2
							        T2 is completely done then T1
					- system interleaves the transactions in noSQL
				- serializable means that if interleaved operations have the same output as serial execution, then the system is serializable 
		concurrency control ensures the system is serializable
	- durability - once a translation has succeeded, the changes will not be lost