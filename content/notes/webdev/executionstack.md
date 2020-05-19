---
title: "Execution Stack"
draft: true
weight: "7"
katex: true
---

### Describing an Execution Context
- An execution context ensures consistent access to non-local state for out-or-order execution (e.g. generators and coroutines)
- Conceptually, an **execution context** is a stack of logical contexts
- A **logical context** is a mapping of context variables to their values in that particular logical context
- There is always exactly one active execution context per thread
- Specifically, the execution context follows a LIFO model
- Sometimes, the execution context is referred to as the call stack
- A **context variable** is an object representing a value in the execution context
- A new context variable object is created by calling the following:
```
contextvars.ContextVar(name)
```

### API Calls for Context Variables
- `name:` The value passed to `ContextVar()`
- `get():` A function for getting a context variable
- `set():` A function for setting the value of a context variable
- `delete():` A function for removing a context variable

### Details about Logical Contexts
- Logical context is an immutable weak key mapping
- There aren't reference cycles that could:
	- Extend the lifespan of ContextVar objects
	- Prevent garbage collection of ContextVar objects
- Values put in the execution context are guaranteed to stay alive while there is a ContextVar key referencing them in the thread
- If a ContextVar is garbage collected, all of its values will be removed from all contexts
- These values will be garbage collected if necessary
- If an OS thread has ended its execution, its thread state will be cleaned up along with its execution context
- Meaning, all values bound to all context variables in the thread will be cleaned up

---

### tldr
- An execution context ensures consistent access to non-local state for out-or-order execution (e.g. generators and coroutines)
- Conceptually, an execution context is a stack of logical contexts
- A logical context is a mapping of context variables to their values in that particular logical context
- A context variable is an object representing a value in the execution context

---

### References
- [Course Content about Execution Contexts and Stacks](https://www.udemy.com/course/the-complete-javascript-course/learn/lecture/5869128#content)
- [Course Content about Execution Contexts in Detail](https://www.udemy.com/course/the-complete-javascript-course/learn/lecture/5869130#content)
- [High-Level Definitions of Execution Contexts](https://stackoverflow.com/a/9384894/12777044)
- [PEP 550: Execution Contexts](https://www.python.org/dev/peps/pep-0550/)
