---
title: "Multithreading"
draft: true
weight: "2"
katex: true
---

### Defining Multithreading
- The idea of a programming language supporting the ability for us to program and manage our own threads is called *multithreading*
- Java and C++ are some examples of programming languages that support multithreading
- Python does not support multithreading
- Typically, the purpose of a multithreaded program is to execute our code in parallel
- Therefore, multithreading is limited by our hardware capabilities, since our hardware is what provides us with the capability of processing threads in parallel
- If we only have one CPU with one core, then multithreading will not achieve anything
- If we have multiple CPU cores, then multithreading will achieve parallelism
- Multithreading is a programming paradigm, whereas hyperthreading is a hardware capability

### Describing the Components of Multithreading
- There are only two ways to run threads in parallel:
	1. Ensuring our CPU core is hyperthreaded
	2. Adding CPU cores to our system
		- We can do this by adding more CPU cores to a single CPU
			- **i.e.** multicore processor
		- Or by adding more CPUs to our system
			- **i.e.** multiprocessor
- The operating system schedules each thread to be executed on a particular CPU core
	- The operating system is very efficient at scheduling these threads
	- It slices each thread in chunks in an attempt to fairly distribute CPU execution time across threads waiting to be finished executing
- Let's say we're writing a program in some programming language
- Then, that program will default to creating one process with one thread when that program is executed
- However, certain programming languages allow us to manually program and manage our own threads
	- Scheduling is still done by the operating system
	- However, we're able to organize code into individual threads
	- Then, we can tell our program what to do with those threads once they're executed

### Multithreading in Python
- The default implementation of Python is CPython
- Python offers multithreading
- In fact, Python uses system threads
- However, CPython  can't use more than one of the available cores
- This is due to something called the Global Interpreter Lock (GIL)
- Python threads still work for I/O bound tasks as opposed to CPU bound tasks
- Specifically, CPU bound tasks can cause deadlocks and race conditions
- Many Python libraries solve this issue by using C extensions to bypass the GIL

### Multithreading Specifics about the GIL
- In order to make the dynamic memory management in CPython work correctly, then the GIL prevents multiple threads from running CPython code at the same time
- This is because CPython's dynamic memory management is not threadsafe
- Specifically, it can have deadlocks and race conditions when multiple threads access the same resources at the same time
- The GIL was a compromise between the two extremes of not allowing multithreaded code, and having the dynamic memory management be very bulky and slow
- Other implementations don't have a GIL
- Some of these implementations include the following:
	- Jython
	- PyPy
	- Cython
- This is because the platforms they are build on (i.e. Java and C) handle dynamic memory management differently

### Illustrating Scenarios with Multithreading
- A single non-hyperthreaded CPU core can execute one single-threaded process at once
- A single hyperthreaded CPU core can execute two single-threaded processes at once
- A single hyperthreaded CPU core can execute one double-threaded process at once
- Two non-hyperthreaded CPU cores can execute two single-threaded processes at once
- Two non-hyperthreaded CPU cores can execute one double-threaded process at once
- Two hyperthreaded CPU cores can execute four single-threaded processes at once
- Two hyperthreaded CPU cores can execute two double-threaded processes at once
- Two hyperthreaded CPU cores can execute two single-threaded processes and one double-threaded process at once

---

### tldr
- Our operating system will allocate available processor time to threads
- These threads can belong to the same process for a multithreaded program
- Therefore, multithreading is limited by our hardware capabilities
- This is because our hardware is what provides us with the capability of processing threads in parallel
- If we only have one CPU with one core, then multithreading will not achieve anything
- If we have multiple CPU cores, then multithreading will achieve parallelism

---

### References
- [Defining the Architecture of Hyperthreading](https://stackoverflow.com/a/19518207)
- [Illustrating the Interaction between Multithreading and the OS](https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/4_Threads.html)
- [Illustrating Single-Threaded and Multi-Threaded Stacks](https://github.com/angrave/SystemProgramming/wiki/Pthreads%2C-Part-1%3A-Introduction#how-does-the-threads-stack-work)
- [Multithreading in Python](https://stackoverflow.com/questions/44793371/is-multithreading-in-python-a-myth)
- [Concurrency with Multithreading in Java8](https://winterbe.com/posts/2015/04/07/java8-concurrency-tutorial-thread-executor-examples/)
- [Submitting Runnables in Java](http://tutorials.jenkov.com/java-util-concurrent/executorservice.html#submit-runnable)
