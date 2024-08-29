---
tags:
  - CS131
  - SJSU
---

- FIle descriptor information
	- point is to see where stdout/stderr
	- every file has 3 descriptors
	- you can access ALL stdout/stderr from a directory
		- but this sucks
		- instead run /proc/PID/dr is stdout
			- the same for other descriptors
- command shortcuts
	ls -f
		—f will add a trailing / at the end
- FILE PERMISSIONS
	- cd mod : changes file permisions
		- 4 2 1
		  R W X
		- chmod 764 <file>
			- a group that can do alll, a group that can only read write, and group that can only read

PWD 
- mnt = mount
- scratch = temp folder, runs processes faster but doesnt get backed up