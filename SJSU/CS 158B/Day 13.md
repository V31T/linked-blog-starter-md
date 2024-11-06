### PROJECT OVERVIEW
- it is just prometheus implementation
- project material will not be on the midterm
- ABLE TO DO IN A DAY?

## NOTES - PROMETHEUS
- Counter 
- Gauge
- Summary
- Histogram

### Summary
![[Pasted image 20241009193555.png]]
- to use prometheus metrics, must import prometheus_client
- OUTPUT:
	- ![[Pasted image 20241009193850.png]]

### Histogram
![[Pasted image 20241009194015.png]]
- output:
	- ![[Pasted image 20241009194237.png]]
	- ![[Pasted image 20241009194618.png]]

### Node Exporter
![[Pasted image 20241009194744.png]]
- CPU Collector
	- ![[Pasted image 20241009194820.png]]
- Filesystem Collector
	- ![[Pasted image 20241009195043.png]]
- Diskstats Collector
	- ![[Pasted image 20241009195200.png]]
- File based Service Discovery
	- ![[Pasted image 20241009195927.png]]
- HTTP based Service Discovery
	- ![[Pasted image 20241009195939.png]]
- Consul based Service Discovery
- EC2 based Service Discovery
	- (elastic compute)
	- ![[Pasted image 20241009200146.png]]