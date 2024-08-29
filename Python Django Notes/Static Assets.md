[[Python Django]]

[YT LINK](https://www.youtube.com/watch?v=kJJx77PYMFA&list=PL4cUxeGkcC9iqfAag3a_BKEX1N43uJutw&index=7)

General Notes:

Notes:
- Serve and Rendering Static Assets (styles images and JS)
	- CSS defines the layout and styles of your pages content
	- JS provides interactive and dynamic behaviors like animations
	- why static files matter
		- consistency
		- performance: improve load time through static assets
		- interactivity: javascript is okay
- Django's approach to static file
	- Static Files Storage
		- `STATICFILES_DIRS` in settings.py
			- to specify where static files live
		- Templates and URL tagging
			- i.e. {% load static %}
	- ![[Pasted image 20240817112812.png]]
		- `from pathlib import Path`
			- turns paths into objects so you can work with them
		- sets BASE_DIR to the path of the current file
			- Path(__ file __ )
				- denotes the non-absolute path of the current working file
			- .resolve()
				- converts to absolute path
				- C:\\Users\\Henry Pham\\VSCode\\Django-learning\\StaticAssets\\django_project\\django_project
			- .parent.parent
				- so path of file is 2 parents up
				- C:\\Users\\Henry Pham\\VSCode\\Django-learning\\StaticAssets\\
	- ![[Pasted image 20240817113534.png]]
		- base url for serving all static files
	- ![[Pasted image 20240817113556.png]]
		- contains anything uploaded by users
	- ![[Pasted image 20240817113613.png]]
		- defines path to additional directories where django will look for additional files
			- combines current path with BASE_DIR to help keep folders/files organized within
- Normal Django App setup
	- views.py
		- `def index(request): return render(request, "django_app/index.html)`
	- urls.py
		- setups url for webpage
		- `from django urls import path`
		- `from .views import index`
		- `urlpatterns = [path('', index, name = "index"),]`
			- DO NOT FORGET THE COMMA
	- go project url.py
		- include in urlpatterns
			- `path('', include(django_app.urls))`
- Front end setup
	- index.html
		- before loading doc
			- `{% load static %}`
				- MUST BE THE FIRST LINE
		- link style
			-  css 
				- `href = "{% static 'styles/styles.css' %}"`
			- js
				- `src = "{% static 'js/scripts.js' %}"`
			- images
				- `src = "{% static 'images/... %}" alt = Django Logo`
					- include file name
- review all of this and write all of it down
- There was a lot to talk about
	- start vid at 5:00
- 