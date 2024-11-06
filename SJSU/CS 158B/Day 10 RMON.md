
## NOTES
![[Pasted image 20240930194735.png]]
### RMON BASICS
- the entire focus, it is SNMP but for monitoring

### RMON GOALS
- effective and efficient way to monitor subnetwork-wide behavior while reducing the burden both on other agents and managers.
- goal it to increase monitoring without increasing load.
	- offline monitoring: monitor to continue accumulating statistics that may be retrieved by the manager at a later time. Monitor may also attempt to notify the manager if an exceptional event occurs.
		- exceptional event -> agent uses a trap to send message to monitor
	- proactive monitoring: if the monitor has sufficient resources and the process is not considered disruptive, then it can cont. run diagnostics and a log network performance.
- Overall can be ACTIVE or PASSIVE recording.
- VALUE ADDED DATA: the monitor can perform some analysis on the collected data before reporting to the manager.
	- 10 batches of data over 60 min, we can analyze (summary stats etc) to reduce the data and then send that data to the manager.

### Configuration
- monitor needs to be configured for data collection.
	- configuration dictates the type and form of data to be collected
- MIB is organized into multiple functional groups 
	- each group has: 
		- one or more control tables (usually read-write)
			- where the manager can control what data will be configured
		- one or more data tables (typically read-only)
			- the actual data, based off of managers instructions on what to collect
	- manger sets appropriate control parameters **by adding a new row or by modifying an existing row or by modifying an existing row in the control table**
		- -> data is stored in corresponding data table

### Collect Configuration
- functions to be performed by a monitor are defined and implemented in terms of table rows
	- a control table may contain objects that specify
		- source of data to be collected
		- type of data
		- collection timing etc.
- by assigning specific values to parameters (columnar objects) of the table, a single row of the control table defines a specific data collection function.
- each control row has one or more rows in the data tables
- each control row has a unique index object
	- each data row includes that control index like a foreign key\

### Modification and Deletion
- MODIFY
	- 1. invalidate the control row entry
		- effect: deletion of the control row and all associate rows in the data tables
	- 2. create a new control row with modified parameters
- DELETE
	- 1. invalidate the control row entry
		- effect: deletion of the control row and all associate rows in the data tables

### Combined Tables
- if control-row

### Action Invocation
- usually, SNMP offers read object values and set object values
- however in RMON, there are many "action objects"
	- ![[Pasted image 20240930200416.png]]

### Multiple Managers
![[Pasted image 20240930200432.png]]
- if u look at control table, yo can see which manager is controlling which agents and what is monitoring what
- another benefit: poggers

### Table Management
![[Pasted image 20240930200953.png]]

### Table Definition Example

### Row Creation State Machine
![[Pasted image 20240930202129.png]]
- dashed = agent
- solid line = manager

### RMON MIB
![[Pasted image 20240930202320.png]]
- is the 16th child of MIB-2
- hosts are biggest traffic producers
![[Pasted image 20240930202608.png]]

### statistic group
- combined control and data table
- eitherStatsIndex: integer for each row
- eitherStatsDataSource: same as `ifIndex` in MIB-LL interfaces group
![[Pasted image 20240930202712.png]]

### History group
![[Pasted image 20240930202953.png]]

### Host Group
![[Pasted image 20240930203316.png]]
