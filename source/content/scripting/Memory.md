---
title: Memory Management
summary: A note about Memory architecure and mangment.
description: A note about Memory architecure and mangment.
tags:
  - memory
---

# Resources

* [Memory Explained - LearnThatStack](https://www.youtube.com/watch?v=WpE8EnVMRBA)

# Stack

---

### Properties

* Small.
* Fast.
* Automatic.
* Data is ordered: LIFO (Last In First Out).
* Fixed size (1-8 MB).
* Data is popped (removed) from the stack when function returns.
* Allocation sizes must be known in advance.

---

### Stack Overflow

Stack Overflow happens when:

* Depth Problem
  * when creating too many frames in the Stack until the stack limit.
  * e.g. recursion with no stop condition.
  * fix: always have a base case.
* Size Problem
  * when creating a frame too large.
  * e.g. try to create a huge variable.
  * fix: put large data in the Heap.

# Heap

---

### Properties

* Large pool of memory (can grow to use most of available RAM).
* Flexible.
* Managed.
* Data is not ordered: you program request space, the system finds a free block and returns the address.
* Access data using its address which is tiny and lives on the stack.
* Use cases: 
  * when don't know how much space is need until runtime.
  * when data needs to survive after the function.
  * when data is too large for the Stack.

---

### Memory Leak

How does the Garbage Collector work:

1. Collector starts from the Stack and traces every reference chain.
1. Anything reachable in the Heap is kept. Anything unreachable is deleted.

Problem: if the program keeps references to object it no longer needs, the Heap memory is no cleared because still reachable

Fix: Explicit cleanup. The garbage collector claim unreachable memory, making memory unreachable is the developer job.

# Programming Language Variables Types

---

### Primitive

Primitives / Pass by Values (numbers, booleans, ...)

* When a primitive variable values is passed to another variable, **the value is copied**. 
* Now there are two separates variables with the same value in the Stack, modify one variable value will not impact the other one.

---

### Objects

Objects / Pass by Reference (lists, dicts, classes, ...)

* When an object variable value is passed to another variables, **the reference is copied**. 
* Now the two variables old the same reference (address) pointing to the same data in the Heap, modify one variable value and the other variable will be impacted.

---

### Example in Python


 > 
 > Assignment statements in Python do not copy objects, they create bindings between a target and an object. For collections that are mutable or contain mutable items, a copy is sometimes needed so one can change one copy without changing the other.
 > 
 > Source: [Shallow and deep copy operations - Python](https://docs.python.org/3/library/copy.html)

````py
# List of dicts
my_list = [
	{ "player": 1, "class": "knight" },
	{ "player": 2, "class": "pirate" }
]

# Normal Copy
# Assign reference of the list that contains references to the dicts
my_list_2 = my_list

# Swallow Copy
# Create a new list that contains the same references to the dicts
my_list_3 = copy.copy(my_list)

# Deep Copy
# Create a new list and new dicts
my_list_4 = copy.deepcopy(my_list)
````
