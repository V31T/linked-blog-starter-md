[[Python Django]]

[YT Link](https://www.youtube.com/watch?v=qQPKqClSDbg&list=PL4cUxeGkcC9iqfAag3a_BKEX1N43uJutw&index=9)

General Notes:
- done within MigrateSQLite3 Folder

Notes: 
-  ipython
	- its cools because you can kinda run anything in it
		- unix commands
		- java
		- sql commands
		- magic functions
			- %time sum(range(10000))
				- applies %time on sum function
	- important because django shell is just ipython
		- allows to manage/interact database
	- exit command ctrl + d
- **troubleshooting**
	- ipython was not the default interpreter for manage.py shell
	- had to deal with virtualenv shell
		- had to install ipython into the virtual environment even though i have it installed globally already
		- make sure to select the correct python interpreter with the vscode fuzzzy find
		- and yeah
- python manage.py shell -i ipython
	- ![[Pasted image 20240815175416.png]]
		- to1 output does not tell us much
			- must use str method to get better string representation of to1
		- self refers to the object the function is being called on![[Pasted image 20240815175649.png]]
		- must restart shell for changes to take place
		- ![[Pasted image 20240815222054.png]]
			- saves changes to database
		- ![[Pasted image 20240815223029.png]]
			- NOTE: to1 has an ID because we saved it into the database (i accidently saved it twice lmfao)
				- to2 has note been saved into the db, tf it does not have an id
- ![[Pasted image 20240821142502.png]]
