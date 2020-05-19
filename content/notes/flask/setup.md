1. http requests
2. Jinj2 -- templating language
3. quickstart
	- a flask app is a wsgi app
	- gunicorn is a wsgi server
	- a wsgi server runs a wsgi app
	- __name__ specified so Flask knows where to look for templates
	- routing -- tells flask what URL should trigger our function
	- templating -- render templates using render_template()
	- url building -- url_build()
	- requests
		- a route only answers to an HTTP request
		- by default, a route only answers to GET requests
		- Can also answer to other HTTP requests with *method* argument
	- redirects/errors 
	- Response object
		- all return values are converted into a response object 
		- receive return values using make_response()
		- returning a dict will convert to json (jsonify() creates json)
	- session proxy -- store information specific to a user from one request to the next
	- contexts -- global objects and local contexts
4. Notes about Request contexts from Video
	- Flask does the following steps:
		- Flask receives an HTTP request from the WSGI server
		- Flask assigns the HTTP request to a Request object
		- Then assigns that Request object to a RequestContext
	- A request context is manually created in two ways:
		- with app.request_context(environ)
			- see PEP3333
			- manually create a real request context
			- too difficult and unnecessary
		- with app.test_request_context('/')
			- manually create an artificial request context
			- not for production
	- A session is basically a view of the session cookies stored in the request context
	- A session is a dictionary
5. Notes about Application contexts from Video:
	- The app variable (from app=Flask(__name__)) is assigned to current_app
	- Flask needs the environment dictionary to create a request context
		- The environment dictionary has all the client data and is taken from the browser
	- Flask needs an app variable to create an application context
	- The environment dictionary is received once the app variable is created
	- Meaning, the application and request contexts are both created at the same time
	- The steps are the following:
		1. Application context is created when app variable assigned
		2. Request context is then created when getting environ dict
		3. View functions are invoked, along with access to objects such as g, current_app, request, and session
6. Summarizing Request Contexts
	- There is a stack that manages request contexts
	- This stack is referred to as the request context stack
		- In the code, this is _request_ctx_stack
	- Each element in the stack is a single request context
		- In the code, this is a RequestContext class
	- Each request context is essentially a list of two objects:
		- A single request object
			- In the code, this is a Request class
		- A single session object
			- In the code, this is a Session class
	- A request proxy refers to the request object within the request context at the top of the stack of request contexts
	- A session proxy refers to the session object within the request context at the top of the stack of request contexts
	- Each thread will have its own request context stack
	- Notes from https://flask.palletsprojects.com/en/1.1.x/reqcontext/
7. Summarizing Application Contexts
	- There is a stack that manages application contexts
	- This stack is referred to as the application context stack
		- In the code, this is _app_ctx_stack
	- Each element in the stack is a single application context
		- In the code, this is an AppContext class
	- Each application context is essentially a list of two objects:
		- A single g object
		- A single current_app object
	- A g proxy refers to the g object
	- A current_app proxy refers to the application object
9. Application Setup
10. Database (https://flask.palletsprojects.com/en/1.1.x/tutorial/views/)
11. Blueprints and Views (https://flask.palletsprojects.com/en/1.1.x/tutorial/views/)
12. Templates (https://flask.palletsprojects.com/en/1.1.x/tutorial/views/)
13. Static Files (https://flask.palletsprojects.com/en/1.1.x/tutorial/views/)
14. config?, signals?

## References
- https://www.youtube.com/watch?v=Z4X5Oddhcc8&feature=emb_title
- https://flask.palletsprojects.com/en/1.1.x/
- https://flask.palletsprojects.com/en/1.1.x/reqcontext/
- https://flask.palletsprojects.com/en/1.1.x/appcontext/
- https://stackoverflow.com/questions/30514749/what-is-the-g-object-in-this-flask-code
- https://www.python.org/dev/peps/pep-3333/#environ-variables
- https://werkzeug.palletsprojects.com/en/1.0.x/local/
- https://stackoverflow.com/questions/20036520/what-is-the-purpose-of-flasks-context-stacks
