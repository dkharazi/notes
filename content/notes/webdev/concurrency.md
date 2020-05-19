---
title: "Concurrency"
draft: true
weight: "15"
katex: true
---

### Summarizing the State of Multithreading in Python
- As a reminder, two threads can run concurrently per core
- Only one thread truly can run at once per non-hyperthreaded core
- Two threads truly can run at once per hyperthreaded core
- The following applies to CPython:
	- Only one CPU-bound thread can run at once per process
	- Multiple I/O-bound threads can run at once per process
- Essentially, CPython allows multithreading for I/O bound threads
- This is a consequence of the GIL in CPython
	- The lock is used because CPython's memory management is not threadsafe
- Therefore, we generally should apply the following logic:
	- Use multithreading for I/O bound threads
	- Use multiprocessing for CPU bound threads
- As a result, we'll achieve the following:
	- Lightweight I/O bound threads that are concurrent
	- Heavyweight CPU bound processes that run in parallel

### Motivating Multitasking in Python
- The way threads or tasks take turns is the big difference between `threading` and `asyncio`
- The `threading` package involves *pre-emptive multitasking*
- Pre-emptive multitasking allows the OS to more reliably guarantee each process a regular slice of CPU time
	- The operating system actually knows about each thread
	- Therefore, the OS can interrupt a thread from processing at any time to start running a different thread
	- Things become simple when threads can switch at any time
	- Specifically, a thread doesn't need to do anything for a check
	- However, that means the switch can happen in the middle of a single Python statement, even a trivial one like $x=x+1$
- The `asyncio` package uses *cooperative multitasking*
- Cooperative multitasking ensures that tasks cooperate by announcing when they are ready to be switched out
	- Meaning, the code in the task has to change slightly
	- The benefit of doing this extra work is that we'll always know where a task will be swapped out
	- It will not be swapped out in the middle of a Python statement unless that statement is marked

| Concurrency Type         | Python Package    | Switching Decision                                             | Number of Processors |
| ------------------------ | ----------------- | -------------------------------------------------------------- | -------------------- |
| Pre-emptive multitasking | `threading`       | The OS decides when to switch tasks (external to Python)       | $1$                  |
| Cooperative multitasking | `asyncio`         | The tasks decide when to give up control (internal to Pythion) | $1$                  |
| Multiprocessing          | `multiprocessing` | The processes all run at the same time on different processors | Many                 |

### When is Concurrency Useful?
- Concurrency can help solve two types of problems:
	- CPU bound operations
	- I/O bound operations
- Improving performance of I/O bound processes involves finding ways to overlap the times spent waiting for these devices
- Improving performance of CPU bound processes involves finding ways to do more computations in the same amount of time
- Certain types of concurrency are better for CPU bound operations
- Other types of concurrency work better for I/O bound operations

### Option 1: Multithreading using ThreadPoolExecutor
- A `Pool` is a collection of threads (from the same process) that can run concurrently
- An `Executor` controls how and when each thread (in its Pool) will run
- A `ThreadPoolExecuter` manages how threads in a pool will be executed concurrently

### Option 2: Event Loop using Asyncio

---

### tldr

---

### References
- [Python's Definition of the GIL](https://wiki.python.org/moin/GlobalInterpreterLock)
- [Applications of Improving Performance with Concurrency](https://realpython.com/python-concurrency/)
- [Details about the Event Loop](https://stackoverflow.com/a/46375948/12777044)
- [Details about Concurrency](https://learn-gevent-socketio.readthedocs.io/en/latest/general_concepts.html)
