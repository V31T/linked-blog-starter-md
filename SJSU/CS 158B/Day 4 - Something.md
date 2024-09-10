
![[Pasted image 20240909193522.png]]
![[Pasted image 20240909193551.png]]
## SNMP Messages
- **GET-REQUEST**: Manager requests the value of a Managed Object 
- **GET-NEXT-REQUEST**: Manager requests the value of the next Managed Object
- **GET-BULK**: Manger requests large data
- **SET-Request**: Manager requests to update the value of one or more Managed Object
- **GET-RESPONSE**: Agent responds to the above requests
- **TRAP**: Agent notifies voluntarily manager about a Managed Object

## SNMP and TCP/IP stack
- SNMP is an application-level protocol
- "" uses UDP
- "" Agents listen to port 161 for requests from Manager
- "" Managers listen to port 162 for traps from Agent
- Weakness: there are no confirmation of messages

