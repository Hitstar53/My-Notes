**Before Getting Started:**
> [!seealso] 
> More on Python Concepts can be found in [[Python Cheatsheet]]
> Detailed explanation on DSA can be found in [[DSA Cheatsheet]]

## Contents:
1. [[#In-Built Functions]]
2. [[#Array/Lists]]
3. [[#Stack]]\
4. [[#Queues]]
5. [[#HashMaps]]
6. [[#Strings]]
7. [[#HashSets]]
8. [[#Heaps]]
9. [[#Linked List]]
10. [[#Binary Tree]]


## Data Structures:
Before diving into implementation of data structures, here are some important python functions to remember while implementing data structures, more can be found in the above mentioned python cheatsheet.
### In-Built Functions:
```python
print(): #with sep="" and end="" arguements
sum(): #with start=val arguement
sorted(): #with reverse=T/F and key=func() arguements
map(): #takes func and iterable as arguements
filter(): #takes filter func and iterable, returns filtered iterable
range(): #with start,end,jump arguements
enumerate(): #gives index,value tuples
zip(): #combine lists, gives tuples with min len
open(): #use file path and mode="" as arguements to open a file
```

### Array/Lists:
```python
import array
arr = array.array("i", [1,2,3,4,5])
arr.append(6)

lis = [1, "two", 3, "four"]
lis.append(5) #add 5 at the last
lis.insert(x,5) #add 5 at x position
lis.extend(list) #add list to current list
lis.remove(x) #remove value 'x'
lis.pop(x) #remove value at x position
lis.sort() #for sorting
lis.reverse() #reverse order
lis.count(x)
lis.index(x)
```

### Stack:
```python
stack = []
stack.append(1) #to perform pushing
stack.pop() #to perform popping
stack[-1] #to peak
```

### Queues:
```python
from collections import deque
q = deque()
q.append(1) #to perform enqueue
q.popleft() #to perform dequeue

from queue import Queue
q = Queue(maxsize=3) #maxsize=0 means dynamic len
q.put(1) #to perform enqueue
q.get() #to perform dequeue
q.empty()
q.full()
```

### HashMaps:
```python
hm = {} or dict()
hm['key'] = value #to insert or update
hm.pop('key') #to remove value
hm.keys() #all keys as list
hm.values() #all values as list
hm.items() #all key-value tuples as list

from collections import defaultdict, OrderedDict
hm = defaultdict(type) #type: int, str, list
hm = OrderedDict() #for preserving order of insertion
```

### Strings:
```python
s = "something"
# casing-related
s.upper()
s.isupper()
s.lower()
s.islower()
s.capitalize()

#char-related
s.isalpha()
s.isnumeric()
s.alnum()
s.isdigit()
s.count("char")
s.find("char")
s.rfind("char")

#slicing & formatting
s[start:end:step]
s.strip()
s.replace(old,new)
s.split("sep")
"".join(list)
f"This is a {value}"
```

### HashSets:
```python
myset = set()
myset.add(1)
myset.add(2)
myset.remove(2)
```

### Heaps:
```python
import heapq
minHeap = []
heapq.heappush(minHeap,3)
heapq.heappush(minHeap,2)
minHeap[0]
heapq.heappop()

maxHeap = []
heapq.heappush(maxHeap,-3) #to push multiply with negative
heapq.heappush(maxHeap,-2)
-1*minHeap[0] #while removing again multiply by negative
-1*heapq.heappop()

heapq.nlargest()
heapq.nsmallest()
```

### Linked List:
```python
class Node:
	def __init__(self, data):
		self.data = data
		self.next = None

class LinkedList: 
	def __init__(self): 
		self.head = None 
		
	def insert_front(self, data): 
		new_node = Node(data) 
		if self.head is None: 
			self.head = new_node 
			return
		else:
			new_node.next = self.head
			self.head = new_node

	def insert_pos(self, data, pos):
		new_node = Node(data)
        current = self.head
        if pos == 1:
	        insert_front(data)
	    else:
		    for i in range(1, pos):
			    current - current.next
			if current != None:
				new_node.next = current.next
				current.next = new_node
			else:
				print("Invalid Pos")
			
	def insert_last(self, data): 
		new_node = Node(data)
	    if self.head is None:
	        self.head = new_node
	        return
	    current = self.head
	    while(current.next):
	        current = current.next
	    current.next = new_node
		
	def delete(self, data): 
		if self.head is None: 
			return 
		if self.head.data == data: 
			self.head = self.head.next 
			return 
		current = self.head 
		while current.next: 
			if current.next.data == data: 
				current.next = current.next.next 
				return 
			current = current.next
			
	def __str__(self): 
		current = self.head 
		while current: 
			print(current.data, end=" -> ") 
			current = current.next 
		print("None")
```

### Binary Tree:
```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

class BinaryTree:
    def __init__(self):
        self.root = None
        
    def insert(self, data):
        if self.root is None:
            self.root = Node(data)
        else:
            self._insert(self.root, data)

    def _insert(self, node, data):
        if data < node.data:
            if node.left is None:
                node.left = Node(data)
            else:
                self._insert(node.left, data)
        else:
            if node.right is None:
                node.right = Node(data)
            else:
                self._insert(node.right, data)

    def search(self, data):
        return self._search(self.root, data)

    def _search(self, node, data):
        if node is None:
            return False
        if node.data == data:
            return True
        if data < node.data:
            return self._search(node.left, data)
        else:
            return self._search(node.right, data)

    def inorder(self):
        self._inorder(self.root)

    def _inorder(self, node):
        if node is not None:
            self._inorder(node.left)
            print(node.data, end=" ")
            self._inorder(node.right)

    def preorder(self):
        self._preorder(self.root)

    def _preorder(self, node):
        if node is not None:
            print(node.data, end=" ")
            self._preorder(node.left)
            self._preorder(node.right)

    def postorder(self):
        self._postorder(self.root)

    def _postorder(self, node):
        if node is not None:
            self._postorder(node.left)
            self._postorder(node.right)
            print(node.data, end=" ")
```
