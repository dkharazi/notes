---
title: "Building a Web Service"
draft: true
weight: "1"
katex: true
---

### Describing Sockets
- A socket is an endpoint of a connection between a client and a server
- An endpoint is defined by:
	- An address (IP address+port)
	How many connections it will backlog until it starts refusing new connections
	Other properties

### Describing the GIL
- Runs one process (and threads of a process) on a single CPU core
- Prioritizes CPU bound threads over I/O-bound threads
	- This contrasts how OS handles thread scheduling (OS prioritizes short-running tasks)

---

### tldr

---

### References
- [Building a Web Service from Scratch](https://www.youtube.com/watch?v=MCs5OvhV9S4)
- [Defining a Socket](https://stackoverflow.com/a/152863/12777044)
- [Python Cookbook](https://d.cxcore.net/Python/Python_Cookbook_3rd_Edition.pdf)
