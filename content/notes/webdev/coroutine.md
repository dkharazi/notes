---
title: "Coroutines"
draft: true
weight: "10"
katex: true
---

### Differentiating between Subroutines and Coroutines
- Subroutines and coroutines are an abstraction of:
	- An call stack
	- An instruction pointer
- An call stack is a collection of code relevant to its scope
- These pieces of code include local variables, functions, etc.
- The instruction pointer is a pointer to the current instruction
- This is useful for generators, since we need to know where to resume in the code when returning to the call stack
- Some examples of subroutines are functions and procedures
- An example of a coroutine is a generator
- The distinction between `def` and `async def` is just for clarity
- However, there is an actual difference is `return` and `yield`

### Defining Subroutines
- A subroutine represents a new stack level to hold local variables
- Consider a subroutine like the following:

```python
def subfoo(bar):
     qux = 3
     return qux * bar
```

- When we run the code above:
	1. Allocate stack space for `bar` and `qux`
	2. Recursively execute the first statement and jump to the next statement
	3. Once at the `return` statement, push its value to the stack calling the function
	4. Clear the `subfoo` stack space (`bar` and `qux`)
	5. Clear the instruction pointer
- Steps 4 and 5 imply the local variables and pointer are lost
- Specifically, the function can't be resumed after `return` without calling it again and creating an entirely new stack
- The instruction pointer follows the following path:

```
root -\
  :    \- subfoo --\
  :/--<---return --/
  |
  V
```

### Defining Coroutines
- A coroutine is like a subroutine
- However, it can exit *without* destroying its state
- Consider a coroutine like the following:

```python
def cofoo(bar):
      qux = yield bar  # yield marks a break point
      return qux
```

- When you run the code above:
	1. Allocate stack space for `bar` and `qux`
	2. Recursively execute the first statement and jump to the next statement
		- Once at a `yield`, push its value to the stack calling the function, while also storing this local stack and instruction pointer
		- Once calling into `yield`, restore stack and instruction pointer
		- Then, push arguments to `qux`
	3. Once at the `return` statement, push its value to the stack calling the function
	4. Clear the `cofoo` stack space (`bar` and `qux`)
	5. Clear the instruction pointer
- Note, the addition of steps 2.1-2.3
- This implies that a coroutine can be suspended and resumed at predefined points
- This is similar to how a subroutine is suspended during calling another subroutine
- However, a suspended coroutine is part of a separate/isolated stack
- Meaning, suspended coroutines can be freely stored or moved between stacks
- Any call stack that has access to a coroutine can resume it

### Summarizing the Subroutines and Coroutines
- The main difference between the two routines:
	- Subroutines use `return` to suspend the function
	- Coroutines use `yield` to suspend the function
- Once a function is suspended:
	- Subroutines can't resume again
	- Coroutines can resume again (e.g. `next()` for generators)
- The output of the two routines:
	- Subroutines return data values
	- Coroutines yield a data value, call stack, pointer (belonging to the called function)
- Specifically, coroutines are used for:
	- Looping over large data objects
	- Asynchronous I/O

### Traversing the Call Stack
- A subroutine can go down the call stack with `return`
- A subroutine can go up the call stack with `()`
- A coroutine only goes down the call stack with `yield`
- A coroutine can go up the call stack with `yield from`
- Consider the following coroutine:

```python
def wrap():
    yield 'before'
    yield from cofoo()
    yield 'after'
```

- Actually, a coroutine goes up *and* down call stacks with `yield from` at the same time
- Specifically, `yield from` does the following:
	- Suspends the stack and instruction pointer of `wrap`
	- And runs `cofoo`
- Note, `wrap` stays suspended until cofoo finishes completely
- Whenever `cofoo` suspends or something is sent, `cofoo` is directly connected to the call stack of `wrap`

### More Traversing with Coroutines
- As stated previously, `yield from` allows us to connect to two scopes across another intermediate one
- When applied recursively, that means the *top* of the stack can be connected to the *bottom* of the stack
- Meaning, newer coroutines pushed on the stack can yield values to older coroutines without knowing about each other
- This makese coroutines much cleaner than callbacks
- This implies coroutines of the same root are concurrent but not parallel

### Python's `async` and `await`
- The explanation has so far explicitly used the `yield` and `yield from` vocabulary of generators
- In Python 3.5, the `async` and `await` keywords were introduces
- These keywords essentially mean the same as `yield` and `yield from`
- They mainly changed for clarity purposes

```python
def foo():  # subroutine?
     return None

def foo():  # coroutine?
     yield from foofoo()  # generator? coroutine?

async def foo():  # coroutine!
     await foofoo()  # coroutine!
     return None
```

---

### tldr
- The main difference between the two routines:
	- Subroutines use `return` to suspend the function
	- Coroutines use `yield` to suspend the function
- Once a function is suspended:
	- Subroutines can't resume again
	- Coroutines can resume again (e.g. `next()` for generators)
- The output of the two routines:
	- Subroutines return data values
	- Coroutines yield a data value, call stack, pointer (belonging to the called function)
- Specifically, coroutines are used for:
	- Looping over large data objects
	- Asynchronous I/O

---

### References
- [How Asyncio Works with Coroutines](https://stackoverflow.com/a/51116910/12777044)
- [Coroutines in Asyncio](https://stackoverflow.com/a/51177895/12777044)
- [Describing Coroutines with Examples](https://stackabuse.com/coroutines-in-python/)
- [Coroutines in gevent](https://learn-gevent-socketio.readthedocs.io/en/latest/general_concepts.html#what-s-a-coroutine)
- [Comparing Python3 with ES6](https://stackoverflow.com/a/47499994/12777044)
- [Understanding the Yield Keyword](https://stackoverflow.com/a/36220775/12777044)
