---
title: "Asyncio"
draft: true
weight: "13"
katex: true
---

### Motivating the Use of Asyncio
- Asyncio is a library used for writing asynchronous (i.e. concurrent) code
- Asyncio uses coroutines for asynchronous programming
- Asynchronous programming has the following properties:
	- Asynchronous routines are able to *pause* while waiting on their ultimate result
		- As a result, they let other routines run in the meantime
	- Asynchronous code facilitates concurrent execution
		- In other words, gives it provides the look and feel of concurrency
- Refer to the following diagram:
	- White terms represent concepts
	- Green terms represent implementations of those concepts

![Asyncio](/img/asyncio.png)

### Illustrating Asynchronous Code with a Chess Analogy
- Async IO may at first seem counterintuitive and paradoxical
- How does something that facilitates concurrent code use a single thread and a single CPU core?
- Let's say we play in a chess exhibition
- Specifically, we play multiple amateur players
- There are two ways of conducting the exhibition:
	- Synchronously
	- Asynchronously
- In the chess exhibition, let's assume the following:
	- There are $24$ opponents
	- Each move only takes us $5$ seconds
	- Each move takes $55$ seconds for each of our opponents
	- There are $30$ pair-moves on average ($60$ moves in total)
- If we played synchronously:
	- We'd complete one game at a time (never two at the same time)
	- Each game takes $30$ minutes
	$$ (55 + 5) \times 30 = 1800 \text{ seconds} = 30 \text{ minutes} $$
	- The entire exhibition takes $12$ hours
	$$ 24 \times 30 = 720 \text{ minutes} = 12 \text{ hours} $$
- If we played asynchronously:
	- We'd move from table to table
	- We'd make one move at each table
	- We'd leave the table and let the opponent make their next move during the wait time
	- One move across all $24$ games takes us $2$ minutes
	$$ 24 \times 5 = 120 \text{ seconds} = 2 \text{ minutes} $$
	- The entire exhibition is now cut down to $1$ hour
	$$ 120 \times 30 = 3600 \text{ seconds} = 1 \text{ hour} $$

### Demonstrating the Birth of `async` and `await`
- **3.3:** The `yield from` expression allows for generator delegation
- **3.4:** asyncio was introduced in the Python standard library with provisional API status
- **3.5:** `async` and `await` became a part of the Python grammar, used to signify and wait on coroutines
	- They were not yet reserved keywords
	- However, you could still define functions or variables named `async` and `await`
- **3.6:** Asynchronous generators and asynchronous comprehensions were introduced
	- The API of asyncio was declared stable rather than provisional
- **3.7:** `async` and `await` became reserved keywords
	- However, they cannot be used as identifiers
	- They are intended to replace the `asyncio.coroutine()` decorator
	- `asyncio.run()` was introduced to the asyncio package, among a bunch of other features

### Motivating the `async` and `await` Syntax
- Asyncio allows functions to run during waiting periods of other functions
- Since CPython is single threaded, the event loop normally would block these functions from doing this
- This is why asynchronous programming is so powerful
- Asincio uses coroutines to perform its asynchronous programming
- A coroutine is a specialized version of a Python generator function
- Specifically, a coroutine is a function that can do the following:
	- Suspend its execution before reaching `return`
	- Indirectly pass control to another coroutine for some time

### Asynchronous Example of Sleeping
- To introduce the `async` and `await` keywords, let's look at the following example:

```python
# countasync.py
import asyncio

async def count():
    print("One")
    await asyncio.sleep(1)
    print("Two")

async def main():
    await asyncio.gather(count(), count(), count())

if __name__ == "__main__":
    import time
    s = time.perf_counter()
    asyncio.run(main())
    elapsed = time.perf_counter() - s
    print(f"{__file__} exec in {elapsed:0.2f} seconds.")
```

- We use `asyncio.run()` to run an event loop
- Meaning, `main()` is our event loop
- It acts as a coordinator of the `count()` coroutines
- Each coroutine is suspended on the call stack temporarily when reaching `asyncio.sleep(1)`
- In other words, when each task reaches `asyncio.sleep(1)`, the function yells up to the event loop and gives control back to it
- Specifically, each function says:
> *I’m going to be sleeping for 1 second, so go ahead and let something else meaningful be done in the meantime*
- We can see this happening in the output:

```sh
$ python3 countasync.py
One
One
One
Two
Two
Two
countasync.py exec in 1.01 seconds.
```

- The order of this output is the heart of asyncio

### Synchronous Example of Sleeping
- Previously, we observed the output of asynchronous timeouts
- Let's contrast this to the synchronous version:

```python
# countsync.py
import time

def count():
    print("One")
    time.sleep(1)
    print("Two")

def main():
    for _ in range(3):
        count()

if __name__ == "__main__":
    s = time.perf_counter()
    main()
    elapsed = time.perf_counter() - s
    print(f"{__file__} exec in {elapsed:0.2f} seconds.")
```

- Note, `time.sleep()` can represent any time-consuming blocking function call
- On the other hand, `asyncio.sleep()` is used to stand in for a non-blocking call
- We can see that `time.sleep()` or any other blocking call is incompatible with asynchronous Python code
- This is because it will stop everything in its tracks for the duration of the sleep time
- We can see this happening in the output:

