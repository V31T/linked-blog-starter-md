## RMON AND RMON 2
- what is a mib? an agent-manager communication. when adding new agent, manager doesn't know how to talk to new agent.
- stores packets
- functional groups
	- data tables and control tables
		- Functions to be performed by a monitor are defined and implemneted in terms of table rows
	- Config dictates the ttype and form of data to be collected
		- sets control params by adding a new row
	- can modify/delete control rows
	- IF CONTROL-ROW IS 1:1; THEN THE TABLES CAN BE COMBINSED SO THAT A SINGLE ROW ODATA CAN HOLD HBOTH CONTROL objects and data objects
- "action" objects
	- represents states in the agent
	- if state changes then an action is performed
	- Race-condition if multiple managers, can cause excessive load on the agent
		- Solution: cooperative mechanism
			- each control table a has a columnar object that identies the owner (i.e. ip address, manger name, location, etc.)
- every control table has:
	- OwnerString object to indicate owner of that row
	- EntryStatus object to indicate the current status in the entry management life-cycle
- Table example: 
	- **![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe5Zi8IsjjAohZDVoZOz-CBJx6k_SEbK7o62oN4A7wt3V8Mhm0cuJQwcn6OcvBP_f_lBNCEcEI4jtUEDsLJAd-I4eGLgIBAtSaYbWD8ZOEcOhapJSD11SN797cXRlxmZJWZPWX1APmGGz_v4Keo_4nk9jne?key=0KCUZw2UR7sJeuu1ksocZiZS)**
	- Control Index - Integer, is the foreign key in Data table
	- if manager attempts to create a new row, and the index object value does not exist, then the row is created with status = **createRequest**
	- Immediately after completing the create operation, the agent sets the status object value to **underCreation**
- RMON MIB
	- host: contains COUNTERS for various types of traffic to and from hosts attached to the subnetwork 
	- hostTopN: contains sorted host stats that report on the hosts at the top of a list that is based on some parameter in the host table
	- **![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcx6yVA1iwILJC9EPI1eTxdWX488lNd56AVDBwj_09XDCv93Deo4ZE2Qrn5U465bmV-pXpIkEufRz2g3rNubus3XB_XpAKYUjucTSkxZMupBuUjvorD388qHLGqI5UuEX8wljPsknOJET2sRABdfsWtV_PY?key=0KCUZw2UR7sJeuu1ksocZiZS)**
	- stats group
		- combined control and data table
		- eitherStatsIndex: index for each row
		- etherStatsDatSource: same as Ifindex in MIB-2 interfaces group
	- history group:
		- BucketsRequested - number of smapling intervals requested default =50
		- BucketsGranted - number of sampling intervals that will be saved
		- ControlInterval - Sampling Interval
		- REMEMBER: these are functional groups with control tables and a corresponding data table
		- Example: Sample once every 1800 seconds and save the most recent 50 rows in etherHistoryTable
	- Host group
		- ControlLastDeleteTime - last time (sysUpTime) an entry was deleted from hostTable (default 0)
		- hostTable - for each interface specified by a row in hostControltbale, the hostTable contains one row for each MACaddress discovered on that interface 
		- indexed by hostAddress
		- EXAMPLE: find the 5 hosts that sent most packets in the next 1 minute
			- you would use hostTable since it keeps tack of packet counts, 
			- hostTopNRate - amount of change in the selected variable during this sampling interval 
			- selected var is specified in TopNRateBase
			- CREATED REPORT IS READ ONLY
- MATRIX
	- Situation: There are N hosts in a subnetwork, say h1, h2, ..hN
	- 1. how many packets are exchanged between the hosts hi and hj
		- locate entries for `matrixSDPkts.[h_i].[h_j]` and `matricxDSPkts.[h_j}/[h_i]`
		- summing both values gives total packets exchanged
		- remember those locations, will be used a lot
- MATRIX TABLE IN RMON
	- table is designed to track detailed pair-wise communication data, allowing for fine-grained packet counts both for specific host pairs and groups of sending/receiving hosts
- Matrix Group
	- matrixSDTable and matrixDSTable have the same content except the index is different
		- Index = (SourceAddress, DestAddress) opposite for DSTable
	- rows: matrixSDPkts , Octets, Errors
	- • The matrixSDTable contains two rows for every pair of hosts on that subnetwork that have recently exchange packets
		• One row, e.g., from hi to hj
		• One row, e.g., from hj to hi

Alarm Group
- defines a set of thresholds for network performance 
- Single Table: alarmTable
	- alarmVaraible: OID of the particular variable in the RMON MIB to be sampled, must be INTEGER, coutner, gauge, or TimeTicks
	- REMEMBER: every table has an index im just not including it in these notes

Tresholds
- rising: crossed if the current smapled value is greater than or equal to the rising threshold and the value at the last sampling intervale was less than the threshold
- Falling: same idea but if current sample is less than falling treshhold and the last sample was greater than it

Sample Types
- absoluteValue: value of the statistic is compared directly to the the thresholds
- deltaValue: value of last sample subtracted from current value, represents the difference over two successive sampling periods
	- problems:
		- repeated minor alarms 
			- for a rising/falling alarm to repeat in an interval, the metric must pass the falling/rising metric
			- i.e. if rising is triggered, cannot trigger another rising until a falling is triggers
		- something
			- itnerval = 10 seconds
			- rising threshold = 20
			- time(10).deltaValue = 19 -> time(15).deltaValue =  13 -> 19+13 = 32 > threshold but no alarm is triggered
				- solution: delta sample must be taken twice per period, each time comparing the sum of the latest two samples to threshold 
					- basically take sample every 5 seconds and compare within that interval (intervals are set to 10 seonds)

## RMON 2
- RMON is for Layer-2
- can analyze traffic through a router, and has visibility into Layer 3 and above
	- meaning has access to ip addresses and ip packets
		- can analyze transit traffic through a route
- addressMap: matches IP address to MAC address
- Time Based Indexing
	- TimeFilter Object
		- is basically a time counter used as an index for the table
- fooTable
- Manager -> Agent Getrequest (foocCoutntts,7.1, fooCounts.7.2)
	- i.e. provides values for timestamp >= 7 for fooIndex = 1,2
- Agent -> Manager GetResponse(fooCounts.7.2 = 9)
	- only returns 1 value because fooCounts.7.1 = 5 which is NOT greate than 7
- problem ^ manager does not know the timestamps, to get around this you must ask for the timestamps and then use it in the next getRequest

## Prometheus 