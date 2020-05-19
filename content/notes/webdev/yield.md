---
title: "The Yield Keyword"
draft: true
weight: "8"
katex: true
---

### Motivating the Yield Keyword
- `yield:` To produce or provide (as in agriculture)
	- In Python, it provides the next data in the series
- `yield:` To give way or relinquish (as in political power)
	- It relinquishes CPU execution until the iterator advances

### The List Approach in Python

```python
def square_list(n):
    the_list = []            # Replace
    for x in range(n):
        y = x * x
        the_list.append(y)   # these
    return the_list          # lines
```

### The Yield Approach in Python

```python
def square_yield(n):
    for x in range(n):
        y = x * x
        yield y              # with this one.
```

### Comparing Behavior
```python
>>> sl = square_list(4)   # [0, 1, 4, 9]
>>> sy = square_yield(4)  # <generator object>
>>> for square in sl:
...     print(square)
...
0
1
4
9
>>> for square in sy:
...     print(square)
...
0
1
4
9
```

### Benefits of using Yield
- Yield is **single-pass**
	- You can only iterate through once
	- A function with `yield` is called a generator function
	- A generator function returns an iterator using `yield`
- Yield is **lazy**
	- It puts off computation
	- A function with `yield` doesn't actually execute at all when you call it
	- It returns an iterator object and remembers where it left off
- Yield is **versatile**
	- Data doesn't have to be stored all together
	- It can be made available one at a time
	- It can be infinite

---

### tldr
- The yield keyword does the following:
	- Provides the next data in the series
	- Relinquishes CPU execution until the iterator advances
- Yield is **single-pass**
- Yield is **lazy**
- Yield is **versatile**

---

### References
- [Examples of the Yield Keyword](https://stackoverflow.com/a/36220775/12777044)
- [Brief Description of Yield](https://stackoverflow.com/a/231788/12777044)