```sh
$ python3 countsync.py
One
Two
One
Two
One
Two
countsync.py exec in 3.01 seconds.
```

### Defining the Rules of Asyncio
- `async def` introduces either:
	- A native coroutine
	- An asynchronous generator
- `await` passes function control back to the event loop
	- It suspends the execution of the surrounding coroutine
- Let's say python encounters an `await` f() expression in the scope of g()
- This is how `await` informs the event loop:

> *Suspend execution of g() until whatever I’m waiting on—the result of f()—is returned. In the meantime, go let something else run.*

- This looks something like this:

```python
async def g():
    # Pause here and come back to g() when f() is ready
    r = await f()
    return r
```

### Defining the `async def` Syntax
- A function introduced with `async def` is a coroutine
- It may use `await`, `return`, or `yield`
	- All of these are optional
- For example, declaring `async def noop(): pass` is valid
- Using `await` and/or `return` also creates a coroutine function
- To call a coroutine function, you must `await` it to get its results
- It is less common to use `yield` in an `async def` block
- This creates an asynchronous generator, which you iterate over with `async for`
- Anything defined with `async def` should not use `yield from`
	- This will raise a `SyntaxError`
- Using `await` outside of an `async def` will raise a `SyntaxError` also
- Here are some examples to summarise the above rules:

```python
async def f(x):
    y = await z(x)  # OK - `await` and `return` allowed in coroutines
    return y

async def g(x):
    yield x  # OK - this is an async generator

async def m(x):
    yield from gen(x)  # No - SyntaxError

def m(x):
    y = await z(x)  # Still no - SyntaxError (no `async def` here)
    return y
```

### Defining the `await` Keyword
- A function introduced with `await` is a coroutine
- When we use `await f()`, `f()` must be an awaitable object
- An awaitable object can be thought of as:
	- Another coroutine
	- An object defining an `__await__()` method that returns an iterator
- Mostly, we'll only need to worry about enforcing case 1
- Note, `async def` and `await` are considered a Python standard now
- Specifically, generator-based coroutines have been removed in Python 3.10

### Introducing High-Level API Structures
- Most programs will contain:
	- Small, modular coroutines
	- One wrapper coroutine
- The wrapper function chains the smaller coroutines together

**`asyncio.run()`**

- The entire management of the event loop is handled by `asynic.run(some_event_loop())`
- Specifically, `asyncio.run()` is used for:
	- Getting the event loop
	- Running tasks until those tasks are marked complete
	- Closing the event loop

**`asyncio.create_task()`**

- We can schedule the execution of a coroutine object using `asyncio.create_task()`
- These specific coroutines are referred to as tasks in asyncio
- These tasks are run by the event loop using `asyncio.run()`
- The following is an example of tasks being created:

```python
>>> async def coro(seq):
...     # 'IO' wait time is proportional to
...     # the max element.
...     await asyncio.sleep(max(seq))
...     return list(reversed(seq))
...
>>> async def main():
...     # This is a bit redundant in the case of one task
...     # We could use `await coro([3, 2, 1])` on its own
...     t = asyncio.create_task(coro([3, 2, 1]))
...     await t
...     print(f't: type {type(t)}')
...     print(f't done: {t.done()}')
...
>>> t = asyncio.run(main())
t: type <class '_asyncio.Task'>
t done: True
```

**`asyncio.gather()`**

- A collection of coroutines (or tasks) are organized into a single future object using `asyncio.gather([c1,c2,c3])`
- As a result, it returns a single future object
- For example, let's say we specify multiple tasks or coroutines $[c_{1},c_{2},c_{3}]$ using `asyncio.gather()`
- If we `await asyncio.gather([c1,c2,c3])`, then we're waiting for them to be completed
- The result of `asyncio.gather()` will be a list of the results across the inputs:

```python
>>> import time
>>> async def main():
...     t = asyncio.create_task(coro([3, 2, 1]))
...     t2 = asyncio.create_task(coro([10, 5, 0]))
...     print('Start:', time.strftime('%X'))
...     a = await asyncio.gather(t, t2)
...     print('End:', time.strftime('%X'))  # 10 seconds
...     print(f'Both done: {all((t.done(), t2.done()))}')
...     return a
...
>>> a = asyncio.run(main())
Start: 16:20:11
End: 16:20:21
Both done: True
>>> a
[[1, 2, 3], [0, 5, 10]]
```

---

### tldr

---

### References
- [Brief Description of Event Loops in Asyncio](https://realpython.com/python-concurrency/#asyncio-version)
- [Course Content about Event Loops](https://www.udemy.com/course/the-complete-javascript-course/learn/lecture/9939770#content)
- [Walkthrough of Asyncio](https://www.integralist.co.uk/posts/python-asyncio/)
- [More about Chaining Coroutines](https://python.readthedocs.io/fr/latest/library/asyncio-task.html#example-chain-coroutines)
- [Asyncio Documentation about Tasks](https://docs.python.org/3/library/asyncio-task.html)
