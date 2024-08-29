[[Python Django]]

Link: [Django Ep#2](https://www.youtube.com/watch?v=aAACOgAHg90)

General Notes:
-  I hate windows so much I wish I had a linux desktop but alas, I enjoying playing video games too much

Notes:
- virtual environments
	- pip install pipenv
	- py -m pipenv shell (this works rather than pipenv shell idk why, maybe its cause we r not directly in a python executable)
		- make sure to switch to python interpreter
		- py -m pipenv install Django
			- GETTING THIS TO WORK WAS A BITCH
				- first pip wasnt working -> had to uninstall python and flush out everything, figure out where all my packages were being installed and yeah
				- I can now understand the appeal to pipenv, it makes all projects seperate so easily
				- dont have to make a new .venv for each project
				- very pog
			- resource on why pipenv is just better and how to use it
				- [Link](https://realpython.com/pipenv-guide/)
		- ![[Pasted image 20240813235320.png]]
	- pip freeze lists all modules install in the project
-  django commands
	- django-admin startproject myproject
		-  startproject is the subcommand, myproject is the name of the new project
- Django initial project file overview
	- __init.py__ 
		- usually empty
	- _asgi.py_
		- asyncronous server gateway
		- bridge between django and asyncronous features
			- long live
			- allows live interactions
			- tech that enables django to stay responsive and handle multiple requests
	- settings.py
		- contains all configs
		- secret key: dont share shit
		- debug key: default true
	- installed_apps
	- Databases: default sqlite3
		- can easily change it to anything
	- static
		- images,css,embedded javascript
	- urls.py
		- maps urls to view functions/classes
			- users -> views -> model
		- urlpatterns:
			- has multiple different paths depending on where the user can visit
	- wsgi.py
		- serves as entrypoint for wsgi stuff
	- manage.py
		- command line utility
		- provides various commands for performing commands
			- creating tables
			- creating superusers
			- run tests
			- wrapper around django admin tasks
- Running the framework
	- ![[Pasted image 20240814001336.png]]