---
title: "Event Loop in Python"
draft: true
weight: "11"
katex: true
---

### Introducing the Event Loop in Python
- We can think of an event loop as something like a `while True` loop
- Specifically, this loop does the following:
	- Monitors coroutines
	- Taking feeback of idle coroutines
	- Looking for executable coroutines in the meantime
- It is able to wake up idle corountines when resources for that coroutine become available
- Coroutines don’t do much on their own until they are tied to the event loop
- By default, an async IO event loop runs in a single thread and on a single CPU core
- Usually, running one single-threaded event loop in one CPU core is more than sufficient

### Describing the Anatomy of Event Loops
- A coroutine is a separate concept from threads and processes
- A coroutine has no concept of yielding control to a new coroutine
- It can only yield control to its caller at the bottom of the coroutine stack
	- A caller refers to the coroutine function calling the child coroutine function
- This caller can then switch to another coroutine and run it
- This root node of several coroutines is commonly an *event loop*
- Once a coroutine is suspended, it yields an *event* once it resumes
- In turn, the event loop is capable of waiting for these events to occur
- This allows it to decide which coroutine to run next, or how to wait before resuming
- Such a design implies that there is a set of pre-defined events that the loop understands
- Several coroutines `await` each other, until finally an event is `await`ed
- This event can communicate directly with the event loop by yielding control
- The key is that coroutine suspension allows the event loop and events to directly communicate
- The intermediate coroutine stack does not require any knowledge about which loop is running it, nor how events work

### Motivating Events in Time
- The simplest event to handle is reaching a point in time
- This is a fundamental block of threaded code as well
- Specifically, a thread repeatedly `sleep`s until a condition is true
- However, a regular `time.sleep()` blocks execution by itself
- Instead, we want other coroutines to not be blocked (meaning it is asynchronous)
- Specifically, we want to tell the event loop when it should resume the current coroutine stack
- In other words, if we need to pause an entire script, then use `time.sleep`
- If we need to pause a single coroutine, then use `asyncio.sleep`

### Defining an Event in Time
- An event is simply a value we can identify
- We can define this with a simple class that stores our target time
- In addition to storing the event information, we can allow to `await` a class directly
- Note, this class only stores the event
- It does not say how to actually handle it
- The only special feature is `__await__`
- Specifically, `__await__` is what the `await` keyword looks for
- Practically, it is an iterator but not available for the regular iteration machinery

```python
class AsyncSleep:
    """Event to sleep until a point in time"""
    def __init__(self, until: float):
        self.until = until

    # used whenever someone ``await``s an instance of this Event
    def __await__(self):
        # yield this Event to the loop
        yield self

    def __repr__(self):
        return '%s(until=%.1f)' % (self.__class__.__name__, self.until)
```

### Awaiting an Event
- Now that we have an event, how do coroutines react to it
- We should be able to express the equivalent of `sleep` by `await`ing our event
- To better see what is going on, we wait twice for half the time:

```python
import time

async def asleep(duration: float):
    """await that ``duration`` seconds pass"""
    await AsyncSleep(time.time() + duration / 2)
    await AsyncSleep(time.time() + duration / 2)
```

- We can directly instantiate and run this coroutine
- Similar to a generator, using `coroutine.send` runs the coroutine until it `yield`s a result

```python
coroutine = asleep(100)
while True:
    print(coroutine.send(None))
    time.sleep(0.1)

# Returns:
# AsyncSleep(until=1589572249.3)
# AsyncSleep(until=1589572249.4)
```

- This gives us two `AsyncSleep` events and then a `StopIteration` when the coroutine is done
- Notice, the only delay is from `time.sleep` in the loop
- Each `AsyncSleep` only stores an offset from the current time

### Using Sleep Events
- At this point, we have two separate mechanisms at our disposal:
	- `AsyncSleep` events that can be yielded from inside a coroutine
	- `time.sleep` that can wait without impacting coroutines
- Notably, these two are very different
- Neither one affects or triggers the other
- As a result, we can come up with our own strategy to `sleep` to meet the delay of an `AsyncSleep`

---

### tldr
- We can think of an event loop as something like a `while True` loop
- Specifically, this loop does the following:
	- Monitors coroutines
	- Taking feeback of idle coroutines
	- Looking for executable coroutines in the meantime
- It is able to wake up idle corountines when resources for that coroutine become available
- Coroutines don’t do much on their own until they are tied to the event loop
- By default, an async IO event loop runs in a single thread and on a single CPU core
- Usually, running one single-threaded event loop in one CPU core is more than sufficient

---

### References
- [Description of Python's Event Loop](https://realpython.com/async-io-python/#the-event-loop-and-asynciorun)
- [Event Loops in Asyncio](https://stackoverflow.com/a/51177895/12777044)
- [Motivating Asyncio with Generators](https://stackoverflow.com/a/51116910/12777044)
- [Comparison of Sleep Example in Asyncio](https://stackoverflow.com/a/56730924/12777044)
