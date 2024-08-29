[[Python Django]]

Notes:
- Using Bootstrap5 and django-crispy-forms and crispy-bootstrap5
	- cripsy-forms follows DRY principles
	- `pipenv install django-crispy-forms`
	- `pipenv install crispy-bootstrap5`
		- extension of crispy forms that focuses on implementing bootstrap styling
- settings.py
	- add app, crispy_forms, crispy_bootstrap5
	- ![[Pasted image 20240819010303.png]]
- A Docker _image_ is a read-only template that describes how to create a Docker _container_. The image is the instructions, while the container is the actual running instance of an image. To continue our apartment analogy from earlier in the chapter, an image is the blueprint or set of plans for building an apartment; the container is the actual, fully built building.
- context notes
	- https://clouddevs.com/django/use-context-in-templates/#:~:text=The%20Django%20context%20is%20essentially,or%20any%20other%20data%20source.
- makemigrations and migrate will tell you if there is any errors within your server
- Frontend Design
	- if pages have common assets you can use a base.html file that will serve as a template
	- Django allows you to create this base layout
	- layout.html will contain elements that will be consistent across pages
		- uses placeholders called `BLOCKS`
		- files that use the layout will extend layout
	- layout.html
		- using bootstrap5 and jquery for styling