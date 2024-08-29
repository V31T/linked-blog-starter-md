[[Python Django]]

[YT LINK](https://www.youtube.com/watch?v=DZVFgMSyRXI&list=PL4cUxeGkcC9iqfAag3a_BKEX1N43uJutw&index=10)

Notes:
- same setup as before
- using Model.py
	- create classes
	- ORM same idea as Java SpringBoot
- mirgrations
	- a way of propagating changes
	- how
		- first ensure settings.py has application name
		- ![[Pasted image 20240815122621.png]]
			- creates model Tour
				- 0001_initial.py
					- contains migrations and models imported from django.db
					- operations
						- list of createmodel functions
							- currently a tour with all of the attributes
						- database schema
		- must apply migrations
			- ![[Pasted image 20240815155422.png]]
			- What happened: Django applied all migrations to the database and establishes the new table in the database
- Note: default database is sqlite3
	- located in settings.py in list `DATABASES`
	- migrations creates the table in the listed database
	- can easily change the database to any other dbms
- next: 
	- how to interact with database

