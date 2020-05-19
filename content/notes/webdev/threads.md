---
title: "Threads and Processes"
draft: true
weight: "1"
katex: true
---

### High-Level Understanding of a Process
- A process is an instance of a computer program that is being executed
- A thread is a basic unit of CPU utilization
- A task is a set of instructions allocated to memory
- A thread is what the CPU actually runs
- A process is what gets loaded in memory
- A process will include one or more threads
- This is because threads are what the CPU actually runs (not processes)
- Tasks and processes are used synonymously sometimes

### Defining the Structure of a Process
- The process model is based on two independent concepts:
	1. Resource grouping
	2. Execution
- In terms of resource grouping:
	- We can think of a process as something that groups related resources together
	- Specifically, a process has the following:
		- An **address space** containing program text and data
		- Information about **open files**
		- Information about **child processes**
		- And other resources
- In terms of execution:
	- We can roughly think of a process as a thread of execution
	- A thread of execution refers to a set of threads
	- A process doesn't perfectly translate to a set of threads, but we can think of it that way for now
	- Specifically, a thread has the following:
		- A **program counter** that keeps track of which instruction to execute next
		- A set of **registers** that hold its current working variables
		- A **stack** that contains the thread execution history

### Describing Processes and Threads
- A process refers to a program that is being executed
- A child process is a process created by another process (i.e. the parent process)
- A thread is the basic unit to which the operating system allocates processor time
- A thread can execute any code from the process
- Once a process is created by the operating system, a single thread will be initialized within that process, called the *primary thread*
- Each process can create additional threads from any of its threads

### Differentiating between Processes and Threads
- A major difference between a thread and a process is the following:
	- A process runs in a seperate memory space (compared to other processes)
	- A thread runs in a shared memory space (compared to other threads of the same process)
- Essentially, processes are used to group resources together, whereas threads are the entities scheduled for execution on the CPU
- For a process, the operating system:
	- Allocates memory for its instructions and data
- For a thread, the operating system:
	- Handles scheduling
	- Allocates CPU time

### Motivating and Defining Hyperthreading
- Recall each thread's state is maintained by the following:
	- A single program counter
	- A set of registers
- Classically, each CPU core could only support a single thread of execution
- Meaning, each CPU core only had enough resources (i.e. registers) for a single thread
- Therefore, the CPU would be idle while data fetching data from the main memory
- This would be especially slow if the data wasn't cached
- Thus, someone had the idea to have two sets of thread states (PC + registers)
- By doing this, another thread can get work done while the other thread is waiting on the main memory
	- This thread could be in the same process or a different process
- This idea of modifying a CPU core to include an extra set of registers and program counter for another thread is called *hyperthreading*
- Hyperthreaded CPU cores *genuinely* support 2 threads per core, compared to only 1 thread per core for non-hyperthreaded CPU cores

### Defining Units of Computation
- A single motherboard can have one or more CPUs
- A single CPU can have one or more cores
- A single non-hyperthreaded CPU core can execute a single thread at once
- A single hyperthreaded CPU core can execute two threads at once
- A single process can have one or more threads
- A single program can have one or more processes

### Illustrating Threads using Word
- Opening MS Word will initiate a process
- MS Word automatically saves typed text at certain time intervals
- Meaning, we're able to edit something and save something at the same time
- In this case, we have two separate threads for editing and saving
- We've observed editing and saving happening in parallel
- Therefore, we've observed these two threads being executed in parallel

### Illustrating using MS Paint
- Opening MS Paint will initiate a process
- MS Paint constantly reads mouse location and movements
- Meaning, we're able to draw pictures at any point
- The program must give its full attention to the mouse input and draw at the same time
- To do this, two or more threads of a program will execute at the same time
- Therefore, these two threads are being executed in parallel

### Illustrating using the JVM
- A JVM runs in a single process
- Threads in a JVM share the heap belonging to that process
- That is why several threads may access the same object
- Threads share the heap and save their own stack space
- This is how one thread's invocation of a method and its local variables are kept thread safe from other threads
- However, the heap is not thread-safe and must be synchronized for thread safety

---

### tldr
- A process refers to a program that is being executed
- A child process is a process created by another process (i.e. the parent process)
- A thread is the basic unit to which the operating system allocates processor time
- A thread can execute any code from the process
- A single motherboard can have one or more CPUs
- A single CPU can have one or more cores
- A single non-hyperthreaded CPU core can execute a single thread at once
- A single hyperthreaded CPU core can execute two threads at once
- A single process can have one or more threads
- A single program can have one or more processes

---

### References
- [Lecture Slides about the Modern Process and Thread](http://www.math-cs.gordon.edu/courses/cs312/lectures/pdf/usingOS.pdf)
- [Threads and Concurrency](https://stackoverflow.com/questions/1050222/what-is-the-difference-between-concurrency-and-parallelism)
- [Examples of a Process and Thread](https://www.quora.com/What-is-the-difference-between-the-thread-of-a-process-and-the-child-of-a-process-What-are-some-real-time-examples)
- [Illustrating Thread Context](https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/4_Threads.html)
- [Hyperthreading and Hardware Threads](https://stackoverflow.com/a/5593432)
- [Hyperthreading and the Operating System](https://stackoverflow.com/a/5593389)
- [Defining the Architecture of Hyperthreading](https://stackoverflow.com/a/19518207)
- [Defining a Process and a Thread](https://stackoverflow.com/a/200543)
- [Another Definition of a Process](https://stackoverflow.com/a/200475)
- [Illustrating a Process and Thread](https://stackoverflow.com/a/49841764)
- [Difference between Threads, Tasks, and Processes](https://stackoverflow.com/a/3051328/12777044)
