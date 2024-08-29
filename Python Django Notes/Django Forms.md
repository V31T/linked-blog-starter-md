[[Python Django]]

[YT Link](https://www.youtube.com/watch?v=WQISlkg_IZk&list=PL4cUxeGkcC9iqfAag3a_BKEX1N43uJutw&index=5)

[Documentation](https://docs.djangoproject.com/en/5.0/topics/forms/)

General Notes:

Notes:
- Django Forms
	- essential for any interactive web application
	- libraries to create, handle, and process forms
	- 1. Validation
	- 2. Security {% csrf tokens %}
	- 3. Reuse 
	- 4. Customization
- Forms Documentation
	- Forms are essential for interactivity
	- HTML Forms
		- must know: 
			- structure
				- collection of elements in a form tag `<form></form>`
			- elements
				- text inputs, checkboxes, day pickers etc
			- attributes
				- must specify target url (action attribution), and http method (GET POST UPDATE PUT)
	- django simplifies the process
		- data handling/rendering
		- creating html forms
		- handling and validating data
- Workflow when Creating Views, URLS, and more in Django
	- create your project (add app to project settings and create app's url.py)
		- include STATIC FILES_DIRS in proj settings.py
		- include path in proj urls.py
	- Workflow
		- plan and create views in views.py
		- add views to urls.py
		- create necessary files
		- static folder
			- contains images js and css
		- templates/app_name
			- html files
				- include {% load static %} at top
		- normal html css and js setup
	- {% csrf_token %}
		- cross site request forgery 
	- form.as_p