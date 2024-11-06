
## Notes

# RMON?
- used for Layer-2
	- hosts were identified by MAC Addresses
	- cannot analyze transit traffic through a router

## RMON**2**?
- has visibility into Layer-3 and above
	- including IP packets and IP addresses
	- can analyze transit traffic through a router

#### Notable RMON2 MIBs
![[Pasted image 20241007193347.png]]
- Notes: 
	- `nl` stands for "Network Layer"
	- terms: addressMap, nlHost (traffic into and out of hosts), nlMatrix (trafffic between hosts)


### Time
![[Pasted image 20241007193927.png]]
- new in RMON2 
- i.e. if we do getNext, agent will give all information that is available 
	- say we only want to get new data and not keep on retrieving old data
	- `TIME` can be used as an indexing object
	- ![[Pasted image 20241007193714.png]]
- `TimeFilter`: 
	- same syntax as `TimeTicks`(time counter)
	- exclusive index to a table
	- Purpose: Manager to retrieve only those rows that have changed since a specific time
- ![[Pasted image 20241007193941.png]]
- ![[Pasted image 20241007194151.png]]
-  notes:
	- the pseudo code:
		- it goes through table and sends back the response where entry timestamp is greater than the request timestamp
- ![[Pasted image 20241007194401.png]]
- Notes: 
	- uses `sysUpTime` to get the *approximate* timestamp 
	- the response basically is saying that the sysUpTime is 600 and then use that sysUpTime in the following request to act as the `timestampe`

## MIDTERM 1 SUMMARY
- graded liberally 
![[Pasted image 20241007195147.png]]
![[Pasted image 20241007200043.png]]
![[Pasted image 20241007200955.png]]

question 11 may be wrong

### WHAT THE FUCK IS PROMETHEUS????????
- an open sourced metric based monitoring system
	- created by SoundCloud?????
- wait this shit sounds really cool
- ![[Pasted image 20241007201517.png]]
- Basically is a super cool opensourced tool used to track the overall system health, behavior, and performance rather than tracking the individual events within the system. 
- ![[Pasted image 20241007201944.png]]
	- Prometheus can scrap data from multiple applications
- ![[Pasted image 20241007202116.png]]
- ![[Pasted image 20241007202320.png]]
- ![[Pasted image 20241007202355.png]]
	- good but also bad
- ![[Pasted image 20241007202507.png]]
	- counter can wrap around
	- gauge cannot wrap around
- ![[Pasted image 20241007202635.png]]
- ![[Pasted image 20241007202746.png]]
- 