
## Video NOTES
![[Pasted image 20240930104748.png]]
- index **is** **IMPORTANT**
- to improve performance, you can create a case-insensitive 
![[Pasted image 20240930105936.png]]
![[Pasted image 20240930110127.png]]


### $in, $nin, and $all 
![[Pasted image 20240930111740.png]]

### $size, $slice, and $elemMatch
![[Pasted image 20240930112302.png]]

![[Pasted image 20240930112521.png]]
![[Pasted image 20240930112623.png]]
![[Pasted image 20240930112949.png]]
![[Pasted image 20240930113645.png]]


## LIVE Lecture Notes
![[Pasted image 20240930104843.png]]
- Notes: 
	- Ordinary index does not 
	- First: case sensitive, index bound `sku: [ '("abc", "abd")`]
	- Second: case insensitive -> look at the `/^abc/i`
		- `""` -> beginning of index range
		- `{}` -> end of index
			- this is silly so there is a better way

![[Pasted image 20240930105314.png]]
- Notes: 
	- `collation` helps with caseinsensitive search
	- `CollationKey` key are the encoded representations used in indexes to facilitate case-insensitive and locale-aware operations in MongoDB
	- ![[Pasted image 20240930105456.png]]
		- this is useful because case-insensitive querries CANNOT use index

![[Pasted image 20240930110432.png]]
![[Pasted image 20240930111156.png]]
![[Pasted image 20240930111328.png]]
![[Pasted image 20240930111354.png]]
