---
created: <% tp.file.creation_date() %>
tags:
  - CS157C
  - SJSU
---
- ISOLATION CONT
	- Transactions will lock a table/database
		- User1 starts transaction/lock, user2 cannot access/modify the database until after
	- ISOLATION LEVELS
		- control the degree of locking that occurs wen selecting data
		- Read uncommited (lowest)
			- dont care if corrupted, i just want it fast
		- Read commited
		- Repeatable reads
		- Serializable (highest)
			- integrity of data is more important than latency
			- wants no concurrency problems
	- Concurreny is good to know when talking about trade offs of integrity and speed in nosql databases
	- Read Phenomena (common problems)
		-dirty reads
			![[Pasted Graphic 4.png]]￼
			- basically after rollback, the T2 update gets undone, making T1’s 1nd Select a dirty read
		- non-repeatable reads
			![[Pasted Graphic 5.png]]￼
			- T1 has already seen a diff value
		- phantom reads
			￼![[Pasted Graphic 6.png]]
			- special form of non-repeatable read because after 1st read, T2 inserts a phantom into the range, so T1’s 2nd select will have a phantom inside its range
	- intuiton: more concerrency control > more problems : more concurrency/isolation control > less problems
		- concurrency is implemented through locks
			- so strong lock = less problem 
				- blocks more transactions = more latency
			- weak locks r the opposite
	- locks
		- read and write locks
		- write lock
			- weak
				- after write, transaction will be released
			- strong
				- if transaction holds lock, it will hold lock until the end of the transaction
		- read lock
			-weak
				- after read, transaction will be released
			-strong
				-after read is done, hold read until end of transaction
	- in order to remove dirty read, a strong write lock is needed,  and a weak read lock is okay
		- the strong write lock will prevent T1 from trying to read until the end of T2’s transaction
	- removing non-repeatable reads
		- read lock’s solution does not work because T2’s commit releases the strong write lock, making it possible for T1 to read
		- instead need a strong read lock is needed
	- phantom reads
		- T2 is not updating what T1 initially read
		- strong read lock and strong write lock
			- also adopts a strong RANGE lock to ensure that nobody can read/write within teh range
-Durability: concerned because transactions write on the database, all systems must be maintained 
	- gaurantees that transactions that ahve commited will survive any subsequent mal-functions
	- i.e. if a flight booking reports that a seat has succesffully been booked, then the seat will remain booked even if the system crashes
	- write-ahead transaction log: first write changes to a transaction log
	- NOTE: Data is saved in disks, and operations are done in memory
		- indexes is data structure in disk
		- index operations are done in memory
			- return pointer that points to area in disc
		￼![[Pasted Graphic 7.png]]
	- Durability is to preserve committed writes
		- say transaction has a lot of operations (read and write)
			- durability only cares about writes
				- all commited writes should survive in the disc even after system failure and media failure
	- Log consists of Log Entries 
		- UPDATE User SET age = 31 WHERE id = 1001;
			- Log entries hold central information to replay the update/operation to either redo or undo the operation
		￼![[Pasted Graphic 8.png]]
	- Write Ahead Log Protocol (WAL) 
		- before updating/changing/anything data, you must log first
		- Commit means all the logs of all the writes are gauranteed to be in the Disc
			- note: Commit is about the LOG not about the data/disc

THE FOUR V’s OF BIG DATA
- Volume
	- system should scale / Scale of data
	- relational designs struggle
	- nosql run on clusters to support high scalability
-Variety
	- data comes in various forms
	- relational systems with rigid designs
-Velocity
	- uncertainty of data
-Veracity

LIMITATIONS OF RDMS
- Scalability problems
	- transactions become difficult under heavy load
	- distributed relational databases (horizontal scaling of relational databases) account for distributed transactions which uses 2PC (two phase commit)
		- voting phase and commit phase
			- voting
				- if yes, coordinator sends commit request to everyone in the voting phase
				- if no, transaction aborts
				- introduces high latency 
	- 2PC blocks introducing higher latency during partial failure
		- scalability becomes limited when networks grow
- impedance mismatch
	- difference between the relational model and your domain objects
		- i.e. database stores data in rows and columns, JAVA stores data in objects
	- to create properly normalized schema, you need joins
	- ORM (i.e. Hibernate) needs extended memory requirements and increasingly unwieldy mapping code
		- writing mapping code is incumbering 
	- WHY IS JDBC NOT OBJECT ORIENTED?
		- say you have a java app that wants to access a database, you need a layer to communicate between them
			- this layer is JDBC (java database connectivity)
		- Java will send SQL commands to the database through the JDBC
		- RDBMS will return a table/tuples
		- the JDBC library will wrap the table/tuples in a resultSet that embeds table
		- Java will be able to iterate over the resultset that is table oriented 
NEXT CLASS
￼![[Pasted Graphic 9.png]]
