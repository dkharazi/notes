---
title: "Generators"
draft: true
weight: "9"
katex: true
---

### Defining Lazy Evaluation
- Lazy evaluation refers to an object that is evaluated when it is needed, not when it is created
- For example, the object returned by `range(0,9)` is a lazy iterable
- However, it doesn't store the entire range $[0,...,9]$ in memory
- Instead, it stores a definition for `(i=0, i<10, i+=1)`
- Then, computes the next value only when needed
- Lazy evaluation is useful when computing on a very large dataset
- It allows us to start using the data immediately, without reading the whole dataset into memory
- Specifically, lazy evaluation is useful when we want to loop over some very large data and apply a computation to each element

### Describing Lazy Evaluation with Generators
- Generators use lazy evaluation
- Therefore, a generator evaluates each element one-by-one
- Generators allow us to suspend and resume the execution of a python function
- Roughly, generators allow us to pause execution of a function
- Generators are implemented using the `yield` keyword
- The following is an example of a generator:

```python
>>> def test():
...     yield 1
...     yield 2
...
>>> gen = test()
>>> next(gen)
1
>>> next(gen)
2
>>> next(gen)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

### Describing the Benefits of Generators
- Generators can be very memory-efficient
- This is because they only store very small iterations in memory at a time
- Since generators use lazy evaluation, their benefits are:
	- Calculating large sets of results
	- Replacing callbacks with iterations
- We should use generators (instead of loops) if we can't store some entire set of data in memory
- For example, this can happen when reading in large files
- Specifically, a file object is a generator
- A file object is lazily evaluated line-by-line using the built-in `open` function
	- The `with` keyword implicitly includes a `close()` function
	- The `open` keyword initializes a file generator

```python
with open('big.csv') as f:
	for line in f:
		do_something(line)
```

### Motivating Coroutines
- In Python 3.4, the new `yield from` keyword was introduced

```python
>>> def inner():
...     inner_result = yield 2
...     print('inner', inner_result)
...     return 3
...
>>> def outer():
...     yield 1
...     val = yield from inner()
...     print('outer', val)
...     yield 4
...
>>> gen = outer()
>>> next(gen)
1
>>> next(gen) # Goes inside inner() automatically
2
>>> gen.send("abc")
inner abc
outer 3
4
```

- This allows us to create generators inside of generators
- We're able to pass the data back and forth from the inner-most to the outer-most generators
- This concept introduced the idea of a *coroutine* in Python

### Introducing Coroutines from Generators
- Since then, coroutines have been separated from generators
- A coroutine is a function that can stop and resume while being run
- In Python, they are defined using the `async def` keyword
- Coroutines use their own form of `yield from` which is `await`
- The `async` and `await` keywords were introduced in Python 3.5
- Before Python 3.5, we created coroutines using the `yield from` keyword taken from generators
- The following is an example of these keywords in action:

```python
async def inner():
	return 1

async def outer():
	await inner()
```

---

### tldr
- Lazy evaluation refers to an object that is evaluated when it is needed, not when it is created
- Specifically, lazy evaluation is useful when we want to loop over some very large data and apply a computation to each element
- Generators use lazy evaluation
- Therefore, a generator evaluates each element one-by-one
- Generators allow us to suspend and resume the execution of a python function
- Roughly, generators allow us to pause execution of a function
- Generators are implemented using the `yield` keyword
- Since generators use lazy evaluation, their benefits are:
	- Calculating large sets of results
	- Replacing callbacks with iterations 

---

### References
- [Benefits of using Generators](https://stackoverflow.com/a/102632/12777044)
- [Defining Lazy Evaluation](https://stackoverflow.com/a/20535379/12777044)
- [Real World Use-Case of Generators](https://stackoverflow.com/a/23530101/12777044)
