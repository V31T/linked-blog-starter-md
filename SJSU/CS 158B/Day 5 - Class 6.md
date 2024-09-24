---
created: <% tp.file.creation_date() %>
tags:
  - CS158B
  - SJSU
---
## RMBR
- MIDTERM is the **25th**
	- knowledge based questions
		- i.e. multiple choice
	- some solving questions
	- computer canvas quiz using lockdown browser
	- 1 hour to take the test
	- mcq, fill in the blank, and short answer
	- Should be doable with just studying the slides and class discussions
	- cheatsheet for midterm 1 -> most likely 1 page double sided

# Notes

## SNMP Object Syntax
![[Pasted image 20240911193757.png]]
- more notes in the last lecture
- Remember the notes about Objects and the such
- Objects can be marked as obsolete/deprecated
	- deprecated: "should not be used" but is still being supported
- Defintion value contains what the definition of the object is 


## MIB-2 Definitions
- implemented universely, get the link from the slides

## Scalar Example
- Object = iso.org.dod.internet/mgmt.mib-2.tcp.tcpMaxConn
- OID = .1.3.6.1.2.1.6.4
```
tcpMaxConn OBJECT-TYPE
	SYNTAX INTEGER
	ACCESS read-only
	STATUS mandatory
	DESCRIPTION
		"Description here"
::= { tcp 4 }
```

## SNMP Composite Types
- Record or Struct type: `SEQUENCE {fieldname1 typ1, fieldname2 tpy2, ..}`
```C
struct Person {
	int age;
	char name[0];
	String address;
};

```
```SNMP
SEQUENCE Person {
	age INTEGER,
	name STRING
}
```

- Array type: SEQUENCE OF type where type is an object
	- a dynamic array
- Table: SEQUENCE OF type where type is a SEQUENCE
	- syntactically the same as Array but conceptually different
	- basically is just a 2d array, a dataframe, a whatever
- SNMP only supports 1dimension or 2dimension arrays

## SNMP Table
- Access vie
	- Primary KEy lookup
	- Linear Search
- Key can be a single attribute or a set of attributes, known as INdex
- An SNMP table index acts as a *constraint*, disallowing two distinct rows with identical index values

`fooTable[6][4]`

|     | 0   | 1   | 2   | 3   | 4       | 5   | 6   |
| --- | --- | --- | --- | --- | ------- | --- | --- |
| 0   |     |     |     |     |         |     |     |
| 1   |     |     |     |     |         |     |     |
| 2   |     |     |     |     | fooData |     |     |
| 3   |     |     |     |     |         |     |     |
| 4   |     |     |     |     |         |     |     |
- `x = fooTable[2][4]` <- this is called Row Major
	- DOES NOT WORK IN SNMP
- SNMP follows Column Major
	- so the correct way is `x = fooTable[4][2]`

##  Columnar Objects
- there are 2 techniques for identifying a columnar object instance
	- Random-access technique 
	- Serial-access technique 
- Table recap:
	- A table consists of a set of 0 or more rows
	- Each row contains the same set of scalar object types, or columnar objects
- Each columnar object has a unique object identifier that is the same in each row

## SNMP Table Example: ifTable

- ifTable is in MIB-II
- Each interface has an abstractly assigned interface number, known as `ifIndex`. It is a single integer
- In an SNMP table 1 or more columns is an index
	- what?
		- we can set a column (i.e. 0) as an index
			- this means that the value of index is unique 
				- same concept as constraints from SQL database
- ifTable example
	- There is only one INDEX object, namely ifIndex
		- its value os an integer in the range between 1 and the value of ifNumber
		- Each interface is assigned a unique number
	- What is the interface type (ifType) of the 2nd interface?
		- OID of ifType = *1.3.6.1.2.1.2.2.1.3*
		- ifIndex = 2
		- Therefore, ifType instance indentifier = *1.3.6.1.2.1.2.2.1.3*.**2**

## STOPped paying attention after that until this

## Table visualization
- T = ifEntry
- Nodes are labeled T.col.row
- Blue-bordered are internal nodes, rest leaf nodes
- table-view
- Tree-view

## ifTable example
oof

## ipRouteTable
- Index is "dest", an IP address
	- which means every IP address/destination should be **UNIQUE **
- ifTable index is dense, ifIndex are typically consecutive numbers
- ipRouteTable index (dest) is sparse 

## tcpConnTable
- 2d table with scalar valued entries
- Example: tcpConnTable (RFC1213)
- OID = mib-2 -> tcp (6) -> tcpConnTable (13)
- this table  basically represents 
- the index is composite
	- takes 4 columns to form the index 
- What is tcp
	- tcp connection is between 2 computers
	- there can be multiple connections
	- Example:
		- comp A 
			- ports 100, 200
		- comp B 
			- ports 300, 400
		- a tcp connection between A and B on ports 100 and 300 would be represented as this in a tcpConnTable
		- `A, 100, B 300`
			- this is why the index is composite
- tcpConnState instance identifier = 
	- OID
	- localaddress
	- localport
	- remoteaddress
	- remoteaddress
			- look at the slides and make sure to understand how the top picture correlates to the bottom picture
	- x is the OID of the tcpConn

## Table definition and structure
- i am not typing all that

## More table example

## i stopped paying attention get the rest from the slides

## Demo: Table -snmptable -tcpConnTable
```bash
snmptable man just get this shit from the slides
```



## SNMP protocol limitation
- it is not possible to add an object
-  it is no tpossible to delete an object
- the snmp manager cannot add new rows to a table
- the options are only
- [GET*] Read
- [SET] Update if allowed
- only the leafe objects can be accessed