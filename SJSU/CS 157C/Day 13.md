
## VIDEO NOTES

### SHARDING
- sharding strategy
	- shards and shard key point to chunks
		- chunks -> unit of data migration
	- mapping shards based on:
		- hashed based
		- ranged based
	- there are CHUNKS
		- contains:
			- min - max RANGE
				- these ranges can NOT overlap
		- how we decide on chunk size is based on sharding strategy
	- RANGE BASED:
		- 3 chunks:
			- 0-5, 5-10, 10-15 (min-max)
	- Hashed based
		- range is based on shard key hash
		- 
- ![[Pasted image 20241009104152.png]]

![[Pasted image 20241009104721.png]]
![[Pasted image 20241009105009.png]]
![[Pasted image 20241009105601.png]]
![[Pasted image 20241009110431.png]]
![[Pasted image 20241009111227.png]]
![[Pasted image 20241009111542.png]]
![[Pasted image 20241009111829.png]]
![[Pasted image 20241009111838.png]]
- counter is within the memory of mongos
![[Pasted image 20241009112223.png]]

### Replication
![[Pasted image 20241009113232.png]]


## LECTURE NOTES