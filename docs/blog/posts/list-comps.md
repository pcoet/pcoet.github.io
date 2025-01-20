---
date: 2025-01-19
categories:
  - Python
tags:
  - Python
---

# Python list comprehensions

*Last updated: January 20, 2025*

This post provides a quick introduction to working with list comprehensions in
Python. List comprehensions let you create lists using a concise syntax that
resembles mathematical set builder notation. The basic syntax looks like this:

```python
new_list = [f(x) for x in old_list if some_condition]
```

`f(x)` is an optional function applied to each element in the list, and
`some_condition` is an optional condition for filtering items in the list.

If you're coming to Python from another language, you might not think to use
list comprehensions in many cases, because building out a list in a `for` loop
is more familiar. But list comprehensions are a concise, readable, and very
Pythonic tool worth having in the toolkit.

The following examples are adapted from the
[official Python docs](https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions).

## Generate a list

This example uses list comprehension syntax and the built-in
[`range()` type](https://docs.python.org/3/library/stdtypes.html#range)
to generate a list of cubes.

```python
cubes = [n**3 for n in range(10)]
print(cubes) # [0, 1, 8, 27, 64, 125, 216, 343, 512, 729]
```

## Apply a function to each item in a list

This example creates a list of cube roots by applying
[`math.cbrt()`](https://docs.python.org/3/library/math.html#math.cbrt) to each
item in `cubes`.

```python
import math

cube_roots = [math.cbrt(n) for n in cubes]
print(cube_roots) # [0.0, 1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 9.0]
```

## Filter a list

The list comprehension in this example filters `cubes` for even numbers greater
than 0.

```python
even_cubes = [n for n in cubes if n % 2 == 0 and n > 0]
print(even_cubes) # [8, 64, 216, 512]
```

## Create a list of tuples

The following list comprehension produces a list of tuples.

```python
nums_and_cubes = [(n, n**3) for n in range(5)]
print(nums_and_cubes) # [(0, 0), (1, 1), (2, 8), (3, 27), (4, 64)]
```

## Use a nested list comprehension

In this example, the list comprehension transposes a 2D list.

```python
sequences = [
  [0, 1, 2, 3, 4],
  [0, 1, 1, 2, 3],
  [2, 3, 5, 7, 11],
]

transposed_seqs = [[seq[i] for seq in sequences] for i in range(5)]
print(transposed_seqs) # [[0, 0, 2], [1, 1, 3], [2, 1, 5], [3, 2, 7], [4, 3, 11]]
```

## More on list comprehensions

To learn more about list comprehensions, see the following resources:

* [Wikipedia: List comprehension](https://en.wikipedia.org/wiki/List_comprehension)
* [PEP 202 &ndash; List Comprehensions](https://peps.python.org/pep-0202/)
* [Real Python: When to Use a List Comprehension in Python](https://realpython.com/list-comprehension-python/)