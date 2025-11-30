Link to External Python Cheatsheet [here](https://www.geeksforgeeks.org/python-cheat-sheet/) 
## Table of Contents:
1. [[#Section 1 Python Basics]]
2. [[#Section 2 Built-In Data Structures in Python]]
3. [[#Section 3 Advanced Data Structures in Python]]
4. [[#Section 4 Advanced Programming Constructs]]
5. [[#Section 5 Exception & File Handling]]
6. [[#Section 6 Object-Oriented Programming (OOP)]]
7. [[#Section 7 Python Standard Libraries]]
8. [[#Section 8 Essential Third-Party Libraries]]

## Section 1: Python Basics
### Language Overview
Python is an **interpreted, object-oriented, high-level** programming language with dynamic typing and dynamic binding. It emphasizes readable, concise syntax and rapid development. Python’s interpreter and extensive standard library are freely available on all major platforms. It supports modules and packages for modularity and code reuse. Because there is no separate compilation step, the edit-test-debug cycle is very fast, and runtime errors raise exceptions with tracebacks instead of segmentation faults.

**Flavors of Python:** CPython (Written in C), Jython (Converts to Java), Pypy (Written in Rpython, JIT Compiler), Anaconda Python (Distro for Data Science)

Sample Program in Python:
```python
print("Hello World!")

Output: Hello World

# single line comment
"""
	Docstring
	Multi-line comment
"""
```

### Types and Values
Python has several **primitive types**. **Numeric types** include `int` (arbitrary-precision integers), `float` (floating-point), and `complex` (complex numbers). Integers (`int`) have unlimited precision; floats follow the machine’s C double format. Boolean values `True` and `False` are a subtype of `int` (where `False==0`, `True==1`), but should be used explicitly as Booleans. Other simple types include `NoneType` (the singleton `None`, represents “no value”) and `str` (immutable text strings).

Values in Python are **immutable** by default except for certain containers. Literals create values: e.g. `42` is an `int`, `3.14` a `float`, `1+2j` a `complex`, `"text"` a `str`, and `[1,2,3]` a `list`. You can convert between types with constructors like `int(x)`, `float(x)`, `complex(x)`, and `bool(x)`.

```python
# Numeric types and basic conversions
x, b, o, h = 255, 0b11101, 0o377, 0xff # Int (decimal, binary, octal, hex)
y = 3.14159      # float
z = 1 + 2j       # complex
print(type(x), type(y), type(z))  # <class 'int'> <class 'float'> <class 'complex'>

x2 = float(x)    # 42.0, converts int to float
z2 = complex(3, 4)  # 3+4j, explicit complex from real, imag
print(z2, z2.real, z2.imag)  # 3+4j 3.0 4.0

flag = True     # bool is subclass of int, but use for truthness, anything other than                    (True, 1) is equated as (False, 0)
print(int(flag))  # 1

var = None # Null value: NoneType
```
##### Types Hints
If needed, as part of code-readability and good-practice, we can introduce type-hints, so that python behaves like a statically typed language and we can avoid errors by using the `typing` module. You can refer more in this [cheat sheet](https://mypy.readthedocs.io/en/stable/cheat_sheet_py3.html)
```python
from typing import List, Set, Dict, Tuple, Optional
```

### Operators
**Arithmetic operators**: `+` (add), `-` (subtract), `*` (multiply), `/` (true division), `//` (floor division), `%` (modulo), and `**` (power).

**Assignment Operators:** Are used to assign values. `+=` (add & assign), `-+` (subtract & assign), `*=` (multiply & assign), `/=` or `//=` (divide & assign).

**Comparison operators:** include `<`, `<=`, `>`, `>=`, ``
equal and `!=` (not equal). `is` and `is not` test object identity, not value equality. Comparisons can be **chained** (e.g. `1 < x <= 5` is like `1 < x and x <= 5`).

**Logical operators**: `and`, `or`, `not` combine Boolean values (with short-circuit evaluation). There are also **bitwise operators** for integers: `&` (and), `|` (or), `^` (xor), `~` (not), `<<` (left shift), `>>` (right shift). (Bitwise ops act on the two’s-complement binary representation of integers.

**Identity operators:** `is` and `is not` check whether values are identical or not.

**Membership operators:** `in` and `not in` check if a value is contained in a container (sequence, set, or other iterable).
```python
# Arithmetic and comparisons
a = 7; b = 3
print(a + b, a - b, a * b, a / b)   # 10 4 21 2.3333...
print(a // b, a % b, a ** b)         # 2 1 343
print(a > b, a == 7, b != 4)         # True True True

# Logical and membership
print( (a > b) and (b > 0) )        # True
print(10 in [5, 7, 10])            # True

# Bitwise
print(bin(a), bin(b))
print(a & b, a | b, a << 1, b >> 1) # bitwise and, or, shifts

'0b{:04b}'.format(0b1100 & 0b1010) # '0b1000' and
'0b{:04b}'.format(0b1100 | 0b1010) # '0b1110' or
'0b{:04b}'.format(0b1100 ^ 0b1010) # '0b0110' exclusive or
'0b{:04b}'.format(0b1100 >> 2)     # '0b0011' shift right
'0b{:04b}'.format(0b0011 << 2)     # '0b1100' shift left
```

### Flow Control and Logic
**Conditional statements** use `if`, `elif`, and `else`:
```python
# if-elif-else
if x < 0:
    print("Negative")
elif x == 0:
    print("Zero")
else:
    print("Positive")
    
# ternary operator
a, b = 10, 20
min = a if a < b else b
print(min) # 10
```
Python tests _truthiness_ of expressions in `if` or `while`; many objects (nonzero numbers, non-empty strings/sequences) are true, and empty or zero ones are false. **Ternary operator:** Another way of writing conditional expression:

**Loops**: use `for` to iterate over a sequence or other iterable, and `while` for conditional looping:
```python
for item in [1,2,3]:
    print(item)

i = 0
while i < 3:
    print(i)
    i += 1
```
You can use `break` to exit a loop early, and `continue` to skip to the next iteration. `pass` can be used as a placeholder in the loop.

**Advanced Loops** (`for...else`, `while...else`)
The `else` block in a loop executes only if the loop terminates normally (i.e., not via a `break` statement). This can be useful for search operations.

**Pattern Matching**: Python 3.10 introduced `match`/`case` for structural pattern matching, similar to a switch/case but more powerful. This allows matching on types, shapes of data (like sequences or class instances), etc. Example:
```python
match value:
    case 0:
        print("Zero")
    case [x, y]:
        print(f"Got a two-element list: {x}, {y}")
    case _:
        print("Something else")
```
Pattern matching lets you concisely branch on complex data structures.

**Comprehensions** provide concise loops to build lists, sets, or dicts:
```python
evens = [x*x for x in range(6) if x % 2 == 0]  # list of squares [0,4,16]
unique = {c for c in "abracadabra"}           # set of letters {'a','b','r','c','d'}
squares = {x: x*x for x in range(5)}          # dict {0:0, 1:1, 2:4, 3:9, 4:16}
```

## Section 2: Built-In Data Structures in Python
Python provides several powerful built-in data structures to store, manipulate, and manage data efficiently. They are **Lists**, **Tuples**, **Dictionaries**, **Sets**, and **Strings**.

### 1. Lists
Lists are **ordered**, **mutable**, and can contain **heterogeneous** elements. A **list** in Python is one of the most versatile and commonly used data structures. It is an **ordered**, **mutable**, and **dynamic** collection that can hold elements of **different data types**, including other lists or objects. Lists allow for **index-based access**, meaning each element can be accessed or modified directly using its position (index).  

They support a wide range of operations — from **adding**, **removing**, and **sorting** elements to **comprehensions** for quick list creation.  
Lists in Python internally use **dynamic arrays**, meaning they automatically resize when items are added or removed, though this can involve copying elements to new memory blocks internally for efficiency.

```python
# Creating lists
fruits = ["apple", "banana", "cherry"]
mixed = [1, "hello", 3.14, True]

# Accessing elements (indexing)
print(fruits[0])     # apple
print(fruits[-1])    # cherry

# Slicing
print(fruits[0:2])   # ['apple', 'banana']

# Modifying elements (mutable)
fruits[1] = "blueberry"
print(fruits)        # ['apple', 'blueberry', 'cherry']

# list comprehension
squares = [x**2 for x in range(5)]
print(squares)  # [0, 1, 4, 9, 16]
```

##### Indexing and Slicing in Python
Both **indexing** and **slicing** are fundamental concepts that work not just on lists, but also on strings, tuples, and other sequences.

**Indexing** is used to access a single element using its position (index number).  
Python uses **zero-based indexing**, meaning:
- The **first element** has index `0`
- The **last element** has index `-1` (negative indices count backward)

**Slicing** is used to extract **a portion of a sequence** (sublist, substring, etc.).  
It uses the syntax: `sequence[start:end:step]`
- **start** → index where slicing begins (inclusive)
- **end** → index where slicing stops (exclusive)
- **step** → interval between elements (default = 1)

```python
                +---+---+---+---+---+---+
                | P | y | t | h | o | n |
                +---+---+---+---+---+---+
Slice position: 0   1   2   3   4   5   6
Index position:   0   1   2   3   4   5
p = ['P','y','t','h','o','n']
p[0] 'P' # indexing gives items, not lists
alpha[slice(2,4)] # equivalent to p[2:4]

# example
nums = [10, 20, 30, 40, 50]

# indexing
print(nums[0])   # 10
print(nums[-1])  # 50

# slicing
print(nums[1:4])     # [20, 30, 40]
print(nums[:3])      # [10, 20, 30]
print(nums[::2])     # [10, 30, 50]
print(nums[::-1])    # [50, 40, 30, 20, 10] (reversed list)
```

##### Features of Lists

| Property               | Description                         |
| ---------------------- | ----------------------------------- |
| **Ordered**            | Yes (Preserves insertion order)     |
| **Mutable**            | Yes (Can be changed after creation) |
| **Allows duplicates**  | Yes                                 |
| **Heterogeneous**      | Yes                                 |
| **Index-based access** | Yes (0-based indexing)              |

##### Common List Methods

| **Method**         | **Description**                                                                                       | **Example**        |
| ------------------ | ----------------------------------------------------------------------------------------------------- | ------------------ |
| `append(x)`        | Adds item `x` to the end of the list.                                                                 | `L.append(4)`      |
| `extend(iterable)` | Extends the list by appending all items from `iterable`.                                              | `L.extend([5, 6])` |
| `insert(i, x)`     | Inserts item `x` at a given position `i`.                                                             | `L.insert(0, 'a')` |
| `remove(x)`        | Removes the _first_ item from the list whose value is `x`.                                            | `L.remove('a')`    |
| `pop(i)`           | Removes and _returns_ the item at position `i`. If `i` is omitted, removes and returns the last item. | `item = L.pop()`   |
| `clear()`          | Removes all items from the list.                                                                      | `L.clear()`        |
| `index(x)`         | Returns the 0-based index of the _first_ item whose value is `x`.                                     | `i = L.index(3)`   |
| `count(x)`         | Returns the number of times `x` appears in the list.                                                  | `c = L.count(2)`   |
| `sort()`           | Sorts the items of the list **in-place**.                                                             | `L.sort()`         |
| `reverse()`        | Reverses the elements of the list **in-place**.                                                       | `L.reverse()`      |
| `copy()`           | Returns a _shallow copy_ of the list.                                                                 | `new_L = L.copy()` |

##### Example Usage:
```python
nums = [4, 2, 9, 1]
nums.sort()
print(nums)          # [1, 2, 4, 9]
nums.reverse()
print(nums)          # [9, 4, 2, 1]
```

### 2. Arrays
While **lists** can store mixed data types, **arrays** (from the `array` module) are designed for **homogeneous data** (same type elements).  
They provide **faster performance** and **lower memory consumption** when dealing with large numerical data. Arrays are especially useful when you want C-style contiguous memory storage and numerical operations without the overhead of lists.

```python
from array import array
arr = array('i', [1, 2, 3])
print(arr[1])  # 2
```
Each array must have a **type code** (like `'i'` for integer, `'f'` for float), which defines the type of its elements.

|Type Code|C Type|Python Type|Example|
|---|---|---|---|
|`'b'`|signed char|int|-128 to 127|
|`'B'`|unsigned char|int|0 to 255|
|`'i'`|signed int|int|typical int range|
|`'f'`|float|float||
|`'d'`|double|float||
Arrays don’t support all list methods (like `insert` or mixed data types), but they support indexing, slicing, and iteration efficiently.
##### Lists vs Arrays in Python
| Feature           | `list`                    | `array.array`                                |
| ----------------- | ------------------------- | -------------------------------------------- |
| **Data Type**     | Can hold mixed types      | Must hold same type                          |
| **Performance**   | Slightly slower           | More memory-efficient for large numeric data |
| **Import Needed** | No                        | Yes (`from array import array`)              |
| **Use Case**      | General-purpose container | Numeric computation / fixed type data        |

### Tuples
A **tuple** is an **ordered**, **immutable** sequence of values. Once created, its elements **cannot be changed**, which makes tuples **hashable** and usable as keys in dictionaries or elements in sets.  
Tuples are faster than lists due to their immutability and are often used for **fixed collections** of items — such as coordinates, database records, or constant data.

Tuples are created using parentheses `()` and can contain heterogeneous elements. If only one element is needed, remember to include a comma (`t = (5,)`) to define it as a tuple.

```python
# Creating tuples
t1 = (1, 2, 3)
t2 = ("a", "b", "c")

# Indexing & slicing
print(t1[0])     # 1
print(t1[1:3])   # (2, 3)

# Concatenation
print(t1 + t2)   # (1, 2, 3, 'a', 'b', 'c')

# immutability
t = (1, 2, 3)
# t[1] = 99  ❌ TypeError
```

##### Tuple Packing & Unpacking
Tuples can be packed and unpacked into atomic values even in loops and `enumerate` is one such function which helps iterate by packing tuples of `(index, value)`

```python
person = ("Hatim", 24, "India")
name, age, country = person
print(name, age, country)
```

##### Features of Tuples
| Property               | Description                                    |
| ---------------------- | ---------------------------------------------- |
| **Ordered**            | Yes                                            |
| **Mutable**            | No (Tuple and its elements both are immutable) |
| **Allows duplicates**  | Yes                                            |
| **Index-based access** | Yes                                            |
| **Heterogeneous**      | Yes                                            |

##### Common Tuple Methods
All the list methods except the ones that try to mutate the list are also available on tuples, there are only 2 unique methods:

| **Method** | **Description**                                                   | **Example**     |
| ---------- | ----------------------------------------------------------------- | --------------- |
| `count(x)` | Returns the number of times `x` appears in the tuple.             | `t.count('a')`  |
| `index(x)` | Returns the 0-based index of the _first_ item whose value is `x`. | `t.index(3.14)` |

##### Example Usage
```python
t = (1, 2, 2, 3)
print(t.count(2))  # 2
print(t.index(3))  # 3
```


### Dictionaries / HashMaps
A **dictionary** in Python is a powerful **key-value pair** data structure used for **mapping unique keys to values**. It’s **mutable**, **unordered (before 3.7)**, and optimized for **fast lookups, insertions, and deletions** using a **hash table** internally. Each key in a dictionary must be **immutable** (e.g., strings, numbers, tuples), while values can be of **any type** (even other dictionaries or lists).

```python
student = {"name": "Alice", "age": 22, "marks": 95}
print(student["name"])        # Alice
student["age"] = 23           # modify value
student["city"] = "Mumbai"    # add new key-value

# dict comprehension
squares = {x: x**2 for x in range(5)}
print(squares)  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

Python 3.7+ preserves insertion order, meaning items retain the order they were added — a feature heavily used in modern APIs and data models.

##### Features of Dictionaries
| Property               | Description                                   |
| ---------------------- | --------------------------------------------- |
| **Ordered**            | Yes (Python 3.7+)                             |
| **Mutable**            | Yes: Values, No: keys are Immutable           |
| **Allows Duplicates**  | Yes: Values, No: Keys must be unique          |
| **Index-based access** | No, access through keys                       |
| **Heterogeneous**      | Value: Any Type, Keys: int, str or tuple only |

##### Common Dict Methods

| **Method**                 | **Description**                                                                                                                               | **Example**                        |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| `keys()`                   | Returns a _view object_ displaying a list of all keys.                                                                                        | `my_dict.keys()`                   |
| `values()`                 | Returns a _view object_ displaying a list of all values.                                                                                      | `my_dict.values()`                 |
| `items()`                  | Returns a _view object_ displaying a list of key-value tuple pairs.                                                                           | `my_dict.items()`                  |
| `get(key, default)`        | Returns the value for `key`. If `key` is not found, returns `default` (or `None`).                                                            | `my_dict.get('age', 0)`            |
| `pop(key, default)`        | Removes and returns the value for `key`. If not found, returns `default`. Raises `KeyError` if `key` not found and `default` is not provided. | `my_dict.pop('name')`              |
| `popitem()`                | Removes and returns the _last_ inserted (key, value) pair as a tuple.                                                                         | `my_dict.popitem()`                |
| `update(other_dict)`       | Updates the dictionary with key-value pairs from `other_dict`, overwriting existing keys.                                                     | `my_dict.update({'city': 'LA'})`   |
| `setdefault(key, default)` | If `key` is in dict, returns its value. If not, inserts `key` with a value of `default` and returns `default`.                                | `my_dict.setdefault('job', 'Dev')` |
| `clear()`                  | Removes all items from the dictionary.                                                                                                        | `my_dict.clear()`                  |
| `copy()`                   | Returns a _shallow copy_ of the dictionary.                                                                                                   | `new_d = my_dict.copy()`           |
| `fromkeys(seq, v)`         | Creates a new dictionary with keys from `seq` and all values set to `v` (default `None`).                                                     | `dict.fromkeys(['a', 'b'], 1)`     |
##### Example Usage:
```python
student = {"name": "Bob", "marks": 88}
student.update({"age": 21})
print(student.items())  # dict_items([('name', 'Bob'), ('marks', 88), ('age', 21)])
```


### Sets
A **set** is an **unordered**, **mutable**, and **unindexed** collection of **unique elements**.  
They’re primarily used to perform **mathematical set operations** like union, intersection, and difference efficiently. Sets automatically eliminate duplicates and can only contain **hashable (immutable)** items.

```python
# Creating sets
s = {1, 2, 3, 3}
print(s)  # {1, 2, 3}

# set comprehension
squares = {x**2 for x in range(6)}
print(squares)  # {0, 1, 4, 9, 16, 25}
```

They are ideal for:
- Removing duplicates from data.
- Membership testing (`in` is O(1) on average).
- Performing mathematical operations between datasets.

Under the hood, sets use a **hash table**, similar to dictionaries, but only store keys (no values).

##### Features of Sets
| Property               | Description                                                            |
| ---------------------- | ---------------------------------------------------------------------- |
| **Ordered**            | No, set is unorderd                                                    |
| **Mutable**            | Yes (The set itself is mutable), No: Elements in the set are immutable |
| **Allows Duplicates**  | No, all elements must be unique                                        |
| **index-based access** | No indexing or slicing                                                 |
| **Heterogeneous**      | Yes                                                                    |

##### Common Set Methods
| **Method (Mutating)**         | **Description**                                                               |
| ----------------------------- | ----------------------------------------------------------------------------- |
| `add(x)`                      | Adds element `x` to the set.                                                  |
| `update(iterable)`            | Adds all elements from `iterable` to the set.                                 |
| `remove(x)`                   | Removes element `x`. Raises `KeyError` if not found.                          |
| `discard(x)`                  | Removes element `x` if it is present.                                         |
| `pop()`                       | Removes and returns an _arbitrary_ element from the set.                      |
| `clear()`                     | Removes all elements from the set.                                            |
| **Method (Non-Mutating)**     | **Description**                                                               |
| `union(other)`                | Returns a new set with all elements from both (same as `                      |
| `intersection(other)`         | Returns a new set with elements common to both (same as `&`).                 |
| `difference(other)`           | Returns a new set with elements in this set but not in `other` (same as `-`). |
| `symmetric_difference(other)` | Returns a new set with elements in either set, but not both (same as `^`).    |
| `issubset(other)`             | Returns `True` if this set is a subset of `other` (same as `<=`).             |
| `issuperset(other)`           | Returns `True` if this set is a superset of `other` (same as `>=`).           |
| `isdisjoint(other)`           | Returns `True` if the two sets have no intersection.                          |
| `copy()`                      | Returns a _shallow copy_ of the set.                                          |
##### Set Operations
Just like mathematical sets, sets in python can perform the common set operation such as: union, intersection, diff and symmetric diff.
```python
a = 3
st = set()
st.add(a) # Add to st
st.remove(a) # Remove from st
st.discard(a) # Removes from set with no error
st.add(a) # Add to st
next(iter(s)) # return 3 without removal
st.pop() # returns 3

# ---------------------------------
# set operations
a = {1, 2, 3}
b = {3, 4, 5}

print(a | b)  # Union → {1, 2, 3, 4, 5}
print(a & b)  # Intersection → {3}
print(a - b)  # Difference → {1, 2}
print(a ^ b)  # Symmetric difference → {1, 2, 4, 5
```


### Strings
A **string** in Python is an **immutable sequence of Unicode characters**.  
Strings are one of the most fundamental data types and are heavily used in almost every application, from user input to file processing, web data, and text analytics. Being immutable means that any modification creates a **new string object**, the original string remains unchanged. Python provides a rich set of **string methods** and supports **indexing, slicing, iteration**, and **formatting** with remarkable ease.

Internally, strings are stored as arrays of Unicode code points, allowing them to handle multilingual text seamlessly.  
They can also be encoded into bytes for low-level operations like network transmission or file I/O.

```python
text = "Hello, Python!"
print(text[0])      # H
print(text[-1])     # !
print(text[0:5])    # Hello

# string immutability
s = "Python"
# s[0] = "J"  ❌ Error
s = "J" + s[1:]  # ✅ Create new string
print(s)  # Jython

```

##### Features of Strings
| Property               | Description                                                      |
| ---------------------- | ---------------------------------------------------------------- |
| **Ordered**            | Yes                                                              |
| **Mutable**            | No, the string itself is mutable, but its elements are immutable |
| **Allows Duplicates**  | Yes                                                              |
| **Indexing & slicing** | Yes, indexing and slicing both are supported                     |
| **Heterogeneous**      | No, only str / char types                                        |

##### Common String Methods

| **Category**            | **Method**                | **Description**                                                                |
| ----------------------- | ------------------------- | ------------------------------------------------------------------------------ |
| **Case**                | `upper()`                 | Converts string to uppercase.                                                  |
|                         | `lower()`                 | Converts string to lowercase.                                                  |
|                         | `capitalize()`            | Converts first character to uppercase, rest to lowercase.                      |
|                         | `title()`                 | Converts first character of each word to uppercase.                            |
|                         | `swapcase()`              | Swaps case (lowercase becomes upper, and vice versa).                          |
| **Splitting / Joining** | `split(sep)`              | Returns a _list_ of words, split by `sep` (default is whitespace).             |
|                         | `rsplit(sep)`             | Same as `split`, but starts from the right.                                    |
|                         | `splitlines()`            | Returns a list of lines, splitting at line breaks.                             |
|                         | `join(iterable)`          | Joins elements of `iterable` (e.g., a list) _using the string as a separator_. |
| **Stripping**           | `strip(chars)`            | Removes leading/trailing characters (default whitespace).                      |
|                         | `lstrip(chars)`           | Removes _leading_ characters.                                                  |
|                         | `rstrip(chars)`           | Removes _trailing_ characters.                                                 |
| **Search / Find**       | `find(sub)`               | Returns lowest index of `sub`. Returns **-1** if not found.                    |
|                         | `index(sub)`              | Same as `find()`, but raises **ValueError** if not found.                      |
|                         | `rfind(sub)`              | Returns highest index of `sub`. Returns -1 if not found.                       |
|                         | `rindex(sub)`             | Same as `rfind()`, but raises ValueError if not found.                         |
|                         | `count(sub)`              | Returns number of non-overlapping occurrences of `sub`.                        |
| **Check / Validate**    | `startswith(pre)`         | Returns `True` if string starts with prefix `pre`.                             |
|                         | `endswith(suf)`           | Returns `True` if string ends with suffix `suf`.                               |
|                         | `isdigit()`               | Returns `True` if all characters are digits.                                   |
|                         | `isalpha()`               | Returns `True` if all characters are alphabetic.                               |
|                         | `isalnum()`               | Returns `True` if all characters are alphanumeric (letters or numbers).        |
|                         | `islower()`               | Returns `True` if all cased characters are lowercase.                          |
|                         | `isupper()`               | Returns `True` if all cased characters are uppercase.                          |
|                         | `isspace()`               | Returns `True` if all characters are whitespace.                               |
| **Modification**        | `replace(old, new)`       | Returns a copy with all occurrences of `old` replaced by `new`.                |
|                         | `center(width, fill)`     | Returns a centered string of `width`, padded with `fill` char.                 |
|                         | `ljust(width, fill)`      | Left-justifies the string.                                                     |
|                         | `rjust(width, fill)`      | Right-justifies the string.                                                    |
|                         | `zfill(width)`            | Pads string on the left with '0' to fill `width`.                              |
| **Formatting**          | `format(*args, **kwargs)` | Performs a string formatting operation (the "old" way).                        |
| **Encoding**            | `encode(enc)`             | Encodes the string into a `bytes` object using `enc` (e.g., 'utf-8').          |

##### Example Usage:
```python
name = "hatim"
print(name.capitalize())         # Hatim
print(" ".join(["Hello", "World"]))  # Hello World

txt = "Hello, welcome to my world."
x = txt.find("welcome")  # 7

str = "this is string example....wow!!!"
str.endswith("!!") # True
str.startswith("this") # True
str.endswith("is", 2, 4) # True


# reverse sentences using split, slicing, and join:
s = "the sky is blue"
wordsWithoutWhitespace = s.split() # ['the', 'sky', 'is', 'blue']
reversedWords = wordsWithoutWhitespace[::-1] # ['blue', 'is', 'sky', 'the']
s = " ".join(reversedWords) # blue is sky the
```

##### String Formatting
```python
name = "Alice"
age = 25

# classic syntax using .format()
print("My name is {} and I am {} years old.".format(name, age))

# new syntax using f-strings
print(f"My name is {name} and I am {age} years old.")

# multiple f-strings
name = "Eric"
profession = "comedian"
affiliation = "Monty Python"
message = (
     f"Hi {name}. "
     f"You are a {profession}. "
     f"You were in {affiliation}."
)
message
'Hi Eric. You are a comedian. You were in Monty Python.'
```


## Section 3: Advanced Data Structures in Python
While Python provides high-level built-in data structures like **lists**, **sets**, and **dictionaries**, sometimes we need **custom data structures** to solve specific algorithmic problems efficiently. These structures can be implemented manually or using modules like `collections` and `queue`.

### 1. Stack
A **stack** is a linear data structure that follows the **Last-In, First-Out (LIFO)** principle — the last inserted element is removed first.  
Stacks are used in function calls, undo mechanisms, expression evaluation, and backtracking algorithms.
##### Implementation
In python, stacks can be implemented easily using the built-in `list` class:
```python
stack = []

# Push elements
stack.append(10)
stack.append(20)
stack.append(30)

print(stack)  # [10, 20, 30]

# Pop element
top = stack.pop()
print(top)    # 30
print(stack)  # [10, 20]

# Peek top element
print(stack[-1])  # 20
```
##### Alternative
Using `collections.deque` (More Efficient), `deque` provides O(1) append and pop operations from both ends:
```python
from collections import deque

stack = deque()
stack.append(10)
stack.append(20)
stack.pop()   # removes 20
```

### 2. Queue
A **queue** is a linear data structure that follows the **First-In, First-Out (FIFO)** principle — elements are removed in the order they are inserted. Queues are used in scheduling, order processing, and BFS traversal of graphs.
##### Implementation 
Queues in Python can be easily implemented using the `collections.deque` class:
```python
from collections import deque

queue = deque()

# Enqueue
queue.append('A')
queue.append('B')
queue.append('C')
print(queue)  # deque(['A', 'B', 'C'])

# Dequeue
queue.popleft()  # Removes 'A'
print(queue)     # deque(['B', 'C'])
```
##### Alternative
Else, there is a separate `queue.Queue` which is more thread-safe:
```python
from queue import Queue

q = Queue()
q.put(10)
q.put(20)
q.put(30)

print(q.get())  # 10
```

### 3. Linked List
A **linked list** is a linear collection of nodes where each node points to the next node. Unlike lists, linked lists don’t store elements in contiguous memory — they are **dynamic** and efficient for frequent insertions/deletions.

##### Implementation (Singly Linked List)
There is no existing implementation for linked lists so they have to be made:
```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def append(self, data):
        new_node = Node(data)
        if not self.head:
            self.head = new_node
            return
        curr = self.head
        while curr.next:
            curr = curr.next
        curr.next = new_node

    def display(self):
        curr = self.head
        while curr:
            print(curr.data, end=" -> ")
            curr = curr.next
        print("None")

# Usage
ll = LinkedList()
ll.append(10)
ll.append(20)
ll.append(30)
ll.display()   # 10 -> 20 -> 30 -> None
```

### 4. Binary Tree
A **binary tree** is a hierarchical data structure where each node has **at most two children** — `left` and `right`. It’s used for organizing hierarchical data, expression trees, and as the base for Binary Search Trees (BSTs).

A **Binary Search Tree** is a binary tree with an ordering property:
- The left subtree of a node contains only values **less than** the node’s key.
- The right subtree contains only values **greater than** the node’s key.
BSTs provide **O(log n)** time complexity for search, insertion, and deletion (on average).
##### Implementation
Similarly, trees have to be made custom in python, here is a simple implementation:
```python
# Binary Tree
class Node:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

def inorder(root):
    if root:
        inorder(root.left)
        print(root.key, end=" ")
        inorder(root.right)

# Usage
root = Node(10)
root.left = Node(5)
root.right = Node(20)
root.left.left = Node(3)

inorder(root)  # 3 5 10 20

# ---------------------------

# Binary Search Tree
class BSTNode:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

def insert(root, key):
    if root is None:
        return BSTNode(key)
    if key < root.key:
        root.left = insert(root.left, key)
    else:
        root.right = insert(root.right, key)
    return root

def search(root, key):
    if root is None or root.key == key:
        return root
    return search(root.left, key) if key < root.key else search(root.right, key)

# Usage
root = insert(None, 50)
insert(root, 30)
insert(root, 70)
insert(root, 20)

found = search(root, 30)
print(found.key if found else "Not Found")  # 30
```

### 6. Graphs
A **graph** is a collection of **nodes (vertices)** and **edges** connecting them.  
Graphs can be **directed** or **undirected**, and are used in social networks, navigation systems, and dependency modeling.

##### Implementation
Graphs can be implemented using either adjacency lists or adjacency matrix, here is a simple implementation using Adjacency List:
```python
class Graph:
    def __init__(self):
        self.graph = {}

    def add_edge(self, u, v):
        self.graph.setdefault(u, []).append(v)

    def show(self):
        for node, edges in self.graph.items():
            print(f"{node} -> {edges}")

# Usage
g = Graph()
g.add_edge('A', 'B')
g.add_edge('A', 'C')
g.add_edge('B', 'D')
g.show()
# A -> ['B', 'C']
# B -> ['D']

# -------------------------------------------
# Traversal Example: Breadth-First Search
from collections import deque

def bfs(graph, start):
    visited = set()
    q = deque([start])
    while q:
        node = q.popleft()
        if node not in visited:
            print(node, end=" ")
            visited.add(node)
            q.extend(graph.get(node, []))

# BFS traversal
bfs(g.graph, 'A')  # A B C D
```

### 7. Heaps (Priority Queue)
A **heap** is a complete binary tree where each node satisfies the **heap property**:
- **Min-Heap:** Parent ≤ Children
- **Max-Heap:** Parent ≥ Children
Heaps are used in priority queues, scheduling, and algorithms like Dijkstra’s and Heap Sort.
##### Implementation
Heaps can be implemented easily in python by importing `heapq` which by defaults implements a min-heap:
```python
import heapq

# min heap - default
nums = [5, 1, 9, 3, 7]
heapq.heapify(nums)        # Convert list to min-heap
heapq.heappush(nums, 0)    # Add element
print(heapq.heappop(nums)) # Remove smallest → 0
print(nums)                # Heap remains ordered internally

l = heapq.nlargest(3, nums) # extract nth largest element
s = heapq.nsmallest(3, nums) # extract nth smallest element

# -------------------------------
# max heap (use negative of the element while storing)
max_heap = []
for n in [5, 1, 9]:
    heapq.heappush(max_heap, -n)
print(-heapq.heappop(max_heap))  # 9
```


## Section 4: Advanced Programming Constructs
This section explores Python's powerful functional and procedural programming constructs, which enable flexible, reusable, and robust code. These features represent a spectrum of metaprogramming, allowing code to inspect, modify, or generate other code at runtime.

### Scope (LEGB Rule)
Python resolves names using the LEGB rule, searching in the following order:
1. Local: The current function's scope.
2. Enclosing: The scope of any enclosing functions (e.g., in nested functions).
3. Global: The top-level module scope.
4. Built-in: Python's built-in names like `len()`, `list`, etc.

### Functions
Functions encapsulate reusable code. Define a function with `def` or an anonymous function with `lambda`.
##### Function Structure
- `def` defines a named function with parameters.
- **Default arguments** (`param2=default`) are optional values if caller omits them.
- `*args` collects extra positional arguments as a tuple, and `**kwargs` collects extra keyword arguments as a dict.
- Use `return` to send back a value (or omit it to return `None`)
```python
def func_name(param1, param2=default, *args, **kwargs):
    """Optional docstring."""
    # ... code ...
    return result

# example
def greet(name, shout=False):
    """Return a greeting."""
    if shout:
        return f"HELLO, {name.upper()}!"
    return f"Hello, {name}."

print(greet("Bob"))            # Hello, Bob.
print(greet("Alice", shout=True))  # HELLO, ALICE!
```

##### Lambda Functions
You can also define **lambda** (anonymous) functions for short one-liners, e.g. `add = lambda x, y: x+y`. These are often used where functions need other functions as arguments, or a temporary function use-case is needed without defining the function permanently.

```python
# lambda used with map
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x**2, numbers))
print(squared)  

# output:
# [1, 4, 9, 16, 25]
```

### Variable-Length Arguments
The special `*` and `**` syntax provides a powerful way to handle a variable number of arguments in functions.
##### In Function Definitions
- `*args`: Gathers any number of positional arguments into a tuple. The name `args` is a convention; any name can be used (e.g., `*numbers`).
- `**kwargs`: Gathers any number of keyword arguments into a dictionary. The name `kwargs` is also a convention.
- **Parameter Order:** The correct order of parameters in a function definition is: standard positional arguments, `*args`, keyword-only arguments, and finally `**kwargs`.
##### As Unpacking Operators in Function Calls
The `*` and `**` operators can also be used to unpack iterables and dictionaries when calling a function, passing their contents as individual arguments.

### Closures
A closure is a nested function that captures and remembers the state of variables from its enclosing (non-global) scope, even after the outer function has completed execution. This is a powerful mechanism for creating function factories and encapsulating state without resorting to classes.

To create a closure, three conditions must be met:
1. There must be a nested function.
2. The nested function must refer to a variable from its enclosing scope.
3. The enclosing function must return the nested function.

```python
def outer_function(msg):
    """Outer function defines a variable and returns an inner function."""
    def inner_function():
        print("Message from closure:", msg)
    return inner_function  # Returning inner function without calling it

# Create closure
greet = outer_function("Hello, Python!")
greet()  # ✅ Prints: Message from closure: Hello, Python!

```

### Decorators
A decorator is a design pattern in Python that allows you to add new functionality to an existing function or method without modifying its source code. It is syntactic sugar for a higher-order function that takes a function as an argument and returns a new function.
- **Implementation and `*args`, `**kwargs`** Decorators are typically implemented using a nested `wrapper` function that forms a closure. To make a decorator generic, the wrapper should accept `*args` and `**kwargs` to handle any arguments passed to the decorated function.
- **Preserving Metadata with `@functools.wraps`** A crucial best practice is to use the `@functools.wraps` decorator on the wrapper function. This preserves the original function's metadata (like its name, docstring, and annotations), which is essential for debugging and introspection.

```python
def my_decorator(func):
    def wrapper():
        print("Before function execution 👇")
        func()
        print("After function execution 👆")
    return wrapper

@my_decorator  # This is equivalent to: say_hello = my_decorator(say_hello)
def say_hello():
    print("Hello, World!")

say_hello()

# Output:
# Before function execution 👇
# Hello, World!
# After function execution 👆
```

### Iterators, Generators & Built-in Functions
##### **The Iterator Protocol**
The iterator protocol is fundamental to how `for` loops work in Python. An object is an _iterable_ if it implements the `__iter__()` method, which must return an _iterator_ object. An iterator is an object that implements the `__next__()` method, which returns the next item in the sequence and raises a `StopIteration` exception when there are no more items.

```python
class CountDown:
    def __init__(self, start):
        self.current = start

    def __iter__(self):
        return self  # The iterator object

    def __next__(self):
        if self.current <= 0:
            raise StopIteration
        num = self.current
        self.current -= 1
        return num

# Usage
for i in CountDown(5):
    print(i)
```

##### **Generators**
Generators provide a convenient way to implement the iterator protocol.
- **Generator Functions:** A function that contains one or more `yield` statements. When called, it returns a generator object (an iterator), but its code does not execute immediately. The code runs each time `__next__()` is called on the generator, executing until it hits a `yield`, which pauses execution and returns the yielded value. This allows for lazy evaluation, which is highly memory-efficient for large datasets.
- **Generator Expressions:** A concise, memory-efficient syntax for creating generators, similar to list comprehensions but with parentheses instead of square brackets.

```python
def countdown(n):
    print("Starting countdown...")
    while n > 0:
        yield n  # Pauses here and resumes on next() call
        n -= 1
    print("Done!")

# Using the generator
for number in countdown(3):
    print(number)
```

### Built-in Functions
Python has many **built-in functions and types** that are always available. Common ones include:

| **Function(s)**                                       | **Description / Purpose**                                                                                                                                  |
| ----------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `print()`                                             | Outputs data to the console. Accepts multiple arguments, supports `sep`, `end`, and `file` parameters.                                                     |
| `input()`                                             | Reads a line of input from the user as a string.                                                                                                           |
| `len()`                                               | Returns the number of items in an iterable (string, list, tuple, dict, etc.).                                                                              |
| `type()`                                              | Returns the data type of an object.                                                                                                                        |
| `id()`                                                | Returns the unique identifier (memory address) of an object.                                                                                               |
| `isinstance(obj, class)` / `issubclass(sub, super)`   | Check object type or subclass relationship.                                                                                                                |
| `dir()`                                               | Lists all valid attributes and methods for an object.                                                                                                      |
| `eval()` / `exec()` / `compile()`                     | `eval()` executes an expression, `exec()` executes Python code dynamically, and `compile()` compiles code to a code object. ⚠️ Use carefully for security. |
| `hash()`                                              | Returns the hash value of an object (if hashable). Used in sets/dict keys.                                                                                 |
| `repr()` / `str()` / `ascii()`                        | Return string representations: `repr()` → developer-readable, `str()` → user-readable, `ascii()` → escapes non-ASCII characters.                           |
| `format()`                                            | Returns a formatted version of a string or number. Similar to f-strings but as a function.                                                                 |
| `abs()`                                               | Returns the absolute value of a number.                                                                                                                    |
| `round(number, ndigits)`                              | Rounds a number to a given precision.                                                                                                                      |
| `sum(iterable[, start])`                              | Returns the sum of all items in an iterable, with optional start value.                                                                                    |
| `min(iterable)` / `max(iterable)`                     | Return the smallest/largest item in an iterable or among arguments.                                                                                        |
| `sorted(iterable, key=None, reverse=False)`           | Returns a new sorted list. Does not modify the original.                                                                                                   |
| `all(iterable)`                                       | Returns `True` if all elements are truthy.                                                                                                                 |
| `any(iterable)`                                       | Returns `True` if at least one element is truthy.                                                                                                          |
| `enumerate(iterable, start=0)`                        | Returns an iterator yielding pairs of (index, value). Often used in loops.                                                                                 |
| `zip(*iterables)`                                     | Aggregates elements from multiple iterables into tuples.                                                                                                   |
| `map(function, iterable)`                             | Applies a function to every item of an iterable. Returns an iterator.                                                                                      |
| `filter(function, iterable)`                          | Filters items from iterable for which the function returns `True`.                                                                                         |
| `reversed(seq)`                                       | Returns a reversed iterator over a sequence.                                                                                                               |
| `range(start, stop[, step])`                          | Returns an immutable sequence of numbers from start to stop with step. Commonly used in loops.                                                             |
| `next(iterator, default)`                             | Returns the next item from an iterator. Returns `default` if no more items.                                                                                |
| `iter(obj[, sentinel])`                               | Returns an iterator object. With a sentinel, repeatedly calls a function until sentinel value is returned.                                                 |
| `chr(i)` / `ord(c)`                                   | `chr()` converts an integer to a Unicode character; `ord()` does the reverse.                                                                              |
| `bin()`, `oct()`, `hex()`                             | Convert an integer to binary, octal, or hexadecimal string representation.                                                                                 |
| `int(x[, base])`, `float(x)`, `complex(real, imag)`   | Convert to numeric types.                                                                                                                                  |
| `bool(x)`                                             | Converts a value to `True` or `False` according to truthiness rules.                                                                                       |
| `list()`, `tuple()`, `set()`, `frozenset()`, `dict()` | Constructors for built-in data structures.                                                                                                                 |
| `bytes()`, `bytearray()`, `memoryview()`              | Used for handling binary data.                                                                                                                             |
| `classmethod()` / `staticmethod()`                    | Define class-level methods that are bound differently than instance methods.                                                                               |
| `super()`                                             | Returns a proxy object that delegates method calls to a parent or sibling class.                                                                           |
| `object()`                                            | Returns a new, featureless base object. Base of all new-style classes.                                                                                     |
| `frozenset()`                                         | Immutable version of a set (can be dictionary key).                                                                                                        |


## Section 5: Exception & File Handling
### Exception Handling
Errors in Python can be of 2 types: Syntax Errors & Exceptions.
1. **Syntax Error** as the name suggests, is caused by wrong syntax in the code. It leads to the termination of the program.
2. **Exceptions** are raised when the program is syntactically correct, but the code resulted in an error. This error does not stop the execution of the program. However, it changes the normal flow of the program. It is a python object which represents an error.

Robust error handling is crucial for building reliable applications. Python provides a sophisticated exception handling mechanism.

##### The Try & Except Statements:
This full structure provides complete control over exception handling:
- `try`: Contains code that might raise an exception.
- `except`: Catches and handles specific exceptions.
- `else`: Executes only if the `try` block completes without raising an exception.
- `finally`: Executes no matter what, ensuring that cleanup code (like closing a file or releasing a lock) always runs.
```python
try:
    # code that might throw an exception
    result = 10 / 0
except ZeroDivisionError as e:
	# runs if exception occurs
    print("Caught division by zero:", e)
else:
    # runs if no exception occurred
    print("No exception, result is", result)
finally:
    # runs regardless of exceptions (for cleanup)
    print("Done with try/except")
```

###### Raising Exceptions
Use the `raise` keyword to throw an exception manually. You can raise built-in or custom exceptions.
```python
def divide(a, b):
    if b == 0:
        raise ZeroDivisionError("Division by zero is undefined")
    return a / b

# Usage
try:
    divide(10, 0)
except ZeroDivisionError as e:
    print("Raised Exception:", e)

```

##### Custom / User-Defined Exceptions
Creating custom exception hierarchies by subclassing the built-in `Exception` class provides domain-specific error information, making code clearer and easier to debug. This allows for more granular error handling and is a best practice for libraries and large applications.

```python
# Define a custom exception
class NegativeNumberError(Exception):
    """Raised when a number is negative."""
    pass

def square_root(x):
    if x < 0:
        raise NegativeNumberError("Cannot compute square root of negative number")
    return x ** 0.5

# Example usage
try:
    result = square_root(-9)
except NegativeNumberError as e:
    print("Custom Exception Caught:", e)

```

##### Exception Chaining
Exception chaining links exceptions together, providing a clear history of how an error occurred.
- **Implicit Chaining:** When an exception is raised inside an `except` block, Python automatically attaches the original exception to the new one's `__context__` attribute. The traceback will show both exceptions.
- **Explicit Chaining:** Using `raise NewException from original_exception` makes it clear that one error was a direct consequence of another. This sets the `__cause__` attribute and produces a more informative traceback, stating that one exception was raised "directly from" another.

```python
def convert_to_int(s):
    try:
        return int(s)
    except ValueError as e:
        raise TypeError("Conversion failed, wrong type provided") from e

# Example
try:
    convert_to_int("abc")
except TypeError as e:
    print("Chained Exception:", e)
    print("Original Exception:", e.__cause__)
```

##### Built-In Exceptions in Python:
| **Exception**         | **Description**                                                                   |
| --------------------- | --------------------------------------------------------------------------------- |
| `Exception`           | Base class for all exceptions                                                     |
| `ArithmeticError`     | Base class for errors in numeric calculations                                     |
| `ZeroDivisionError`   | Raised when division or modulo by zero occurs                                     |
| `OverflowError`       | Raised when result of an arithmetic operation is too large to be represented      |
| `ValueError`          | Raised when a function gets the right type but an inappropriate value             |
| `TypeError`           | Raised when an operation is applied to an object of inappropriate type            |
| `IndexError`          | Raised when a sequence subscript is out of range                                  |
| `KeyError`            | Raised when a dictionary key is not found                                         |
| `AttributeError`      | Raised when an invalid attribute reference is made                                |
| `ImportError`         | Raised when an import statement fails                                             |
| `ModuleNotFoundError` | Raised when a module cannot be found                                              |
| `FileNotFoundError`   | Raised when a file or directory is requested but doesn't exist                    |
| `IOError`             | Raised when an I/O operation fails (alias of `OSError` in Python 3)               |
| `OSError`             | Base class for system-related errors (e.g., file system, OS)                      |
| `StopIteration`       | Raised to signal the end of an iterator                                           |
| `AssertionError`      | Raised when an `assert` statement fails                                           |
| `RuntimeError`        | Raised when an error occurs that doesn’t fall under other categories              |
| `NotImplementedError` | Raised when an abstract method is not implemented                                 |
| `NameError`           | Raised when a local or global name is not found                                   |
| `MemoryError`         | Raised when an operation runs out of memory                                       |
| `RecursionError`      | Raised when the maximum recursion depth is exceeded                               |
| `EOFError`            | Raised when `input()` hits end-of-file condition (EOF)                            |
| `IndentationError`    | Raised when there is incorrect indentation                                        |
| `TabError`            | Raised when indentation consists of inconsistent tabs & spaces                    |
| `KeyboardInterrupt`   | Raised when the user interrupts program execution (Ctrl+C)                        |
| `ReferenceError`      | Raised when a weak reference proxy is used to access a garbage collected referent |

### File I/O Handling
Python allows users to read & write files and many other options to operate on files. There are 2 types of files that can be handled in python: Text Files & Binary Files.
1. **Text Files** In this type of file, each line of text is terminated with a special character called EOL, which is the newline character ("\n") in python.
2. **Binary Files** In this type of file, there is no terminator for a line, and the data is stored after converting it into machine-readable binary language.

The `with` statement is the standard, robust way to manage resources like files, ensuring that cleanup operations are always performed. This is achieved through context managers.

Open files using `open()` which returns a file object. The basic usage is:
```python
# old / classic syntax
f = open("file.txt", "r", encoding="utf-8")
data = f.read()
f.close()

# new syntax
with open("log.txt", "a") as log:
    log.write("New entry\n")
# file is auto-closed when exiting block
```

Using `with open(...) as f:` ensures the file is properly closed (even if exceptions occur). If `open()` fails (e.g. file not found), it raises an `OSError`. Always specify encoding in text mode (default is platform-dependent).

##### File-Opening Modes in Python:
| **Mode** | **Description**                                                                                    | **File Behavior**                                      |
| -------- | -------------------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| `'r'`    | Read mode (default). Opens the file for reading only.                                              | File must exist; pointer at beginning.                 |
| `'w'`    | Write mode. Opens the file for writing, truncating (overwriting) existing content.                 | Creates file if it doesn’t exist. pointer at the start |
| `'x'`    | Exclusive creation mode. Opens for writing only if the file does not already exist.                | Raises `FileExistsError` if file exists.               |
| `'a'`    | Append mode. Opens the file for writing, appending new content to the end.                         | Creates file if it doesn’t exist. Pointer at the end   |
| `'b'`    | Binary mode modifier. Used with other modes to read/write binary data (e.g., images, executables). | Must be combined (e.g., `'rb'`, `'wb'`).               |
| `'t'`    | Text mode (default). Used with other modes for reading/writing text data.                          | Implicit if not specified.                             |
| `'+'`    | Read and write mode modifier. Allows reading and writing in the same file.                         | Must be combined (e.g., `'r+'`, `'w+'`, `'a+'`).       |

##### Custom Context Managers
You can define your own context managers to encapsulate setup and teardown logic for any resource. This is a form of metaprogramming that allows you to wrap a block of code with custom behavior.
- **Class-based Approach:** Implement a class with `__enter__()` and `__exit__()` methods. `__enter__` sets up the resource and can return an object to be used in the `with` block. `__exit__` handles cleanup and receives exception details if an error occurred.
- **Function-based Approach:** A more concise method using the `@contextmanager` decorator from the `contextlib` module. The function should `yield` exactly once. Code before the `yield` is the setup (`__enter__`), and code after the `yield` is the teardown (`__exit__`).


## Section 6: Object-Oriented Programming (OOP)
This section provides a deep dive into Python's object-oriented capabilities, from fundamental method types to the esoteric but powerful concept of metaclasses.

Object-Oriented Programming is a programming paradigm based on the concept of "objects", which can contain data in the form of fields (often known as attributes or properties) and code in the form of procedures (often known as methods).

### Classes & Objects
- **Class:** A blueprint for creating objects. It defines the attributes and methods that all objects of that class will have.
- **Object (Instance):** A specific instance of a class. All the data is stored in the objects.

##### Key Concepts
- `class`: Used to define a class.
- `self`: The first parameter in any instance method. It refers to the **current instance** of the class. It's how the object accesses its own attributes and methods.
- `__init__(self, ...)`: The **constructor** method. It's called automatically when a new object is created. It's used to initialize the object's attributes.
- **Instance Attributes:** Data that is unique to each object (e.g., `dog.name`). Defined inside `__init__` using `self.attribute_name`.
- **Class Attributes:** Data that is **shared** among _all_ instances of a class. Defined outside of any method.

Example Usage
```python
# Define a class (blueprint)
class Dog:
    # Class Attribute (shared by all instances)
    species = "Canis familiaris"

    # The constructor (initializes the object)
    def __init__(self, name, age):
        # Instance Attributes (unique to each instance)
        self.name = name
        self.age = age

    # Instance Method (a function inside the class)
    def bark(self):
        print(f"{self.name} says Woof!")

    # Another instance method
    def description(self):
        return f"{self.name} is {self.age} years old."

# Create Objects (instances) from the class
my_dog = Dog("Buddy", 3)
other_dog = Dog("Lucy", 5)

# Accessing attributes
print(my_dog.name)        # Output: Buddy
print(other_dog.species)  # Output: Canis familiaris

# Calling methods
my_dog.bark()             # Output: Buddy says Woof!
print(other_dog.description()) # Output: Lucy is 5 years old.
```

### Method Types
Python classes support three distinct method types, each with a specific purpose and relationship to the class and its instances.
##### 1. Instance Methods
This is the default method type. It operates on an instance of the class and receives the instance itself as its first argument, conventionally named `self`. Instance methods are used for operations that need to access or modify instance-specific state (attributes).

##### 2. Class Methods (`@classmethod`)
A class method is bound to the class, not the instance. It is defined using the `@classmethod` decorator and receives the class as its first argument, conventionally named `cls`. Its primary use case is for factory methods—alternative constructors that can create instances of the class in different ways.

##### 3. Static Methods (`@staticmethod`)
A static method is essentially a regular function namespaced within a class. It is defined with the `@staticmethod` decorator and does not receive any implicit first argument (`self` or `cls`). It is used for utility functions that are logically related to the class but do not depend on any class or instance state.

Example Usage:
```python
class Pizza:
    def __init__(self, toppings):
        self.toppings = toppings

    # Instance method
    def show_toppings(self):
        print(f"This pizza has: {self.toppings}")

    # Class method (a "factory")
    @classmethod
    def pepperoni(cls):
        # 'cls' is the Pizza class
        return cls(['pepperoni', 'cheese'])

    # Static method (a "utility")
    @staticmethod
    def is_vegetarian(ingredients):
        # Doesn't need instance or class data
        return "meat" not in ingredients

# Regular instance creation
p1 = Pizza(['mushrooms', 'onions'])
p1.show_toppings()

# Factory method (using @classmethod)
p_pep = Pizza.pepperoni()
p_pep.show_toppings()

# Utility function (using @staticmethod)
print(Pizza.is_vegetarian(['mushrooms', 'cheese'])) # True
```

##### 4. Special (Dunder) Methods
"Dunder" stands for "Double Underscore (`__`)". These methods let your objects integrate with built-in Python operations.

| **Method**               | **Operator/Function**  | **Description**                                                                                                   |
| ------------------------ | ---------------------- | ----------------------------------------------------------------------------------------------------------------- |
| `__init__(self, ...)`    | Object creation        | The constructor.                                                                                                  |
| `__str__(self)`          | `print()`, `str()`     | Returns a user-friendly string representation.                                                                    |
| `__repr__(self)`         | `repr()`, console echo | Returns an unambiguous, developer-friendly string. A good `repr` should ideally allow you to recreate the object. |
| `__len__(self)`          | `len()`                | Returns the "length" of the object.                                                                               |
| `__eq__(self, other)`    | ==                     | Defines behavior for the equality operator.                                                                       |
| `__add__(self, other)`   | `+`                    | Defines behavior for the addition operator.                                                                       |
| `__getitem__(self, key)` | `obj[key]`             | Allows your object to act like a sequence (e.g., list, dict).                                                     |

Example Usage:
```python
class Book:
    def __init__(self, title, author, pages):
        self.title = title
        self.author = author
        self.pages = pages
    
    # For print()
    def __str__(self):
        return f'"{self.title}" by {self.author}'
    
    # For developer output
    def __repr__(self):
        return f"Book(title='{self.title}', author='{self.author}', pages={self.pages})"
    
    # For len()
    def __len__(self):
        return self.pages

book = Book("The Hobbit", "J.R.R. Tolkien", 310)

print(book)      # Calls __str__ -> "The Hobbit" by J.R.R. Tolkien
print(repr(book))  # Calls __repr__ -> Book(title='The Hobbit', ...)
print(len(book))     # Calls __len__ -> 310
```

### Inheritance Concepts
##### **Multiple Inheritance and the Diamond Problem**
Python supports multiple inheritance, where a class can inherit from more than one parent class. This can lead to the "diamond problem," an ambiguity that arises when a class inherits from two classes that share a common ancestor. Python resolves this ambiguity using a well-defined Method Resolution Order (MRO).

##### **Method Resolution Order (MRO)**
The MRO is the precise order in which Python searches the class hierarchy for a method. Python uses the **C3 Linearization algorithm** to compute a deterministic and consistent MRO that satisfies several key properties, including preserving the local precedence order of base classes and monotonicity. You can inspect the MRO of a class using the `__mro__` attribute or the `.mro()` method.

##### The `super()` Function
In the context of multiple inheritance, `super()` is a dynamic proxy object that delegates method calls to the _next_ class in the MRO, not necessarily the direct parent. This is crucial for implementing "cooperative multiple inheritance," where each class in the chain calls the `super()` implementation of a method, ensuring all parent methods are executed in the correct order.


### The Four Pillars of OOP in Python
##### 1. Encapsulation
Encapsulation is the bundling of data (attributes) and the methods that operate on that data into a single unit (a class). Python uses naming conventions for access control rather than strict enforcement.

Python doesn't have strict `private` keywords like Java or C++. It relies on naming conventions:
- **Public:** Attributes are accessible from anywhere (e.g., `self.name`).
- **Protected:** Attributes prefixed with a single underscore (e.g., `self._internal_data`) are treated as non-public by convention and should not be accessed directly from outside the class.
- **Private:** Attributes prefixed with a double underscore (e.g., `self.__private_var`) are subject to _name mangling_, where the name is changed to `_ClassName__private_var`. This makes it harder, but not impossible, to access from outside the class.

```python
class Car:
    def __init__(self, make, model):
        self.make = make          # Public
        self._speed = 0           # Protected
        self.__engine_serial = "A123X" # Private (name-mangled)

    def _accelerate(self):        # Protected method
        self._speed += 10
        print(f"Speed is now {self._speed}")
    
    def get_serial(self):
        # We can access __engine_serial inside the class
        return self.__engine_serial

c = Car("Toyota", "Corolla")
print(c.make)    # OK
print(c._speed)  # OK (but bad practice)
# print(c.__engine_serial) # AttributeError!

# This is how you can access it (don't do this)
print(c._Car__engine_serial) # Output: A123X
```

**Properties (The Pythonic Way):**
A cleaner, more "Pythonic" way to manage attributes is using **properties**. They allow you to use getters, setters, and deleters to control access.
```python
class Person:
    def __init__(self, age):
        self._age = age # Internal attribute
    
    # This is the "getter"
    @property
    def age(self):
        """Gets the age."""
        print("Getter called")
        return self._age

    # This is the "setter"
    @age.setter
    def age(self, value):
        """Sets the age, with validation."""
        print("Setter called")
        if value < 0:
            raise ValueError("Age cannot be negative")
        self._age = value

# Usage
p = Person(25)
print(p.age)      # Getter called. Output: 25

p.age = 30        # Setter called.
print(p.age)      # Getter called. Output: 30
```


##### 2. Inheritance
Inheritance allows a new class (the **child class** or **subclass**) to inherit attributes and methods from an existing class (the **parent class** or **superclass**). This supports the **"is-a"** relationship (e.g., a `Dog` "is-a" `Animal`).
- `super()`: A function used to call methods from the parent class. This is crucial for extending `__init__` and other methods, rather than completely replacing them.
- **Method Overriding:** A child class can provide its own implementation of a method that is already defined in its parent class.

Example Usage:
```python
# Parent Class
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        print("Some generic animal sound")

# Child Class
class Dog(Animal):
    def __init__(self, name, breed):
        # Call the parent's constructor
        super().__init__(name)
        self.breed = breed
    
    # Overriding the speak method
    def speak(self):
        print(f"{self.name} says Woof!")

# Another Child Class
class Cat(Animal):
    # This class inherits speak() without overriding it
    pass

d = Dog("Buddy", "Golden Retriever")
d.speak()  # Output: Buddy says Woof!

c = Cat("Whiskers")
c.speak()  # Output: Some generic animal sound
```

**Multiple Inheritance:** A class can inherit from multiple parent classes. Python follows a **Method Resolution Order (MRO)** to determine which method to call.
```python
class A:
    def ping(self): print("A")

class B(A):
    def ping(self): print("B")

class C(A):
    def ping(self): print("C")

class D(B, C): # Inherits from B, then C
    pass

d = D()
d.ping() # Output: B

# You can inspect the MRO
print(D.mro())
# Output: [<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>]
```

##### 3. Polymorphism
Polymorphism (from Greek, "many forms") means that objects of different classes can be treated as objects of a common superclass. It allows you to use a single interface (like a function) to operate on objects of different types.

**Duck Typing:** This is Python's main approach to polymorphism.
> "If it walks like a duck and it quacks like a duck, then it must be a duck."

Python doesn't care about the _type_ of the object, only if it has the required _methods_.

##### 4. Abstraction
Abstraction involves hiding the complex implementation details and exposing only the essential features (interface) to the user.

In Python, this is formally achieved using **Abstract Base Classes (ABCs)** from the `abc` module.
- An **abstract class** cannot be instantiated by itself.
- It defines one or more `@abstractmethod`, which are methods without an implementation.
- Any concrete (non-abstract) child class _must_ implement all abstract methods. If a subclass fails to implement all abstract methods, a `TypeError` is raised.

Example Usage:
```python
from abc import ABC, abstractmethod

# Abstract Class (the "interface")
class Shape(ABC):
    
    @abstractmethod
    def area(self):
        """Calculate the area of the shape."""
        pass
    
    @abstractmethod
    def perimeter(self):
        """Calculate the perimeter of the shape."""
        pass

# Concrete Class (the "implementation")
class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height
    
    def area(self):
        return self.width * self.height
    
    def perimeter(self):
        return 2 * (self.width + self.height)

# Another Concrete Class
class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14159 * self.radius**2
    
    def perimeter(self):
        return 2 * 3.14159 * self.radius

# You cannot create an instance of the abstract class
# s = Shape() # TypeError: Can't instantiate abstract class Shape

r = Rectangle(10, 5)
c = Circle(7)

print(f"Rectangle Area: {r.area()}") # Output: 50
print(f"Circle Area: {c.area()}")    # Output: 153.93791
```


## Section 7: Python Standard Libraries
### Random
The **`random`** module in Python is part of the standard library and provides functions to generate **pseudo-random numbers**, make **random selections**, **shuffle sequences**, and **simulate randomness** for various applications — such as simulations, gaming, sampling, and data randomization.

It uses the **Mersenne Twister algorithm**, which is deterministic but provides high-quality pseudo-random numbers.

##### Example Usage
```Python
import random

# generate random numbers
# Returns a float in the range [0.0, 1.0)
print(random.random())  # e.g. 0.745325612

# Returns a random float N such that a ≤ N ≤ b
print(random.uniform(10, 20))  # e.g. 14.37

# Returns a random integer N such that a ≤ N ≤ b
print(random.randint(1, 6))  # simulates dice roll → 1 to 6

# Returns a randomly selected **element** from the given range.
print(random.randrange(0, 10, 2))  # e.g. 2  (0, 2, 4, 6, 8)

# Returns a random element from a non-empty sequence (like list or tuple).
colors = ['red', 'blue', 'green']
print(random.choice(colors))  # e.g. 'blue'
random.choices([1,2,3],[1,1,10]) # e.g. 3, (heavily weighted towards 3)

# Shuffles the sequence in-place
deck = [1, 2, 3, 4, 5]
random.shuffle(deck)
print(deck)  # shuffled order, e.g. [3, 1, 5, 2, 4]
```

We, can **seed** the random number generator for reproducible results:
- Using the same seed guarantees the same random sequence each time.
- Good for testing or debugging.
```python
random.seed(42)
print(random.random())  # always same for same seed
```

##### Practical Use Case
```python
# random password generation
import random, string
password = ''.join(random.choices(string.ascii_letters + string.digits, k=8))
print(password)

# random sampling from a dataset
data = ['A', 'B', 'C', 'D', 'E']
sampled = random.sample(data, 3)
print(sampled)
```

### Math
The `math` module provides access to common mathematical functions and constants, many from the C standard library. Example functions/constants:
- `math.sqrt(x)` – square root.
- `math.pow(x,y)` – x raised to y (use `**` as operator or `pow(x,y)` as built-in).
- `math.sin(x)`, `math.cos(x)`, `math.tan(x)` – trigonometry.
- `math.log(x[, base])`, `math.log10(x)`, `math.exp(x)` – logarithms and exponentials.
- `math.ceil(x)`, `math.floor(x)`, `math.factorial(n)`, `math.gcd(a,b)`.
- Constants: `math.pi`, `math.e`, `math.inf`, `math.nan`, etc.

All `math` functions (except those noted for complex numbers) return floats.
```python
import math
print(math.pi, math.e)            # 3.14159... 2.71828...
print(math.sqrt(16), math.log10(100))  # 4.0, 2.0
print(math.factorial(5), math.gcd(8, 12))  # 120, 4

# constants:
max = float('-inf')
min = float('inf')
```

### Collections
The `collections` module provides specialized container datatypes as alternatives to built-in list/dict/set/tuple. Useful classes include:
- `deque`: A list-like container optimized for fast appends and pops from both ends ($O(1)$ time complexity). It is implemented as a doubly-linked list.
- `Counter`: a `dict` subclass for counting hashable objects. It is an unordered collection where elements are stored as dictionary keys and their counts are stored as dictionary values.
- `defaultdict`: A subclass of `dict` that provides a default value for a nonexistent key, avoiding `KeyError` exceptions. It is initialized with a "default factory" function (e.g., `int`, `list`, `set`) that is called to supply the default value. A `defaultdict(int)` would create missing keys with default `0`, etc.
- `namedtuple`: A factory function for creating tuple subclasses with named fields. This allows for more readable, self-documenting code, as elements can be accessed by name instead of just by index.

##### Example Usage:
```python
from collections import deque, Counter, defaultdict, namedtuple
d = deque([1,2,3])  
d.appendleft(0)  
d.pop() # 3, pops from right end

words = ["apple","banana","apple","orange","banana","apple"]
cnt = Counter(words)
print(cnt)  # Counter({'apple':3, 'banana':2, 'orange':1})
print(cnt.most_common(1))  # [('apple', 3)]

d = defaultdict(list)
dd['a'].append(1)
dd['b'].append(2)
print(dd)  # {'a':[1], 'b':[2]}

Point = namedtuple('Point', ['x','y'])
p = Point(10, 20)
print(p.x, p.y)  # 10 20

# real-life use case: To find if given str is an anagram using counter dict
def isAnagram(self, s: str, t: str) -> bool:
    sc = collections.Counter(s)
    st = collections.Counter(t)
    if sc != st:
        return False
    return True
```

The `collections` module also includes `OrderedDict` (ordered dict, though regular `dict` is ordered by default now), `ChainMap`, `UserDict`, etc. In summary, it implements “specialized container datatypes” beyond the built-ins.


## Section 8: Essential Third-Party Libraries
### NumPy
NumPy provides the powerful `ndarray` for numerical computing. An `ndarray` is a multi-dimensional, homogeneous array of fixed-size items. You work with NumPy by importing it, usually as `import numpy as np`. Example:
```python
import numpy as np
a = np.array([1,2,3])             # 1D array
b = np.array([[1,2,3],[4,5,6]])   # 2D array
print(a + 5)                      # elementwise add -> [6 7 8]
print(b.shape)                    # (2,3)
c = np.zeros((2,2))               # 2x2 array of zeros
d = np.arange(5)                  # [0 1 2 3 4]
```
NumPy arrays support vectorized operations: adding, multiplying arrays does elementwise math without Python loops. Common functions include `np.mean`, `np.sum`, `np.dot` (or `@` operator for matrix multiplication), and linear algebra routines. NumPy excels at numerical computations and is the basis for many scientific Python libraries. Broadcasting rules allow combining arrays of different shapes in arithmetic.

##### **Advanced Array Manipulation**
1. **Reshaping and Transposing:**
    - `reshape(shape)`: Returns an array with a new shape without changing its data. The new shape must be compatible with the original size.
    - `.T` / `transpose()`: Reverses the dimensions of an array.
2. **Joining and Splitting:**
    - `np.concatenate((a1, a2,...), axis=0)`: Joins a sequence of arrays along an existing axis.
    - `np.vstack(tup)` and `np.hstack(tup)`: Stack arrays vertically (row-wise) and horizontally (column-wise), respectively.
    - `np.split(ary, indices_or_sections, axis=0)`: Splits an array into multiple sub-arrays.
3. **Adding and Removing Elements:**
    - `np.append(arr, values, axis=None)`: Appends values to the end of an array. Note: this returns a _new_ array, as NumPy arrays have a fixed size.
    - `np.insert(arr, obj, values, axis=None)`: Inserts values along a given axis before given indices.
    - `np.delete(arr, obj, axis=None)`: Returns a new array with sub-arrays along an axis deleted.

**Vectorization and Performance**
Vectorization is the practice of replacing explicit `for` loops with array expressions. This is the core of efficient NumPy programming.
- **Boolean Indexing (Masking):** Using a Boolean array to select or modify elements. This is a highly efficient filtering technique.
- `np.where()`: A vectorized equivalent of a ternary `if/else` expression.
- `np.vectorize()`: A convenience function for applying a scalar Python function to arrays. This function is primarily for convenience and does _not_ provide performance benefits, as it internally uses a Python loop. For performance, rewrite the function using native NumPy operations.

### Pandas
Pandas is a popular library for data analysis. Its primary data structures are **Series** and **DataFrame**. A _Series_ is a 1D labeled array, and a _DataFrame_ is a 2D labeled table (like a spreadsheet).
```python
import pandas as pd
# Create a DataFrame from a dict of lists
df = pd.DataFrame({'col1': [1,2,3], 'col2': [4,5,6]})
print(df)
#    col1  col2
# 0     1     4
# 1     2     5
# 2     3     6

# Create a Series with custom index
s = pd.Series([10, 20, 30], index=['a','b','c'])
print(s)
# a    10
# b    20
# c    30
# dtype: int64
```

Pandas offers many powerful operations: reading data from CSV/JSON/SQL (`pd.read_csv`, etc.), grouping, merging, statistics, handling missing data, and time series functionality. The DataFrame aligns on row/column labels for arithmetic and handles heterogeneous column types. Pandas objects have methods like `.head()`, `.describe()`, `.mean()`, etc., for quick insights.

DataFrame is described as “two-dimensional, size-mutable, potentially heterogeneous tabular data [with] labeled axes”. It is the primary Pandas structure, analogous to a table or Excel spreadsheet.

**Advanced Indexing (`.loc`, `.iloc`, Boolean Indexing)**
Pandas offers powerful and explicit indexing methods to select subsets of data.
- **`.loc` (Label-based):** Selects data based on index labels. Slices are _inclusive_ of the endpoint.
- **`.iloc` (Integer-based):** Selects data based on 0-indexed integer positions. Slices are _exclusive_ of the endpoint, following standard Python slicing.
- **Boolean Indexing (Masking):** Creates a boolean `Series` from a condition and uses it to filter a `DataFrame`. Multiple conditions must be combined with `&` (and) or `|` (or), with each condition wrapped in parentheses.

**Advanced GroupBy and Aggregation**
The `groupby` operation enables the powerful "split-apply-combine" strategy for data analysis.
- **Aggregation (`.agg()`):** Applies one or more aggregation functions to each group. It supports named aggregations for cleaner output.
- **Transformation (`.transform()`):** Performs a group-wise computation and broadcasts the result back to the original `DataFrame`'s shape. This is ideal for creating new features based on group properties, such as a group-wise z-score.
- **Filtering (`.filter()`):** Subsets the `DataFrame` by keeping only groups that satisfy a Boolean condition.

**Combining DataFrames (`merge`, `join`, `concat`)**
Pandas provides several functions for combining `DataFrame` objects.
- **`pd.concat()`:** Stacks DataFrames vertically (`axis=0`) or horizontally (`axis=1`). It aligns data based on the index.
- **`pd.merge()`:** The most flexible function for SQL-style joins on common columns or indices. The `how` parameter specifies the join type (`'inner'`, `'left'`, `'right'`, `'outer'`).
- **`.join()`:** A convenience method for merging `DataFrame`s based on their indices. It is equivalent to using `pd.merge` with `left_index=True` and/or `right_index=True`.