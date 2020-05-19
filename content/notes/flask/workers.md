---
title: "Gunicorn Workers"
draft: true
weight: "1"
katex: true
---

### Benefit of Multithreading in Gunicorn
- Threads in Gunicorn are always real
- The GIL locks the interpreter while interpreting a CPython thread
- Consequently, CPython threads can't work simultaneously
- Therefore, the CPython threads executed in Gunicorn will suffer from this same problem
- However, this doesn't mean threading in general is useless
- Specifically, multiple threads can be used without locking
- In particular, multiple threads can be processed concurrently
- This is true for threads that don't require interpretation:
	- Threads that are I/O bound
	- Threads that use C extensions for interpretation

### Describing Workers in Gunicorn
- A Gunicorn worker is a process
- Gunicorn is based on the pre-fork worker model
- Pre-forking refers to a master creating a fork that handles each request
- A fork is a completely separate process
- The *pre* in pre-fork means that these processes are forked before a request comes in
- This model differs from a threading model
- Specifically, the master would create lighter weight threads to dispatch requests in a threading model
- However, this master process can have repercussions if a thread causes an error
- Gevent helps make these threads asynchronous
- Meaning, a process can handle hundreds of requests without any blocking

### Configuring the Number of Workers
- Generally, the number of workers $n$ should be set as the following:

$$ \text{number of threads} \times \text{number of workers} + 1 $$
$$ = 2n + 1 $$

- The intuition behind this formula is the following:
	- `+1:` One worker should be reserved to for scheduling
	- `2n:` While one thread is doing I/O and waiting, another thread can be using the CPU
- As an illustration, we can set the number of workers to be $2$:
```sh
$ gunicorn --workers=2 'test:create_app()'
```
- There is a trade-off between the following:
	- The overhead of the GIL (threads)
	- The memory overhead of starting new processes (workers)
- Meaning, we need to test which is better: threads or workers

### Configuring the Synchronicity of Workers
- https://github.com/benoitc/gunicorn/issues/1045#issuecomment-269575459

### Common Configurations of Workers
- Gunicorn Workers and Threads

---

### tldr
- Hello world

---

### References
- [Basics of Processes and Threading](https://learn-gevent-socketio.readthedocs.io/en/latest/general_concepts.html)
- [Defining a Pre-Fork Web Server Model](https://stackoverflow.com/a/25894770/12777044)
- [Gunicorn Threads](https://stackoverflow.com/a/48572328/12777044)
- [Gunicorn Workers and Threads](https://stackoverflow.com/a/41696500/12777044)
- [Web Servers and the GIL](https://stackoverflow.com/a/49938239/12777044)
- [Configuring the Number of Workers](https://github.com/benoitc/gunicorn/issues/1045#issuecomment-269575459)
- [Threading in Flask's Development-Only WSGI Server](https://stackoverflow.com/a/38876915/12777044)
- [Optimizing Gunicorn Configurations](https://medium.com/building-the-system/gunicorn-3-means-of-concurrency-efbb547674b7)
