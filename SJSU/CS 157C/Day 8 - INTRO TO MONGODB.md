
## Handling concurrency control
- Wired tiger
	- the default storage engine as of MongoDB3.2 (MMAP used to be the default)
	- docoument level concurrency control (MVCC: Multiplie)
		- done by snapshot
			- snapshot isolation level
				- holds read and write lock
					- writers do not block readers and vice versa
			- ![[Pasted image 20240923103337.png]]

### Index Fundamentals
- when creating index, b tree is created within the disk
	- when searching, index should be loaded to memory and then the search is done
		- write operations now come with overhead using this method

## Slide NOTES

### BEFORE GOING OVER STUFF
- MongoDB has a document size limit
	- to ensure efficiency, but what if we need large size?
		- this is why it used GridFS

### GridFS
- the max size of a MongoDB document in BSON: 16 MB: not enough for movie clips, high quality clips etc
- GridFS is to store large files and yet to access parts of the file without retrieving the entire thing
- TO MongoDB, files inGridFS are just normal collections constraining documents.
- GridFS consists of two collections
	- `Metadata` are in the `files` collection
	- Data are broken down into chunks that are stored in the `chunks` collection - easy and scalable
	- how GridFS processes a large file
		- ![[Pasted image 20240923104506.png]]
			- doc.jpg is split through the GridFS driver into fs.files and fs.chunks
				- these 2 collections have no relation to eachother
				- `fs.` is to make collection unique

### Using GridFS using pymongo (python driver)
![[Pasted image 20240923105410.png]]

### Replica Sets
- a replica set is a group of mongodb instances that maintain the same data set
- a replica set has one primary server (master server)
- the primary server handles all the write requests from the clients
- when a write occurs, it is logged in the primary's oplog
- the `oplog` is replicated by the secondary servers (slave servers) in the same replica set
- when the primary fails, a new primary will be elected among surviving members of the replica set

### Sharding
- sharding provides horizontol scalability - additional shards can be added to increase resource capacity without any changes to your application code
- auto-sharding: mongoDB takes care of all the data splitting and recombination for you

### Advanced Queries
- Map and Reduce functions (deprecated as of 5.0)
	- the map function is to find all the documents that meet a certain criteria. these results are then passed to reduce function, which processes the data
- The Aggregation Framework
	- map-reduce can be slow
	- pip line based aggregate operators implemented in C++; highly performant
	- If you would normally use GROUP BY in SQL, then the aggregate funciton may be the right tools for the job in MongoDB
- MongoDB's MapReduce function
	- ![[Pasted image 20240923110414.png]]
- Pipeline based aggregation
	- ![[Pasted image 20240923110607.png]]


## Video Notes
- note: work is being done within the ubuntu docker container
- i did not pay attention


# MONGODB DATA MODEL (new set of slides)

## Document
- the unit of storage in MongoDb (vs row in RDBMS)
- the maximum BSON document size is 16 MB
- Field name are strings
- Values can be any of the followiing BSON types
	- String,Integer, Boolean, Double, Min/Max keys, Array, Timestamp, Object, Null, Symbol, Date, ObectID, Binary Data, Regular Expression, Java Script code
- MongoDB is a type-sensitive and case sensitive
	- `{"foo":3}` is distinct form `{"foo": "3"}` and `{"Foo":3}`
- A MongoDB document cannot have duplicate field names.
	- `db.foo.insertOne({"foo":30,foo:20})`
- Field_value pairs in documents are ordered 
- ![[Pasted image 20240923111454.png]]
- 
- not requires every document to have the same field, or that every field with the same name has the same type of value.
- ![[Pasted image 20240923111551.png]]

### \_id field of document
- each document has a unique \_id field that acts as  a primary key
- if an inserted document omits the `_id` field, MongoDb automatically generates an ObjectId for the `_id` filed.
- bybdefault., MongoDB creates a unique index on the `_id` field during the creation of a collection
- the default value is an ObjectId BSON data type consisting of a 12-bye binary value:
	- Time: the second since the Unix epoch
	- Machine Identifier 
	- Process id
	- Random Counter
- ![[Pasted image 20240923111827.png]]

### Collection 
- a Collection is a group of similar documents
- Advantages of grouping related types of documents together:
	- applications code takes less effort to weed out irrelevant documents
	- Faster to get a list of collections than to extract a list of the types in one colleciton.
		- i.e. having three collections skim, whole, chunky monkey (faster) vs Having one collection where each document has a type of field specifying the document is about skim, whole, chunk monkey
	- Data Locality
		- i.e. Getting blog posts from a collection containing posts only (less disk access) vs Getting blog posts from a collection containing posts and author data
	- Efficient Indexing 
- Dynamic Schemas: Documents within a single colection can have any number of different shapes (different fields and different types of values). you do not need to predefine a structure for any of hte documnets
- Supports programming in a dynamic typed language such as Python or PHP
- Still ned to design database and define indexes.
- Expandable collection (default) vs capped collections
	- expandable collections: the more data you add to it, the larger it becomes. capped collections can contain a certain amount of data. 
	- `db.createCollection({"log", {capped: true, size: 10000}})`
		- size in bytes
- Every collection should have a unique name

### Subcollections
- a **naming convention** to organize collections
	- i.e. blog.posts blog.authors
- This is for organizatoinal purpose only. there is no parent and child relationship between blogs and posts

### Data Model: MongoDB vs RDBMS
![[Pasted image 20240923113845.png]]


## REVIEW
- FOREIGN KEY IS A CONSTRAINT IN RDBMS -> referencing is NOT a constraint in MongoDB

## Video Notes
- ![[Pasted image 20240923112420.png]]
- capped collections
	- circular queue (oldest data is replaced by newest data)
	- new data/writes are just appended
		- makes write super quick
	- ![[Pasted image 20240923113522.png]]
	- oplog is necessary to support replica set
		- how? when there is a write operation in master, data of master is updated and should be propregated, instead of sending data that could be huge, the oplog is sent instead