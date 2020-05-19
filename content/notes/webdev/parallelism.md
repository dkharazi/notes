---
title: "Introducing Parallelism"
draft: true
weight: "3"
katex: true
---

### Introducing Concurrency and Parallelism
- Concurrency refers to the state of two or more threads performing at the same time
- Parallelism refers to the state of two or more threads executing at the same time
- In other words, concurrency allows one thread being paused while another is being executed
- On the other hand, parallelism requires both threads to be executed at the same time
- In python, threads are associated with concurrency, whereas processes are associated with concurrency and parallelism

### Describing Concurrency and Parallelism
- Concurrency is a condition that exists when two threads are making progress during a period of time on a system
- Parallelism is a condition that exists when two threads are executing simultaneously during a particular point in time on a system
- Concurrency is a property of a program or system
- Parallelism is a property of the run-time behavior of executing multiple tasks at the same time
- The following are examples of concurrency:
	- Executing two threads on a single non-hyperthreaded CPU core
	- Time-Slicing by the operating system
	- Loading multiple documents simultaneously while opening new browser tabs
- The following are examples of parallelism:
	- Executing two threads on a single hyperthreaded CPU core
	- Simultaneously executing two different threads on a multicore processor
	- Simultaneously executing two different processes on a multicore processor
	- Graphic computations on a GPU

### Describing Multithreading and Concurrency
- At the hardware level, a CPU can execute threads in parallel for:
	- Hyperthreaded processors
	- Multicore processors
- A CPU core only appears to run threads from a multithreaded program in parallel
- However, a CPU core doesn't truly run threads from a multithreaded program in parallel
- This is because the operating system is very efficient at time-slicing (i.e. scheduling) threads by default
- Specifically, each thread gets a few milliseconds to execute before the OS schedules another thread to run on that same CPU core
- For example, let's say we have the following:
	- A java program with 4 threads
	- A computer with 4 CPU cores
- Most likely, those 4 java threads truly will run in parallel on 4 separate cores
- In this situation, we're assuming those 4 cpu cores are idle beforehand

---

### tldr
- Concurrency refers to the state of two or more threads performing at the same time
- Parallelism refers to the state of two or more threads executing at the same time
- At the hardware level, a CPU can execute threads in parallel for:
	- Hyperthreaded processors
	- Multicore processors
- A CPU core only appears to run threads from a multithreaded program in parallel
- However, a CPU core doesn't truly run threads from a multithreaded program in parallel
- This is because the operating system is very efficient at time-slicing (i.e. scheduling) threads by default
- Specifically, each thread gets a few milliseconds to execute before the OS schedules another thread to run on that same CPU core

---

### References
- [Concurrency and Parallelism in Python](https://medium.com/building-the-system/gunicorn-3-means-of-concurrency-efbb547674b7)
- [Haskell Wiki on Concurrency and Parallelism](https://wiki.haskell.org/Parallelism_vs._Concurrency)
- [Concurrency and Parallelism in Java](http://tutorials.jenkov.com/java-concurrency/concurrency-vs-parallelism.html#concurrency-vs-parallelism)
- [Parallelism with Hardware Threads](https://stackoverflow.com/a/5593432)
