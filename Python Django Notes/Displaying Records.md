[[Python Django]]

[YT LINK](https://www.youtube.com/watch?v=RozHfswVZYE&list=PL4cUxeGkcC9iqfAag3a_BKEX1N43uJutw&index=8)

General Notes:

Notes:
-  asiatours
	- views.py
		- dont like httpresponce to render a string
		- use render function instead
			- purpose to render html on the page
			- store html in templates folder
		- use django template language 
			- very similar to jinja2 in flask
	- NOTE: make sure you add a urls.py to new applications
	- how do we display  interactive data on a static html page?
		- using a context variable that stores tour data in a dictionary![[Pasted image 20240815235516.png]]
		- ![[Pasted image 20240816001802.png]]
			- example of django template language 
				- uses {} and %
		- very easy to update date in django super cool
			- you can add and update databases on the fly and can have changes reflected on the front end