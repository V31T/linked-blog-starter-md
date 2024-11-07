
## NOTES

## CRUD OPERTAIONS

- insert/create: 
- `insertOne() ` and `insertMany()`
![[Pasted image 20240925103523.png]]
- `insertOne() ` vs `insertMany()`
	- with a specified number of documents, insertOne() takes more round trips between app and database, and thus it is slow compared to bulk operations such as insertMany()

### History of Insert
- insert has been deprecated -> because
- `db.foo.insert{id:001}`
	- assume the db has {id:001} already
	- -> insert will throw a document containing error message (NOT an exception)
	- ^ the reason to why it has been deprecated because error message sucks compared to exception handling
		- Exception handling allows code to run in normal mode whether an exception is thrown or not
		-  ^^ ALLOWS THE USE OF TRY AND CATCHING WHICH IS VERYVERY GOOD
		- key point: although exception occurs, the catch block will handle it and the rest of the application will continue to run.

### Insert Validation
- The max BSON doc size is 16 MB
- to store docs larger than the maximum size, MongoDB provides the GridFS API
- to check the BSON size (in byte): Obkect.bsonsize(doc)
\>doc={"a":"b"}
{"a":"b"}
### FIND method
![[Pasted image 20240925104643.png]]
- super good and strong very pog
	- query: where/how to select data
	- projection: how to project the fields from the given documents
	- Returns: a cursor to the doc that matches criteria
![[Pasted image 20240925105827.png]]
![[Pasted image 20240925105949.png]]
- document ending bracket in `red`
![[Pasted image 20240925110111.png]]
`find()`
![[Pasted image 20240925110709.png]]

### sort(), skip(), limit()
![[Pasted image 20240925111247.png]]

### Cursor Manipulation in Mongo Shell
![[Pasted image 20240925111510.png]]

### Capped Collection
- created in advance and its fixed in size 
- `db.createCollection(:addit100", {capped:true, size:20480, max:100})` -> the size limit takes precendence over the max limit
- behavior like circular queue: if it runs out of space, the new document will over write the oldest document.
- documents are stored in insertion order
	- documents cannot be removed
	- updates causing documents to grow in size cannot be done
- good for logging and auto archiving data
	- i.e. oplog.rs that stores a log of operations in a replica set

### Natural Order
- natural sort: documents in the order that they appear on disk. 
	- Normal Collection: natural order may != insertion order
	- Capped Collection: natural order = insertion order
- with `sort{$natural:1)` , MongoDB returns document in forwarding natural order 

### findOne()
![[Pasted image 20240925112054.png]]

![[Pasted image 20240925112513.png]]

### Query and Projection Operators
![[Pasted image 20240925112939.png]]

#### Comparison: $gt, $te, $lt, $lte, and $ne
![[Pasted image 20240925113011.png]]
- used within the predicate
- $ne compares value of fields 

#### Logical: $or, $and, $not
![[Pasted image 20240925114012.png]]
- using or `.find({$or:[{"Title": "Toy Story 3"},{"ISBN":"978-1..."}]})`
	- "logical disjunction"


## Whiteboard Notes
![[Pasted image 20240925104344.png]]
### Exist-tensial Find
![[Pasted image 20240925105411.png]]
- notes: the `.` within the parameter means it is an embedded document 
- "if there exists such a field"
	- good for unstructured big data

![[Pasted image 20240925113254.png]]
- 2 conditions separated by `,`
	- "there should be elements that satisfy the 1st condition and elements that satisfy the 2nd element"
	- uh idk what gets returned ask chatgpt later, what does Cast do?
	- 