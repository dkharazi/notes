---
title: "Web Servers"
draft: true
weight: "2"
katex: true
---

### Defining a Web Server
- A web server is a server that runs software
- Specifically, this software handles client requests
- It serves clients with files stored on its server
- Typically, these files are:
	- HTML files
	- CSS files
	- Some JavaScript files
- In other words, it usually serves static files to the client
- These static files include images, videos, forms, etc.
- Communication between the web server and its client must take the form of HTTP messages

### Describing the Functions of a Web Server
- A web server can be used for the following functions:
	- An **HTTP cache**
	- A **mail proxy**
	- A **reverse proxy**
	- A **load balancer**
- A reverse proxy is a server sending resources to a client
- It fulfills the following functions:
	- Accepts a request from a client
	- Forwards that request to a server that can fulfill it
	- Returns the server's response to the client
- A load balancer is a server that distributes network traffic across multiple servers
	- A load balancer is a reverse proxy
- There is a lot of overlap between these functions
- Therefore, web servers attempt to provide these functions in a centralized service
- Nginx is a popular web service that achieves this goal

### Defining an Application Server
- An application server is a server that runs software
- Specifically, this software serves files generated on the fly
- Some examples of this software are:
	- Gunicorn (Python)
	- Unicorn (Ruby)
- Web servers achieve the functionality of application servers
- However, they can remove load from the web server

### References
- [Difference between Web Servers and Application Servers](https://stackoverflow.com/a/35360821/12777044)
- [How Web and Application Servers work Together](https://www.nginx.com/resources/glossary/application-server-vs-web-server/)
- [Using WSGI Frameworks with Web Servers](https://stackoverflow.com/a/12798019/12777044)
- [Setting up WSGI Servers with Web Servers](https://stackoverflow.com/a/8691337/12777044)
- [What is Nginx?](https://kinsta.com/knowledgebase/what-is-nginx/)
- [Examples of Nginx Configurations](https://www.nginx.com/resources/wiki/start/topics/examples/full/)
- [Rate Limiting with Nginx](https://www.nginx.com/blog/rate-limiting-nginx/)
