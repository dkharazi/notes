---
title: "High-Level Asyncio API"
draft: true
weight: "14"
katex: true
---

### Describing Coroutines
- Coroutines are a more generalized form of subroutines
- Subroutines are entered at one point and exited at another point
- Coroutines can be entered, exited, and resumed at many different points
- They can be implemented with the `async def` statement
- Coroutines are declared using async/await syntax preferably

### Defining Basic Coroutines
- The following snippet of code:
	- Prints *hello*
	- Waits 1 second
	- Prints *world*

```python
>>> import asyncio

>>> async def main():
...     print('hello')
...     await asyncio.sleep(1)
...     print('world')

>>> asyncio.run(main())
hello
world
```

- Calling a coroutine will not schedule it for execution:

```python
>>> main()
<coroutine object main at 0x1053bb7c8>
```

- To do this synchronously, we need to:
	1. Create a coroutine using `async def` and `await`
	2. Execute the coroutine directly (without involving the asyncio event loop) using `asyncio.run()`
- To do this asynchronously, we need to:
	1. Create a coroutine using `async def` and `await`
	2. Wrap the coroutine as a task using `asyncio.create_task()`
	3. Pass the task into the asyncio event loop using `asyncio.run()`

### Asynchronously Running a Coroutine in an Event Loop
1. Await on a coroutine
- Coroutines dont't run concurrently
- Meaning, coroutines run synchronously

```python
import asyncio
import time

async def say_after(delay, what):
    await asyncio.sleep(delay)
    print(what)


async def main():
    c1 = say_after(10, 'hello')
    c2 = say_after(20, 'world')

    print(f"started at {time.strftime('%X')}")
    await c1
    await c2
    print(f"finished at {time.strftime('%X')}")


asyncio.run(main())  # 30 seconds
```

2. Awaiting on a task
- Tasks wrap coroutines
- Roughly speaking, tasks are an asynchronous coroutine
- Tasks run concurrently
- Specifically, tasks run asynchronously
- Tasks are used to run coroutines in event loops
- Meaning, event loops only run tasks


```python
import asyncio
import time

async def say_after(delay, what):
    await asyncio.sleep(delay)
    print(what)


async def main():
    c1 = say_after(10, 'hello')
    c2 = say_after(20, 'world')

    task1 = asyncio.create_task(c1)
    task2 = asyncio.create_task(c2)

    print(f"started at {time.strftime('%X')}")
    await task1
    await task2
    print(f"finished at {time.strftime('%X')}")


asyncio.run(main())  # 20 seconds
```

### Defining a Task

### The Relationship between Tasks, the Event Loop
- Deep inside asyncio, we have a single event loop (per thread/process)
- The event loop runs tasks from a queue
- To be clear, this queue contains tasks
- It is sometimes referred to as the task queue
- The event loop is responsible for:
	- Calling tasks when they are ready
	- Coordinating all the effort into one single working machine

### Defining An Awaitable

---

### tldr

---

### References
- [Asyncio Documentation](https://docs.python.org/3/library/asyncio.html)
- [Asyncio Docs about Coroutines and Tasks](https://docs.python.org/3/library/asyncio-task.html)
- [Asyncio Docs about Queues](https://docs.python.org/3/library/asyncio-queue.html)
- [Asyncio Streams](https://docs.python.org/3/library/asyncio-stream.html)
- [Synchonization Primitives](https://docs.python.org/3/library/asyncio-sync.html)
- [Asyncio Subprocesses](https://docs.python.org/3/library/asyncio-subprocess.html)
- [Comparing Tasks to Promises in JS](https://stackoverflow.com/a/47499994/12777044)
