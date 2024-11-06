matrix groups 

RMON probe: what is this?

open ssl commands will be provided

![[Pasted image 20241104204453.png]]

# RMON
basics-> a definition of a MIB, monitors network, can store packets for later analysis, can count or capture with Filters
goals -> monitors even while system is offfline to accumulate statistics, proactively monitors if the it has sufficient resources and is not considered disruptive. Active vs pasive recording
configuration -> dictates the type and form od data to be collected, divided into groups that has control tables (rw) and data tables (r). manager sets appropriate control parameters by adding a new row or by modifying an existing row in the contorl table, collected data is stored in the corresponding data table