---
title: "Python Data Structures"
weight: 2
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# Python Data Structures

Python’s data structures are essential tools for any programmer. They help us store, manipulate, and retrieve data efficiently. Python's built-in data structures, like lists, tuples, sets, and dictionaries, offer various ways to handle and organize data, each with its own strengths and purposes.

## A Bit of History

Python was created by Guido van Rossum in the late 1980s with a focus on simplicity and readability. From the start, Python’s design aimed to make data handling straightforward. Early versions, like Python 1.0 released in 1994, included basic structures like lists and dictionaries. As Python evolved, so did its data structures, getting more features and optimizations with each new version.

## Lists

### What Are Lists?

In Python, a list is a versatile, ordered collection that can hold items of any type. Lists are mutable, meaning you can change their contents after creation. This flexibility makes them perfect for many tasks, from simple data storage to complex data manipulation.

You create a list using square brackets `[]`. Here’s a quick example:

```python
# A list of integers
numbers = [1, 2, 3, 4, 5]

# A list with different types of elements
mixed_list = [1, "hello", 3.14, [1, 2, 3]]
```

### Working with Lists

Python lists are packed with useful operations. You can access elements by their index, slice the list to get a subset, append new items, or remove existing ones. Here’s how:

```python
# Accessing elements and slicing
numbers = [1, 2, 3, 4, 5]

# Get the first element
first_element = numbers[0]  # Output: 1

# Slice to get a subset
subset = numbers[1:4]  # Output: [2, 3, 4]

# Append and remove elements
numbers.append(6)
numbers.remove(3)
```

### Performance Tips

Lists are dynamic arrays. They grow or shrink as needed, making them quite flexible. Appending items is usually fast, but inserting or removing elements in the middle can be slower. This is because shifting elements takes time proportional to the list’s size.

## Tuples

### What Are Tuples?

A tuple is similar to a list but with a key difference: it’s immutable. Once you create a tuple, you can’t change its contents. This immutability makes tuples ideal for data that shouldn’t change, like coordinates or fixed settings.

You create a tuple using parentheses `()`. Here’s an example:

```python
# A simple tuple
coordinates = (10, 20)

# A tuple with mixed types
info = ("Alice", 30, 5.6)
```

### Working with Tuples

You can access elements and slice tuples just like lists, but you can’t modify their contents:

```python
# Accessing elements and slicing
coordinates = (10, 20)

# Get the first element
x = coordinates[0]  # Output: 10

# Slice to get a subset
subset = coordinates[0:2]  # Output: (10, 20)
```

### Performance Tips

Tuples are generally more memory-efficient than lists. They offer faster access times due to their fixed size, which allows for some performance optimizations.

## Sets

### What Are Sets?

A set is an unordered collection of unique elements. Unlike lists and tuples, sets don’t allow duplicates and don’t keep any specific order. Sets are great for operations that involve uniqueness, like checking membership or performing set operations.

You create a set using curly braces `{}` or the `set()` function:

```python
# A set of unique numbers
unique_numbers = {1, 2, 3, 4, 5}

# Create a set with duplicates removed
more_numbers = set([1, 2, 2, 3, 4])
```

### Working with Sets

Sets support operations like checking if an element is present, finding the union, intersection, or difference of sets:

```python
# Checking membership and set operations
unique_numbers = {1, 2, 3, 4, 5}

# Membership test
is_present = 3 in unique_numbers  # Output: True

# Union, intersection, and difference
set_a = {1, 2, 3}
set_b = {3, 4, 5}
union_set = set_a | set_b  # Output: {1, 2, 3, 4, 5}
intersection_set = set_a & set_b  # Output: {3}
difference_set = set_a - set_b  # Output: {1, 2}
```

### Performance Tips

Sets use hash tables internally, making operations like membership testing and set operations generally very efficient, with average time complexity of O(1) for membership tests and O(n) for other set operations.

## Dictionaries

### What Are Dictionaries?

A dictionary is an unordered collection of key-value pairs. Each key is unique, and it maps to a value. Dictionaries are incredibly useful for cases where you need to associate keys with values, like storing user information or configuration settings.

You define a dictionary using curly braces `{}` with keys and values separated by colons `:`:

```python
# A dictionary of student information
student = {
    "name": "Alice",
    "age": 21,
    "grades": [85, 90, 78]
}
```

### Working with Dictionaries

You can access values by their key, add or update key-value pairs, and remove entries:

```python
# Accessing and modifying dictionary entries
student = {
    "name": "Alice",
    "age": 21,
    "grades": [85, 90, 78]
}

# Get a value by key
name = student["name"]  # Output: Alice

# Add or update entries
student["major"] = "Computer Science"
student["age"] = 22

# Remove an entry
del student["grades"]
```

### Performance Tips

Dictionaries are also implemented as hash tables, offering efficient performance for lookups, insertions, and deletions, with an average time complexity of O(1).

## Specialized Data Structures

Python’s `collections` module offers specialized data structures that provide even more functionality:

### NamedTuple

The `namedtuple` function creates tuple subclasses with named fields, making your code more readable:

```python
from collections import namedtuple

# Define a named tuple
Point = namedtuple('Point', ['x', 'y'])

# Create and use a named tuple
p = Point(x=10, y=20)
print(p.x, p.y)  # Output: 10 20
```

### Deque

`deque` is a double-ended queue that supports fast appends and pops from both ends. It's perfect for implementing queues and stacks:

```python
from collections import deque

# Create and manipulate a deque
queue = deque([1, 2, 3])
queue.append(4)
queue.appendleft(0)
item = queue.pop()
item = queue.popleft()
```

### Counter

`Counter` is a specialized dictionary for counting hashable items, useful for tallying occurrences:

```python
from collections import Counter

# Create and use a Counter
count = Counter(['a', 'b', 'a', 'c', 'b', 'a'])
print(count['a'])  # Output: 3
print(count.most_common(2))  # Output: [('a', 3), ('b', 2)]
```

### OrderedDict

`OrderedDict` maintains the order of items as they are inserted, which is helpful when order matters:

```python
from collections import OrderedDict

# Create and use an OrderedDict
ordered_dict = OrderedDict([
    ('first', 1),
    ('second', 2),
    ('third', 3)
])

for key, value in ordered_dict.items():
    print(key, value)
```

## Performance Considerations

### Time Complexity

Knowing the time complexity of operations helps you understand how data structures perform. For instance, list operations like appending are {{< katex >}}O(1){{< /katex >}}, while inserting or deleting elements can be {{< katex >}}O(n){{< /katex >}}. Set and dictionary operations usually have average-case time complexity of {{< katex >}}O(1){{< /katex >}} thanks to hash tables.

### Space Complexity

Space complexity refers to the amount of memory a data structure uses. Lists and dictionaries grow as needed, while tuples are more memory-efficient because of their immutability. Named tuples offer a memory-efficient alternative to regular tuples with named fields.