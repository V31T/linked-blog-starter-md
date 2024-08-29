[[Python Django]]

General Notes:
- some html tags do not have void/closing tags because they do not have any content within them
	- duh
Notes:
- we will be building our own form authentication system
	- using django.contrib.auth modules
	- how to allow users to create accounts and securely logging user account
	- how to protect pages where only authenticated users can gain access
- Create project and app
	- note: auth and contenttypes are already included in installed apps
	- first must create user registration as form.py
		- ![[Pasted image 20240818170732.png]]
			- important to allow user to register username and password and stuff
		- ![[Pasted image 20240818171116.png]]
			- defines meta data
	- python decorators
		- special functions that modify the behavior of other functions
			- usually to add functionality without changing the original function's code
	- mixins
		- reusable classes that add specific classes that add additional functionality to class based views without being the primary parent class
	