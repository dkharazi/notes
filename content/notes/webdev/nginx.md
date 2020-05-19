---
title: "Web Servers"
draft: true
weight: "18"
katex: true
---

### Defining a Web Server
- A web server refers to software that handles client requests
- This software lives on a physical server
- Specifically, a web server serves clients with files stored on a server
- Typically, these files are html, css, and some javascript scripts
- In other words, a web server usually serves static files to the client
- These static files include images, videos, forms, etc.
- Communication between the web server and its client must take the form of HTTP messages

### Describing the Functions of a Web Server
- A web server can be used for the following functions:
	- A reverse proxy
	- A load balancer
	- A mail proxy
	- An HTTP cache
- A reverse proxy refers to returning resources from a server on behalf of a client
- A load balancer refers to a reverse proxy distributed across separate servers
- There is a lot of overlap between these functions
- Therefore, web servers attempt to provide these functions in a centralized service
- Nginx is a popular web service that achieves this goal

### Motivating the Benefits of Nginx
- Offers low memory usage
- Offers high concurrency
- Supports asynchronous events
	- Each request is handled in a single thread
- Reverse proxies with caching
	- Local copies of web resources are stored
	- Caching resources leads to faster retrieval for future requests

---

### tldr
- A web server serves clients with files stored on a server
- Communication between the web server and its client must take the form of HTTP messages
- A web server can be used for the following functions:
	- A reverse proxy
	- A load balancer
	- A mail proxy
	- An HTTP cache

---

### References
- [Difference between Web and Application Servers](https://stackoverflow.com/a/35360821/12777044)
- [How Web and Application Servers Work Together](https://www.nginx.com/resources/glossary/application-server-vs-web-server/)
- [Using WSGI Frameworks with Web Servers](https://stackoverflow.com/a/12798019/12777044)
- [Setting up WSGI Servers with Web Servers](https://stackoverflow.com/a/8691337/12777044)
- [What is Nginx?](https://kinsta.com/knowledgebase/what-is-nginx/)
- [Examples of Nginx Configurations](https://www.nginx.com/resources/wiki/start/topics/examples/full/)
- [Rate Limiting with Nginx](https://www.nginx.com/blog/rate-limiting-nginx/)
