---
created: <% tp.file.creation_date() %>
tags:
  - SJSU
  - CS157C
---
![[Pasted image 20240911104430.png]]
- **NOTE** we are working with columns so in the picture we are looking at **ONE ROW** of data
	- a row consists of column families and each column family consists of columns

## Apache HBase Data Model (example of wide-column databases)
- Conceptual View:
	- a table is a multidimensional sorted map.
	- The map is indexed by a row key, column key, and a timestamp; each value in the map is an uninterpreted array of bytes
- Example: 
	- the following table, called `webtable`, one row that contains two column families named contents and anchor. anchor contains two columns (anchor:cssnsi.com, ancho:my.look.ca) and contents contain one column (contents:html)
![[Pasted image 20240911104924.png]]

![[Pasted image 20240911105532.png]]
![[Pasted image 20240911110125.png]]
![[Pasted image 20240911111624.png]]
![[Pasted image 20240911112150.png]]
![[Pasted image 20240911112625.png]]
![[Pasted image 20240911113037.png]]
![[Pasted image 20240911113714.png]]
