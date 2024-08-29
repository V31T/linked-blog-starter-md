[[Python Django]]

### What is Django?
- web framework denoted as "with batteries included"
	- a bunch of included features like admin view and sqlite3 integration
- good because of Rapid Development and Database Flexibility
	- built in admin flexibility
	- extensive ecosystem
### Follows the Mode-View-Template
1. View
	1. Python function that receives requests and sends out the response after communicating with database through the model
2. Model (Database)
	1. connects to the database
3. Template
	1. User Interface
		1. includes dynamic tags
		2. uses django template language

How it works: 
![[Pasted image 20240813194329.png]]
- ORM: Object Relational Mapping
	- define database using python classes (models)
- View prepares data uses the template to send out an http response
	- renders the page to the user