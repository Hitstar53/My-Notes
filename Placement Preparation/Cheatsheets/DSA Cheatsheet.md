## Table of Contents:
1. [[#Section 1 Introduction to Algorithmic Analysis]]
2. [[#Section 2 Foundational Data Structures]]
3. [[#Section 3 Advanced Data Structures]]
4. [[#Section 4 Essential Algorithms & Techniques]]
5. [[#Conclusion]]

## Section 1: Introduction to Algorithmic Analysis
The study of Data Structures and Algorithms (DSA) forms the bedrock of computer science and software engineering. At its core, this discipline is concerned with the efficient organization, processing, and retrieval of data. The choice of a data structure and its corresponding algorithms directly impacts a program's performance, determining its speed, memory consumption, and scalability. An understanding of DSA is what enables the development of software that is not only correct but also robust and efficient, capable of handling vast amounts of data and complex computational tasks. This document serves as a comprehensive technical reference, or "cheatsheet," detailing the fundamental principles, implementations, and performance characteristics of the most critical data structures and algorithms.

### Measuring Performance: Time & Space Complexity
To evaluate and compare the efficiency of algorithms, a formal, quantitative framework is required. This framework is provided by complexity analysis, a technique used to characterize the resources—primarily execution time and memory—that an algorithm requires as a function of the size of its input. The two principal metrics of this analysis are:

1. **Time Complexity**: This measures the amount of time an algorithm takes to complete as a function of its input size, denoted as 'n'. It is not a measure of wall-clock time, which can vary dramatically based on hardware, the programming language, and the compiler. Instead, it quantifies the number of basic operations (e.g., comparisons, assignments) the algorithm performs. This abstraction allows for a standardized, machine-independent comparison of algorithmic efficiency.2

2. **Space Complexity**: This measures the amount of memory space an algorithm requires to solve a problem as a function of its input size 'n'. It includes both the space used by the input data and any auxiliary space used by the algorithm during its execution (e.g., for temporary variables or data structures).

By analyzing these two complexities, one can make informed decisions about which algorithm is best suited for a particular problem, especially when considering constraints on time or memory resources.

### The Big $O$ Notation
Big O notation is the standard mathematical notation used in computer science to describe the asymptotic behavior of an algorithm's complexity. Specifically, it describes the **upper bound** or the **worst-case scenario**, providing a concise way to express how an algorithm's resource consumption scales as the input size grows infinitely large.

The power of Big O notation lies in its abstraction. It focuses on the dominant factor that affects performance as the input size increases, deliberately ignoring constant factors and lower-order terms. For instance, an algorithm that performs $3n2+5n+100$ operations is simplified to $O(n^2)$. The $n^2$ term dominates the function's growth for large values of $n$, making the other terms negligible in the context of scalability. This focus on the growth rate, rather than the exact number of operations, is what allows for a universal, hardware-agnostic comparison of algorithmic efficiency. An algorithm with $O(nlogn)$ complexity will fundamentally be more scalable for large inputs than one with $O(n^2)$ complexity, regardless of the speed of the machine it runs on. This understanding of scalability is the cornerstone of effective algorithmic design.

#### Common Complexity Classes:
The following are the most common complexity classes, ordered from most to least efficient for large input sizes.

1. **$O(1)$ - Constant Time**: The algorithm's execution time is constant and does not depend on the input size 'n'. Operations like accessing an array element by its index or pushing an element onto a stack fall into this category.
    ```python
    def get_first_element(data_list):
        if data_list:
            return data_list # O(1) operation
        return None
    ```

2. **$O(logn)$ - Logarithmic Time**: The algorithm's runtime grows logarithmically with the input size. These algorithms are highly efficient, as the time required increases only slightly for a large increase in 'n'. They typically work by repeatedly reducing the problem size by a constant factor, often by half. Binary search is a classic example.
    ```python
    # Simplified concept of halving the problem space
    def logarithmic_example(n):
        i = 1
        while i < n:
            i *= 2 # The number of iterations is log_2(n)
            # O(1) work per iteration
    ```

3. **$O(n)$ - Linear Time**: The algorithm's runtime is directly proportional to the input size. If the input size doubles, the runtime also roughly doubles. A simple loop that iterates through all elements of a list is a common example.
    ```python
    def find_max_element(data_list):
        max_val = data_list
        for item in data_list: # Loop runs n times
            if item > max_val:
                max_val = item
        return max_val
    ```

4. **$O(nlogn)$ - Linearithmic Time**: This complexity class is common for efficient, comparison-based sorting algorithms. The runtime grows in proportion to 'n' times the logarithm of 'n'. Merge sort and heapsort are prime examples.
    ```python
    # Conceptual structure of a divide-and-conquer sort
    def n_log_n_sort(data_list):
        if len(data_list) <= 1:
            return data_list
        mid = len(data_list) // 2
        left_half = n_log_n_sort(data_list[:mid]) # Recursive call on n/2
        right_half = n_log_n_sort(data_list[mid:]) # Recursive call on n/2
        # Merging takes O(n) time
        return merge(left_half, right_half)
    ```

5. **$O(n^2)$ - Quadratic Time**: The algorithm's runtime is proportional to the square of the input size. This is typical of algorithms that involve nested iterations over the input data, such as comparing every element of a list to every other element. Simple sorting algorithms like bubble sort, insertion sort, and selection sort have this complexity.
    ```python
    def find_duplicates(data_list):
        for i in range(len(data_list)): # Outer loop runs n times
            for j in range(i + 1, len(data_list)): # Inner loop runs roughly n times
                if data_list[i] == data_list[j]:
                    return True
        return False
    ```

6. **$O(2^n) \space \& \space O(n!)$ - Exponential and Factorial Time**: These complexities represent highly inefficient algorithms whose runtimes grow extremely rapidly with the input size. They are often associated with brute-force solutions that explore every possible combination or permutation of a set of elements, such as solving the traveling salesman problem by checking every possible route.

| Notation   | Name         | Growth Characteristic                                                                                             |
| ---------- | ------------ | ----------------------------------------------------------------------------------------------------------------- |
| $O(1)$     | Constant     | Runtime is constant and does not grow with input size.                                                            |
| $O(logn)$  | Logarithmic  | Runtime grows very slowly as input size increases.                                                                |
| $O(n)$     | Linear       | Runtime grows directly in proportion to the input size.                                                           |
| $O(nlogn)$ | Linearithmic | More efficient than quadratic but less than linear. Common for advanced sorting. Suitable for input sizes $>10^5$ |
| $O(n^2)$   | Quadratic    | Runtime grows rapidly, proportional to the square of the input size. Only feasible for input sizes $<10^4$        |
| $O(2^n)$   | Exponential  | Runtime doubles with each addition to the input, becoming quickly unusable.                                       |
| $O(n!)$    | Factorial    | Runtime grows extremely fast, only feasible for very small input sizes.                                           |

## Section 2: Foundational Data Structures
Data structures are specialized formats for organizing, processing, retrieving, and storing data. They are designed to make certain operations more efficient. The choice of data structure is a critical design decision that can profoundly affect the performance of a software system.

### Arrays
An array is a linear data structure that stores a collection of elements, each identified by at least one array index or key. The defining characteristic of an array is that its elements are stored in **contiguous memory locations**. This contiguous memory layout is the fundamental property from which all of an array's performance characteristics are derived.

The ability to store elements side-by-side in memory allows for the calculation of an element's memory address directly from its index. The address of an element at index 'i' can be computed using a formula like `base_address + i * element_size`. This direct computation is what enables one of the array's most significant advantages: constant-time random access.

#### Operational Analysis and Complexity
- **Access**: The time complexity for accessing an element at a given index is **O(1)**. This is the primary strength of the array data structure, as it allows for immediate retrieval of any element regardless of its position or the size of the array.
- **Search**: To find an element by its value (without knowing its index), a **linear search** is required, which involves iterating through the elements one by one. This results in a time complexity of **O(n)** in the worst case. If the array is sorted, a more efficient **binary search** can be used, which has a time complexity of **O(logn)**.
- **Insertion and Deletion**: These operations are generally inefficient. To insert or delete an element at the beginning or in the middle of an array, all subsequent elements must be shifted one position to the right or left, respectively, to maintain contiguity. This shifting process results in a time complexity of **O(n)** in the worst and average cases. An exception is insertion at the end of a _dynamic array_, which is an amortized **O(1)** operation.

#### Python Implementation
In Python, the built-in `list` type serves as a dynamic array. It automatically handles resizing when elements are added or removed. While convenient, it's important to remember that this resizing operation can occasionally lead to performance overhead that is averaged out over many operations. For applications requiring high-performance numerical computations with strictly homogeneous data, the `numpy` library's `array` is often preferred due to its memory efficiency and optimized operations.
```python
# Python's list acts as a dynamic array
my_array = []

# Accessing an element (O(1))
first_element = my_array
print(f"First element: {first_element}")

# Appending an element (Amortized O(1))
my_array.append(60)
print(f"Array after append: {my_array}")

# Inserting an element at a specific index (O(n))
my_array.insert(1, 15) # Shifts elements from index 1 onwards
print(f"Array after insertion: {my_array}")

# Deleting an element by index (O(n))
del my_array # Shifts elements from index 3 onwards
print(f"Array after deletion: {my_array}")
```
#### Arrays vs Lists in Python
In Python, while the built-in `list` object is versatile and often used like an array, there is a distinct `array` object available through the `array` module that behaves more like traditional arrays found in languages like C. The primary difference lies in their data type constraints and memory efficiency.8

- **Python `list`**:
    - **Data Type Flexibility**: A `list` is a highly flexible container that can store elements of different data types (heterogeneous) within the same list. You can have integers, strings, and other objects all in one list.
    - **General Purpose**: Lists are the go-to, general-purpose sequence type in Python, suitable for a wide variety of tasks.
        
- **Python `array` (from the `array` module)**:
    - **Strict Data Typing**: An `array` is constrained to store elements of only one specific data type (homogeneous), which is declared upon its creation using a `typecode`.9 For example, an array can be declared to hold only signed integers or only floating-point numbers.
    - **Memory Efficiency**: Because `array` objects store only one type of data, they are more memory-efficient than lists, especially for large sequences of numeric data. This makes them a better choice for performance-critical applications involving large numerical datasets.
```python
import array as arr

# Creating an array of signed integers ('i')
# All elements must be of the same type
my_array = arr.array('i', [3, 4, 5, 6])

# Appending another integer is successful
my_array.append(50)

print(f"Python array: {my_array}")
# Expected Output: Python array: array('i', [3, 4, 5, 6, 7])

# Attempting to add a non-integer (e.g., a string) will cause a TypeError
```

### Linked Lists
A linked list is a linear data structure where elements are not stored at contiguous memory locations. Instead, it consists of a sequence of **nodes**, where each node contains two components: the data itself and a **pointer** (or reference) to the next node in the sequence. The entry point to the list is a pointer called the `head`, which points to the first node. The last node in the list points to `None` (or `NULL`), signifying the end of the list.

This non-contiguous, pointer-based structure is the source of the fundamental trade-off between linked lists and arrays. While arrays excel at random access due to their memory layout, linked lists excel at insertion and deletion at their ends because they only require redirecting pointers, not shifting data.

#### Variations and Trade-offs
- **Singly Linked List**: This is the simplest form, where each node has a single pointer to the next node. Traversal is unidirectional, from head to tail.
- **Doubly Linked List**: Each node contains three components: data, a pointer to the next node, and a pointer to the _previous_ node. This allows for bidirectional traversal (forward and backward), which can simplify certain operations like deletion, but it comes at the cost of increased memory usage per node.
- **Circular Linked List**: In this variation, the `next` pointer of the last node points back to the `head` node instead of `None`, creating a loop. This structure is useful for applications that require continuous cycling through elements, such as round-robin scheduling algorithms.

#### Operational Analysis and Complexity
- **Access and Search**: To access an element at a specific index or to search for a value, one must traverse the list starting from the `head` and following the `next` pointers. This results in a time complexity of **O(n)** in the worst case.
- **Insertion and Deletion (at the beginning)**: Adding or removing a node at the beginning of the list is highly efficient. It only requires updating the `head` pointer and, in the case of insertion, setting the new node's `next` pointer. These are constant-time operations, resulting in a time complexity of **O(1)**.
- **Insertion and Deletion (at the end or middle)**: To perform these operations, the list must first be traversed to find the desired position. This traversal takes $O(n)$ time, making the overall complexity **O(n)**. In a doubly linked list, if a direct reference to a node is available, its deletion can be performed in **O(1)** time because its previous node is directly accessible.

#### Python Implementation
Python does not have a built-in linked list data structure. It must be implemented from scratch using classes. A `Node` class is created to hold the data and the `next` reference, and a `LinkedList` class is created to manage the operations on the collection of nodes.
```python
# Implementation of a Node for a singly linked list
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

# Implementation of a Singly Linked List
class LinkedList:
    def __init__(self):
        self.head = None

    # Insertion at the beginning (O(1))
    def insert_at_beginning(self, new_data):
        new_node = Node(new_data)
        new_node.next = self.head
        self.head = new_node

    # Deletion from the beginning (O(1))
    def delete_from_beginning(self):
        if self.head is None:
            return
        self.head = self.head.next

    # Traversal and display (O(n))
    def display(self):
        current = self.head
        elements =
        while current:
            elements.append(str(current.data))
            current = current.next
        print(" -> ".join(elements))

# Example usage
ll = LinkedList()
ll.insert_at_beginning(30)
ll.insert_at_beginning(20)
ll.insert_at_beginning(10)
print("Linked List:")
ll.display() # Output: 10 -> 20 -> 30

ll.delete_from_beginning()
print("After deletion:")
ll.display() # Output: 20 -> 30
```

### Stacks
A stack is a linear data structure that adheres to the **Last-In, First-Out (LIFO)** principle. This means the last element added to the stack is the first element to be removed. Operations are restricted to a single end, known as the "top" of the stack. A common real-world analogy is a stack of plates: you add a new plate to the top, and you remove a plate from the top.

#### Core Operations and Complexity
The primary operations for a stack are designed to be highly efficient, reflecting its use as a structure for temporary storage and ordered processing.

- **Push**: Adds an element to the top of the stack.
- **Pop**: Removes and returns the element from the top of the stack.
- **Peek (or Top)**: Returns the top element without removing it.

In a proper implementation, all three of these core operations have a time complexity of **O(1)**.

#### Python Implementation Strategies
Python offers several ways to implement a stack, with different performance characteristics.

1. **Using `list`**: This is the simplest method. The `list.append()` method serves as `push`, and `list.pop()` (without an index) serves as `pop`. Both operations target the end of the list and have an amortized time complexity of 'O(1)'.33 While generally efficient, the underlying dynamic array can occasionally require resizing, which is an $O(n)$ operation, though this cost is averaged out over many appends.
    ```python
    stack_list =
    # Push operations
    stack_list.append('A')
    stack_list.append('B')
    stack_list.append('C')
    print(f"Stack as list: {stack_list}") # Output:
    
    # Pop operation
    top_element = stack_list.pop()
    print(f"Popped: {top_element}") # Output: C
    print(f"Stack after pop: {stack_list}") # Output:
    ```

2. **Using `collections.deque`**: The `deque` object (double-ended queue) is implemented as a doubly linked list and is the recommended approach for performance-critical applications. It provides true, worst-case **O(1)** time complexity for `append` (push) and `pop` (pop) operations from its right end, avoiding the potential resizing overhead of lists.
    ```python
    from collections import deque
    stack_deque = deque()
    # Push operations
    stack_deque.append('A')
    stack_deque.append('B')
    stack_deque.append('C')
    print(f"Stack as deque: {stack_deque}") # Output: deque()
    
    # Pop operation
    top_element = stack_deque.pop()
    print(f"Popped: {top_element}") # Output: C
    print(f"Stack after pop: {stack_deque}") # Output: deque()
    ```

3. **Using a Linked List**: Implementing a stack from scratch using a singly linked list provides a clear demonstration of the LIFO principle. Pushing and popping elements at the head of the list are both **O(1)** operations, offering guaranteed worst-case performance without any amortization.
    

#### Applications
The LIFO behavior of stacks makes them ideal for a variety of computational problems, including:
- **Function Call Management**: The "call stack" keeps track of active function calls. When a function is called, a new frame is pushed onto the stack; when it returns, its frame is popped.
- **Undo/Redo Mechanisms**: In applications like text editors, each user action can be pushed onto a stack. The "undo" operation simply pops the last action.
- **Expression Evaluation and Parsing**: Stacks are used to convert expressions from infix to postfix notation and to evaluate postfix expressions.
- **Backtracking Algorithms**: In problems like maze-solving or depth-first search, a stack can be used to keep track of the path taken, allowing the algorithm to backtrack when it reaches a dead end.

### Queues
A queue is a linear data structure that operates on the **First-In, First-Out (FIFO)** principle. This means the first element added to the queue will be the first element to be removed. Elements are added at one end, called the "rear," and removed from the other end, called the "front".41 A common real-world analogy is a checkout line at a store: the first person to get in line is the first person to be served.

#### Core Operations and Complexity
- **Enqueue**: Adds an element to the rear of the queue.
- **Dequeue**: Removes and returns the element from the front of the queue.
- **Peek (or Front)**: Returns the front element without removing it.

For an efficient implementation, both `enqueue` and `dequeue` operations should have a time complexity of **O(1)**.

#### Python Implementation Strategies
The choice of underlying structure is critical for implementing an efficient queue in Python.
1. **Using `list` (Anti-Pattern)**: A naive implementation might use `list.append()` for enqueue and `list.pop(0)` for dequeue. While `append` is efficient (amortized 'O(1)'), `pop(0)` is highly inefficient. Removing an element from the beginning of a list requires shifting all subsequent elements one position to the left, which is an **O(n)** operation. This violates the performance requirement of a queue and should be avoided in production code.

2. **Using `collections.deque`**: This is the canonical and most efficient method for implementing a queue in Python. The `deque` is a doubly linked list optimized for fast appends and pops from both ends. `deque.append()` is used for `enqueue`, and `deque.popleft()` is used for `dequeue`. Both are true **O(1)** operations, making `deque` the ideal choice.
    ```python
    from collections import deque
    queue_deque = deque()
    
    # Enqueue operations
    queue_deque.append('Task 1')
    queue_deque.append('Task 2')
    queue_deque.append('Task 3')
    print(f"Queue as deque: {queue_deque}") # Output: deque()
    
    # Dequeue operation
    front_element = queue_deque.popleft()
    print(f"Dequeued: {front_element}") # Output: Task 1
    print(f"Queue after dequeue: {queue_deque}") # Output: deque()
    ```

3. **Using `queue.Queue`**: This class from Python's `queue` module provides a thread-safe implementation of a FIFO queue. It is designed for use in concurrent programming where multiple threads need to safely exchange data. It uses `put()` for enqueue and `get()` for dequeue, which can block if the queue is full or empty, respectively.

#### Applications
The FIFO property of queues makes them essential for managing tasks and resources in order:
- **Task Scheduling**: Operating systems use queues to manage processes waiting for the CPU. The first process to request the CPU is the first to get it (in simple scheduling models).
- **Buffering**: Queues are used as buffers in data streaming, where data is produced at a variable rate and consumed at a different rate. The queue smooths out the process.
- **Breadth-First Search (BFS)**: This graph traversal algorithm uses a queue to keep track of the nodes to visit next, ensuring the graph is explored layer by layer.
- **Print Queues**: Documents sent to a shared printer are placed in a queue to be printed in the order they were received.

### Hash Maps (Dictionaries)
A hash map, known as a dictionary in Python, is a data structure that stores data in **key-value pairs**. Its primary advantage is providing fast data retrieval. This is achieved by using a **hash function**, which takes a key and computes an index into an array of buckets or slots. The value associated with the key is then stored at this index.

The efficiency of a hash map relies on a good hash function that distributes keys evenly across the array, minimizing **collisions** (when two different keys hash to the same index). When collisions do occur, they are typically handled by storing a list of key-value pairs at the collision index (a technique called separate chaining). In Python, dictionary keys must be immutable types (like strings, numbers, or tuples) because their hash value must remain constant.

#### Operational Analysis and Complexity
- **Insertion, Deletion, and Access**: The time complexity for these operations is **O(1)** on average. The hash function allows for direct computation of the storage location, eliminating the need to search through the data structure.
- **Worst Case**: In the rare worst-case scenario where many keys hash to the same index, the time complexity can degrade to **O(n)** as it becomes necessary to search through the list at that index.

#### Python Implementation
Python's built-in `dict` type is a highly optimized hash map implementation.
```python
# Creating a dictionary
student_scores = {"Alice": 95, "Bob": 87, "Charlie": 92}
print(f"Initial dictionary: {student_scores}")

# Accessing a value (O(1) on average)
alices_score = student_scores["Alice"]
print(f"Alice's score: {alices_score}")

# Adding a new key-value pair (O(1) on average)
student_scores = 88
print(f"After adding David: {student_scores}")

# Updating a value (O(1) on average)
student_scores = 90
print(f"After updating Bob's score: {student_scores}")

# Deleting a key-value pair (O(1) on average)
del student_scores["Charlie"]
print(f"After deleting Charlie: {student_scores}")
```

#### Example Problem: Count Word Frequencies
**Problem:** Given a list of words, count the frequency of each word.

**Explanation:** A hash map is ideal for this task. We can iterate through the list of words. For each word, we use it as a key in our dictionary. If the key already exists, we increment its corresponding value (the count). If it doesn't exist, we add it to the dictionary with a value of 1.
```python
def count_word_frequencies(words):
    """
    Counts the frequency of each word in a list.
    Returns a dictionary mapping each word to its frequency.
    """
    word_counts = {}
    for word in words:
        #.get(key, default) is useful to handle first-time occurrences
        word_counts[word] = word_counts.get(word, 0) + 1
    return word_counts

# Example
word_list = ["apple", "banana", "apple", "orange", "banana", "apple"]
frequencies = count_word_frequencies(word_list)
print(f"Word frequencies: {frequencies}")
# Expected Output: {'apple': 3, 'banana': 2, 'orange': 1}
```

### HashSets
A set is an unordered collection of **unique** elements. The key characteristics are that sets do not allow duplicate values and the elements are not stored in any particular order. Like hash maps, sets are implemented using a hash table, which allows for highly efficient membership testing (checking if an element is in a set). The elements of a set must be immutable. Sets are particularly useful for tasks that involve uniqueness, such as removing duplicates from a list, and for performing mathematical set operations like union, intersection, and difference.

#### Operational Analysis and Complexity
- **add, remove, and contains (membership testing)**: The time complexity for these core operations is **O(1)** on average, thanks to the underlying hash table implementation.
- **Set Operations (union, intersection, etc.)**: The complexity depends on the sizes of the sets involved. For example, `set1.intersection(set2)` is $O(min(len(s1),\space len(s2)))$.

#### Python Implementation
Python's built-in `set` type provides a direct implementation of the set data structure.
```python
# Creating a set (duplicates are automatically removed)
my_set = {1, 2, 3, 2, 4, 5, 1}
print(f"Initial set: {my_set}")

# Adding an element (O(1) on average)
my_set.add(6)
print(f"After adding 6: {my_set}")

# Removing an element (O(1) on average)
my_set.remove(3) # Raises KeyError if element not found
my_set.discard(10) # Does not raise an error
print(f"After removing 3: {my_set}")

# Membership testing (O(1) on average)
print(f"Is 4 in the set? {4 in my_set}")
print(f"Is 10 in the set? {10 in my_set}")

# Set operations
set_a = {1, 2, 3, 4}
set_b = {3, 4, 5, 6}

# Union: all elements from both sets
print(f"Union: {set_a.union(set_b)}")

# Intersection: elements common to both sets
print(f"Intersection: {set_a.intersection(set_b)}")

# Difference: elements in set_a but not in set_b
print(f"Difference (A-B): {set_a.difference(set_b)}")
```

#### Example Problem: Remove Duplicates from a List
**Problem:** Given a list of elements, return a new list with all duplicate elements removed.
**Explanation:** This is a classic use case for sets. By converting the list into a set, all duplicates are automatically discarded due to the inherent properties of a set. Then, we can convert the set back into a list to get the desired result. The order of elements in the final list is not guaranteed.
```python
def remove_duplicates(data_list):
    """
    Removes duplicate elements from a list.
    Returns a new list with unique elements.
    """
    # Convert the list to a set to remove duplicates, then back to a list
    unique_elements = list(set(data_list))
    return unique_elements

# Example
my_list = [1, 5, 2, 8, 2, 5, 9, 1, 10]
unique_list = remove_duplicates(my_list)
print(f"Original list: {my_list}")
print(f"List with duplicates removed: {unique_list}")
```

|Operation|Array (Dynamic)|Linked List (Singly)|Stack (Efficient)|Queue (Efficient)|
|---|---|---|---|---|
|**Access (by index)**|O(1)|O(n)|O(n)|O(n)|
|**Search (by value)**|O(n)|O(n)|O(n)|O(n)|
|**Insertion (at beginning)**|O(n)|O(1)|O(1) (Push)|O(n)|
|**Insertion (at end)**|O(1) (amortized)|O(n) or O(1) (with tail pointer)|O(n)|O(1) (Enqueue)|
|**Deletion (from beginning)**|O(n)|O(1)|O(n)|O(1) (Dequeue)|
|**Deletion (from end)**|O(1)|O(n)|O(1) (Pop)|O(n)|

## Section 3: Advanced Data Structures
While linear data structures arrange elements in a sequence, non-linear data structures represent more complex, hierarchical, or network-like relationships. Trees and graphs are the two most important non-linear data structures.

### Trees
A tree is a non-linear hierarchical data structure consisting of a collection of nodes connected by edges. It is defined by a single topmost node called the **root**. Each node can have zero or more child nodes, forming a parent-child relationship. A key property of a tree is that there is exactly one unique path from the root to any other node in the tree.

#### Core Terminology:
- **Node**: A fundamental part of a tree that can store data and hold references (pointers) to other nodes (its children).
- **Root**: The topmost node in the tree, which has no parent.
- **Edge**: The link connecting a parent node to a child node.
- **Parent**: A node that has one or more child nodes.
- **Child**: A node that has a parent node.
- **Leaf**: A node that has no children.
- **Subtree**: A tree consisting of a node and all of its descendants.
- **Height of a Node**: The length of the longest path from that node to a leaf. The height of a leaf is 0.
- **Depth of a Node**: The length of the path from the root to that node. The depth of the root is 0.

#### Binary Search Trees (BST)
A Binary Search Tree is a special type of binary tree (a tree where each node has at most two children) that maintains a specific ordering property. This property is the key to its efficiency:

> For any given node `N`, all values in its left subtree are less than `N`'s value, and all values in its right subtree are greater than `N`'s value. This property must hold true for all nodes in the tree.

This ordering allows for highly efficient search, insertion, and deletion operations. However, this efficiency is critically dependent on the **balance** of the tree. A balanced tree has a height of approximately 'log2​n', where 'n' is the number of nodes. A completely unbalanced or "skewed" tree, where each node has only one child, degenerates into a linked list, with a height of 'n'. This structural difference directly determines the performance of its operations. The O(log n) advantage is not guaranteed; it is an outcome of maintaining a balanced structure. This is the primary motivation for the development of more complex self-balancing trees (like AVL trees and Red-Black trees), which automatically restructure themselves upon insertion and deletion to maintain a logarithmic height and guarantee worst-case 'O(logn)' performance.

#### Operations and Complexity
- **Search, Insertion, and Deletion**:
    - **Average Case (Balanced Tree)**: The time complexity for these operations is **O(logn)**. Each comparison allows the algorithm to discard about half of the remaining nodes, leading to a logarithmic search path from the root to the target node.54
    - **Worst Case (Skewed Tree)**: The time complexity degrades to **O(n)**. In a skewed tree, the search path can extend through all nodes, similar to a linear search in a linked list.51

#### Python Implementation of a BST
```python
class Node:
    def __init__(self, key):
        self.left = None
        self.right = None
        self.val = key

def insert(root, key):
    if root is None:
        return Node(key)
    else:
        if root.val < key:
            root.right = insert(root.right, key)
        else:
            root.left = insert(root.left, key)
    return root

def search(root, key):
    if root is None or root.val == key:
        return root
    if root.val < key:
        return search(root.right, key)
    return search(root.left, key)

# In-order traversal function to display the sorted tree
def inorder_traversal(root):
    if root:
        inorder_traversal(root.left)
        print(root.val, end=" ")
        inorder_traversal(root.right)

# Example usage
r = Node(50)
r = insert(r, 30)
r = insert(r, 20)
r = insert(r, 40)
r = insert(r, 70)
r = insert(r, 60)
r = insert(r, 80)

print("In-order traversal of the BST:")
inorder_traversal(r) # Output: 20 30 40 50 60 70 80
```

#### Tree Traversal Algorithms
Traversal is the process of visiting (e.g., printing, processing) each node in a tree exactly once.

- **In-order (Left, Root, Right)**: In a BST, this traversal visits the nodes in ascending sorted order. This is one of the most useful properties of a BST.
- **Pre-order (Root, Left, Right)**: This traversal is useful for creating a copy of the tree or for obtaining an expression prefix notation.
- **Post-order (Left, Right, Root)**: This is useful for processes where a node must be handled after its children, such as deleting nodes from a tree.

### Graphs
A graph is a non-linear data structure consisting of a set of **vertices** (or nodes) and a set of **edges** that connect pairs of vertices. Graphs are used to model relationships and networks, making them one of the most versatile data structures. Unlike trees, graphs can have cycles, and there are no hierarchical constraints like a single root node.

#### Core Terminology
- **Vertex (Node)**: The fundamental unit of a graph. 
- **Edge (Link/Arc)**: A connection between two vertices.
- **Undirected Graph**: Edges have no direction; the connection is symmetric.
- **Directed Graph (Digraph)**: Edges have a direction, represented by arrows.
- **Weighted Graph**: Each edge is assigned a numerical weight or cost.
- **Path**: A sequence of vertices connected by edges.
- **Cycle**: A path that starts and ends at the same vertex.

#### Representation Strategies
The choice of graph representation is a critical decision that depends on the graph's properties (specifically its density) and the operations that will be performed most frequently.
1. **Adjacency Matrix**: A 'V×V' matrix (where 'V' is the number of vertices) where the entry `matrix[i][j]` is 1 if an edge exists from vertex 'i' to vertex 'j', and 0 otherwise. For weighted graphs, the entry stores the edge's weight.
    - **Pros**: Fast edge lookup (checking for an edge between two vertices) in **O(1)** time.
    - **Cons**: Requires **O(V2)** space, which is inefficient for sparse graphs (graphs with few edges). Iterating over a vertex's neighbors takes **O(V)** time.

2. **Adjacency List**: An array of lists, where the list at index 'i' contains all the vertices adjacent to vertex 'i'.
    - **Pros**: Space-efficient for sparse graphs, requiring **O(V+E)** space (where 'E' is the number of edges). Iterating over a vertex's neighbors is efficient, proportional to the number of neighbors.
    - **Cons**: Edge lookup can be slower, taking up to 'O(V)' time in the worst case (or 'O(degree(v))').

|Feature|Adjacency Matrix|Adjacency List|
|---|---|---|
|**Space Complexity**|O(V2)|O(V+E)|
|**Edge Lookup Time**|O(1)|O(V) or O(degree(v))|
|**Neighbor Iteration Time**|O(V)|O(degree(v))|
|**Add/Remove Edge**|O(1)|O(V) or O(degree(v))|
|**Best Use Case**|Dense graphs (where E≈V2)|Sparse graphs (where E≪V2)|

#### Graph Traversal Algorithms
Traversal algorithms systematically visit every vertex and edge in a graph.
- **Breadth-First Search (BFS)**: BFS explores the graph layer by layer. It starts at a source vertex, explores all of its immediate neighbors, then the neighbors of those neighbors, and so on. It uses a **queue** to manage the order of vertices to visit. BFS is guaranteed to find the shortest path between two nodes in an unweighted graph.63
    - **Time Complexity**: **O(V+E)**
    - **Space Complexity**: **O(V)**
    ```python
    from collections import deque
    
    def bfs(graph, start_node):
        visited = set()
        queue = deque([start_node])
        visited.add(start_node)
    
        while queue:
            vertex = queue.popleft()
            print(vertex, end=" ")
    
            for neighbor in graph[vertex]:
                if neighbor not in visited:
                    visited.add(neighbor)
                    queue.append(neighbor)
    ```
    
- **Depth-First Search (DFS)**: DFS explores as far as possible along each branch before backtracking. It starts at a source vertex and explores along a path until it reaches a dead end, then backtracks to explore other unvisited paths. It typically uses a **stack** (often implemented implicitly via recursion).63
    - **Time Complexity**: **O(V+E)**
    - **Space Complexity**: **O(V)**
    ```python
    def dfs_recursive(graph, vertex, visited=None):
        if visited is None:
            visited = set()
        visited.add(vertex)
        print(vertex, end=" ")
    
        for neighbor in graph[vertex]:
            if neighbor not in visited:
                dfs_recursive(graph, neighbor, visited)
    ```

## Section 4: Essential Algorithms & Techniques
Algorithms are step-by-step procedures for solving problems or accomplishing tasks. The efficiency of these procedures is paramount, and a core part of DSA is understanding the trade-offs between different algorithmic approaches.

### 1. Searching Algorithms
Searching algorithms are designed to retrieve an element from any data structure where it is stored.
#### Linear Search:
Linear search, or sequential search, is the most straightforward searching algorithm. It sequentially checks each element in a list until a match for the target value is found or until the end of the list is reached. It can be applied to any list, sorted or unsorted.
**Algorithm**:
1. Start from the first element (index 0).
2. Compare the current element with the target value.
3. If they match, return the current index.
4. If they do not match, move to the next element.
5. Repeat until the target is found or the list ends. If the list ends without a match, the target is not present.

**Complexity**:
1. Time Complexity: **O(n)**, as in the worst case, the entire list must be scanned.
2. Space Complexity: **O(1)** for the iterative implementation.

**Use Case**: Ideal for small or unsorted datasets where simplicity is more important than raw speed.

##### Python Implementation
```python
def linear_search(data_list, target):
    """
    Returns the index of the target in the list, or -1 if not found.
    """
    for i in range(len(data_list)):
        if data_list[i] == target:
            return i
    return -1

# Example
my_list = 
target_index = linear_search(my_list, 45) # Returns 4
```

#### Binary Search
Binary search is a highly efficient "divide and conquer" algorithm that operates on **sorted / monotonic** arrays. It works by repeatedly dividing the search interval in half. If the value of the search key is less than the item in the middle of the interval, it narrows the interval to the lower half. Otherwise, it narrows it to the upper half. This process continues until the value is found or the interval is empty.

**Algorithm (Iterative)**:
1. Initialize two pointers, `low` at the start of the array and `high` at the end.
2. While `low` is less than or equal to `high`:
3. Calculate the middle index: `mid = (low + high) // 2`.
4. Compare the element at `mid` with the target.
5. If they match, return `mid`.
6. If the target is greater than the middle element, discard the left half by setting `low = mid + 1`.
7. If the target is smaller, discard the right half by setting `high = mid - 1`.
8. If the loop finishes, the target is not in the array.

**Complexity**:
1. Time Complexity: **O(logn)**, because the search space is halved in each step.
2. Space Complexity: **O(1)** for the iterative version.

**Use Case**: The standard for searching in large, sorted arrays.

##### Python Implementation:
```python
def binary_search(sorted_list, target):
    """
    Returns the index of the target in the sorted list, or -1 if not found.
    """
    low = 0
    high = len(sorted_list) - 1

    while low <= high:
        mid = (low + high) // 2
        guess = sorted_list[mid]
        if guess == target:
            return mid
        if guess < target:
            low = mid + 1
        else:
            high = mid - 1
    return -1

# Example
my_sorted_list = 
target_index = binary_search(my_sorted_list, 45) # Returns 5
```

### 2. Sorting Algorithms
Sorting algorithms arrange elements of a list in a specific order (e.g., ascending or descending). The choice of algorithm is not merely a question of which is fastest on average; it involves a nuanced consideration of trade-offs in time complexity, space complexity, stability, and performance on specific types of data. An algorithm is considered **stable** if it preserves the original relative order of equal elements. An algorithm is **in-place** if it sorts the data with only 'O(1)' or 'O(logn)' additional space.

#### Fundamental Sorts $[O(n^2)]$
These algorithms are simple to understand and implement but are inefficient for large datasets.
1. **Bubble Sort**: This algorithm repeatedly steps through the list, compares adjacent pairs of elements, and swaps them if they are in the wrong order. Passes are repeated until the list is sorted. The largest unsorted element "bubbles" to its correct position in each pass. It is a stable sort.
    ```python
    def bubble_sort(arr):
        n = len(arr)
        for i in range(n):
            swapped = False
            for j in range(0, n - i - 1):
                if arr[j] > arr[j + 1]:
                    arr[j], arr[j + 1] = arr[j + 1], arr[j]
                    swapped = True
            if not swapped:
                break # Optimization: if no swaps in a pass, list is sorted
    ```

2. **Insertion Sort**: This algorithm builds the final sorted array one item at a time. It iterates through the input elements and, for each element, it finds the correct position in the already-sorted part of the array and inserts it there by shifting larger elements one position to the right. It is stable and particularly efficient for small or nearly-sorted datasets (adaptive).
    ```python
    def insertion_sort(arr):
        for i in range(1, len(arr)):
            key = arr[i]
            j = i - 1
            while j >= 0 and key < arr[j]:
                arr[j + 1] = arr[j]
                j -= 1
            arr[j + 1] = key
    ```

#### Efficient Sorts $[O(n \space log \space n)]$
These algorithms use more sophisticated divide-and-conquer strategies to achieve significantly better performance on large datasets.

1. **Merge Sort**: A classic divide-and-conquer algorithm. It works as follows:
	1. **Divide**: Recursively divide the unsorted list into 'n' sublists, each containing one element (a list of one element is considered sorted).
	2. **Conquer (Merge)**: Repeatedly merge sublists to produce new sorted sublists until only one sublist remains.

Merge sort's performance is very consistent across best, average, and worst cases. Its primary advantages are its stability and guaranteed 'O(nlogn)' time complexity. Its main disadvantage is that it is not in-place; it requires 'O(n)' auxiliary space for the merging process.

##### Python Implementation:
```python
    def merge_sort(arr):
        if len(arr) > 1:
            mid = len(arr) // 2
            left_half = arr[:mid]
            right_half = arr[mid:]
    
            merge_sort(left_half)
            merge_sort(right_half)
    
            i = j = k = 0
            while i < len(left_half) and j < len(right_half):
                if left_half[i] < right_half[j]:
                    arr[k] = left_half[i]
                    i += 1
                else:
                    arr[k] = right_half[j]
                    j += 1
                k += 1
    
            while i < len(left_half):
                arr[k] = left_half[i]
                i += 1
                k += 1
    
            while j < len(right_half):
                arr[k] = right_half[j]
                j += 1
                k += 1
    ```

2. **Quick Sort**: Another powerful divide-and-conquer algorithm. It works as follows:
	1. **Pivot**: Select an element from the array, called the pivot.
    2. **Partition**: Reorder the array so that all elements with values less than the pivot come before it, while all elements with values greater than the pivot come after it. After this partitioning, the pivot is in its final sorted position.
    3. **Recurse**: Recursively apply the above steps to the sub-arrays of elements with smaller and greater values.

Quick sort is generally faster in practice than merge sort due to better cache performance and being an in-place sort (requiring only 'O(logn)' space for the recursion stack). However, its primary drawback is its worst-case time complexity of 'O(n2)', which occurs when the pivot selection consistently results in highly unbalanced partitions (e.g., on an already-sorted array with the first element as pivot). It is also not a stable sort.

##### Python Implementaion:
```python
    def partition(arr, low, high):
        pivot = arr[high]
        i = low - 1
        for j in range(low, high):
            if arr[j] <= pivot:
                i += 1
                arr[i], arr[j] = arr[j], arr[i]
        arr[i + 1], arr[high] = arr[high], arr[i + 1]
        return i + 1
    
    def quick_sort_recursive(arr, low, high):
        if low < high:
            pi = partition(arr, low, high)
            quick_sort_recursive(arr, low, pi - 1)
            quick_sort_recursive(arr, pi + 1, high)
    
    def quick_sort(arr):
        quick_sort_recursive(arr, 0, len(arr) - 1)
    ```

|Algorithm|Time Complexity (Best)|Time Complexity (Average)|Time Complexity (Worst)|Space Complexity (Worst)|Stability|
|---|---|---|---|---|---|
|**Bubble Sort**|O(n)|O(n2)|O(n2)|O(1)|Yes|
|**Insertion Sort**|O(n)|O(n2)|O(n2)|O(1)|Yes|
|**Merge Sort**|O(nlogn)|O(nlogn)|O(nlogn)|O(n)|Yes|
|**Quick Sort**|O(nlogn)|O(nlogn)|O(n2)|O(logn)|No|


### 3. Two-Pointers Technique
The two-pointers technique is an approach that uses two pointers, typically array indices, to traverse a data structure in a coordinated way. This method is often used on sorted arrays or linked lists to optimize search and validation tasks, commonly reducing a nested-loop 'O(n2)' complexity to a single-pass 'O(n)' complexity.

Common patterns include:
- **Opposite Ends:** One pointer starts at the beginning and the other at the end, and they move towards each other. This is useful for problems like finding pairs that sum to a target in a sorted array.
- **Same Direction (Fast and Slow):** Both pointers start at the beginning but move at different speeds. This is famously used to detect cycles in linked lists.

#### Example Problem: Two Sum in a Sorted Array
**Problem:** Given a sorted array of integers, determine if there exists a pair of numbers that sum to a given target.

**Explanation:** A brute-force approach would use nested loops to check every possible pair, resulting in 'O(n2)' time. The two-pointers technique provides an 'O(n)' solution. We place one pointer (`left`) at the start of the array and another (`right`) at the end. We then check the sum of the values at these pointers.
- If the sum is equal to the target, we've found a pair.
- If the sum is less than the target, we need a larger sum, so we increment the `left` pointer.
- If the sum is greater than the target, we need a smaller sum, so we decrement the right pointer.

We repeat this until the pointers cross, at which point we know no such pair exists.

##### Python Implementation:
```python
def has_pair_with_sum(sorted_arr, target):
    """
    Checks if a pair with the given sum exists in a sorted array.
    """
    left = 0
    right = len(sorted_arr) - 1

    while left < right:
        current_sum = sorted_arr[left] + sorted_arr[right]
        if current_sum == target:
            print(f"Pair found: ({sorted_arr[left]}, {sorted_arr[right]})")
            return True
        elif current_sum < target:
            left += 1
        else:
            right -= 1
    
    print("No pair found with the given sum.")
    return False

# Example
my_sorted_array = [1, 3, 4, 6, 8, 10, 13]
has_pair_with_sum(my_sorted_array, 13) # Output: True (3 + 10)
has_pair_with_sum(my_sorted_array, 15) # Output: False
```

### 4. Sliding Window Technique
The sliding window technique is used to efficiently solve problems involving contiguous subarrays or substrings. It involves maintaining a "window" (a sub-portion of the data) and sliding it through the data structure. This approach avoids redundant calculations by reusing the work from the previous step, transforming a brute-force approach with nested loops into a single-pass, linear-time 'O(n)' solution.

Windows can be of a **fixed size** (e.g., find the max sum of all subarrays of size 'k') or a **variable size** (e.g., find the smallest subarray whose sum is at least 'k').

#### Example Problem: Maximum Sum Subarray of Size K
**Problem:** Given an array of integers and a number 'k', find the maximum sum of any contiguous subarray of size 'k'.

**Explanation:** A naive approach would be to generate every subarray of size 'k', calculate its sum, and find the maximum, which would take 'O(n⋅k)' time. The sliding window technique optimizes this to 'O(n)'. First, we calculate the sum of the initial window of size 'k'. Then, we "slide" the window one position at a time. In each slide, we efficiently update the sum by adding the new element that enters the window and subtracting the element that leaves the window.

##### Python Implementation:
```python
def max_sum_subarray_of_size_k(arr, k):
    """
    Finds the maximum sum of a contiguous subarray of size k.
    """
    if len(arr) < k:
        return "Invalid input: array is smaller than window size k"

    # Calculate sum of the first window
    window_sum = sum(arr[:k])
    max_sum = window_sum

    # Slide the window from the start to the end of the array
    for i in range(k, len(arr)):
        # Update window sum by adding the new element and removing the old one
        window_sum = window_sum - arr[i - k] + arr[i]
        max_sum = max(max_sum, window_sum)
        
    return max_sum

# Example
my_array = [3, 5, 2, 1, 7, 8]
k = 3
print(f"Maximum sum of a subarray of size {k} is: {max_sum_subarray_of_size_k(my_array, k)}")
# Subarrays: [3, 5, 2]=10, [5, 2, 1]=8, [2, 1, 7]=10, [1, 7, 8]=16. Output: 16
```

### 5. Backtracking
Backtracking is an algorithmic technique for solving problems by recursively exploring all possible solutions.105 It builds candidates for the solution incrementally and abandons a candidate ("backtracks") as soon as it determines that the candidate cannot possibly be completed to a valid solution.

This approach is a form of brute-force search but is more optimized because it prunes branches of the search space that won't lead to a solution. It is often used for problems that involve permutations, combinations, or satisfying a set of constraints, such as solving puzzles like Sudoku or the N-Queens problem.

#### Example Problem: Generate All Valid Parentheses
**Problem:** Given 'n' pairs of parentheses, write a function to generate all combinations of well-formed parentheses. For n=3, the solution is `["((()))","(()())","(())()","()(())","()()()"]`.

**Explanation:** This problem can be solved using backtracking. We build the string from left to right. At each step, we have two choices: add an opening parenthesis `(` or a closing parenthesis `)`. We can add an opening parenthesis as long as we haven't used all 'n' of them. We can add a closing parenthesis as long as it doesn't exceed the number of opening parentheses already placed. The recursion stops when the string length reaches `2*n`.

##### Python Implementation:
```python
def generate_parentheses(n):
    """
    Generates all combinations of well-formed parentheses for n pairs.
    """
    solutions =
    
    def backtrack(current_string, open_count, close_count):
        # Base case: if the string is complete
        if len(current_string) == 2 * n:
            solutions.append(current_string)
            return
        
        # Recursive step:
        # 1. Add an opening parenthesis if we can
        if open_count < n:
            backtrack(current_string + "(", open_count + 1, close_count)
            
        # 2. Add a closing parenthesis if it's valid to do so
        if close_count < open_count:
            backtrack(current_string + ")", open_count, close_count + 1)

    # Start the backtracking process
    backtrack("", 0, 0)
    return solutions

# Example
n = 3
parentheses_combinations = generate_parentheses(n)
print(f"Valid parentheses combinations for n={n}: {parentheses_combinations}")
```

## Conclusion
This cheatsheet provides a condensed yet comprehensive overview of the essential data structures and algorithms that form the foundation of modern computing. The analysis reveals a consistent theme: there is no single "best" data structure or algorithm. Instead, the optimal choice is always contingent upon the specific requirements of the problem at hand. The decision-making process involves a careful evaluation of trade-offs between time complexity, space complexity, implementation simplicity, and other properties like stability.

The fundamental distinction between the memory layouts of arrays (contiguous) and linked lists (non-contiguous) dictates their respective performance characteristics for access, insertion, and deletion. This choice, in turn, influences the implementation of abstract data types like stacks and queues, where the selection of an underlying structure like Python's `list` versus `collections.deque` can lead to significant performance differences. For non-linear structures, the efficiency of a Binary Search Tree is shown to be critically dependent on its balance, highlighting the importance of structure in determining performance. Similarly, the choice between an Adjacency Matrix and an Adjacency List for representing graphs is dictated by the graph's density.

