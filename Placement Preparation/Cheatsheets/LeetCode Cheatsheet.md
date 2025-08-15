## Table of Contents:
1. [[#Introduction From Puzzles to Patterns]]
2. [[#Section 1 The Universal Problem-Solving Framework]]
3. [[#Section 2 The Art of Pattern Recognition - A Heuristic Guide]]
4. [[#Section 3 The Core Patterns - A Deep Dive]]
5. [[#Conclusion]]

## Introduction: From Puzzles to Patterns
Success in technical coding interviews, particularly those involving platforms like LeetCode, is frequently misconstrued as a function of memorizing a vast catalog of individual problems. This approach, however, is both inefficient and unsustainable. A more robust and scalable strategy is rooted in the recognition and mastery of a finite set of underlying algorithmic patterns. Most LeetCode problems are not unique puzzles but are instead variations of approximately 15 core patterns. By mastering these patterns, one can develop a problem-solving intuition that transforms unfamiliar questions into manageable variations of familiar themes.

The common practice of randomly solving problems often leads to a cycle of frustration and slow progress, as it fails to build a transferable framework of knowledge. This guide eschews that method in favor of a systematic, pattern-based curriculum. It is structured to first establish a universal framework for deconstructing any algorithmic problem, then to provide a heuristic guide for rapidly identifying the most probable pattern, and finally to offer a detailed technical deep dive into each of the core patterns. This methodology aims to replace guesswork with a structured, analytical process, enabling the development of lasting problem-solving skills.

## Section 1: The Universal Problem-Solving Framework
A structured, repeatable protocol is essential for dissecting any algorithmic problem. This framework ensures that all critical aspects of the problem are considered, from initial comprehension to final analysis. More than a personal checklist, this framework serves as a powerful communication tool during a technical interview. Articulating each step demonstrates a methodical and logical thought process, which is often more valuable to an interviewer than simply arriving at a correct solution. A candidate who can explain their journey from a brute-force approach to an optimized one proves they can solve any unfamiliar problem, not just those they have memorized.

### Phase 1: Deconstruction and Clarification
Before writing any code, one must achieve a complete and unambiguous understanding of the problem statement. This initial phase is critical for preventing wasted effort on an incorrect interpretation of the requirements.

1. **Clarify Ambiguities:** It is imperative to resolve any potential ambiguities in the problem description. A checklist of clarifying questions should be mentally prepared:
    - **Input Properties:** Is the input array sorted? Can numbers be positive, negative, or zero? Does the input permit duplicate elements?
    - **Output Requirements:** If multiple valid answers exist, which should be returned? Is a specific order required for the output? What is the expected output for edge cases where no solution exists (e.g., `null`, an empty array, `-1`)?

2. **Analyze Constraints:** The problem's constraints are not mere formalities; they are strong hints about the required time and space complexity. For instance, an input array size of $N≤10^5$ immediately invalidates a naive $O(N^2)$ solution and strongly suggests that an algorithm with $O(NlogN)$ or $O(N)$ time complexity is necessary.

3. **Work Through Examples:** Beyond the examples provided in the problem statement, it is crucial to manually construct one or two simple, custom examples. This practice helps solidify one's understanding of the logic and often reveals edge cases, such as empty inputs, single-element inputs, or inputs where all elements are identical.

### Phase 2: The Brute-Force Baseline
Formulating a brute-force solution is a strategic starting point, not a sign of weakness. This initial approach serves two primary functions: it verifies a correct understanding of the problem's logic and establishes a baseline against which optimizations can be measured. The most straightforward solution often involves nested loops to explore all possible combinations or permutations, typically resulting in a time complexity of $O(N^2)$ or worse. Outlining the logic of this naive approach demonstrates a foundational grasp of the problem before proceeding to more sophisticated solutions.

**Note:** This step is not required while solving problems in an online assessment if you already have identified the optimal approach because time is key, but it is crucial while working through a solution in an interview as it shows your thought process to the interviewer.

### Phase 3: Optimization and Pattern Matching
The transition from a brute-force to an optimal solution is the most critical phase of the problem-solving process. The inefficiencies inherent in the brute-force method, specifically, the redundant computations are the primary indicators for which algorithmic pattern to apply. For example, if a brute-force solution for a subarray problem repeatedly recalculates the sum of overlapping subarrays, this points directly toward the **Sliding Window** or **Prefix Sum** patterns, which are designed to eliminate such re-computations. This phase involves a conscious effort to map the problem's characteristics and the brute-force solution's bottlenecks to the patterns detailed in [[#Section 2 The Art of Pattern Recognition - A Heuristic Guide|Section 2]].

### Phase 4: Implementation and Verification
The implementation phase is where the conceptual solution is translated into clean, readable, and correct code.

- **Code with Clarity:** Use descriptive variable names (e.g., `left`, `right` for pointers; `freq_map` for a frequency counter) to enhance code readability.
- **Dry Run:** Before submitting or running the code, perform a manual walk-through with a simple example and a known edge case. This "dry run" is an effective technique for catching off-by-one errors, incorrect loop conditions, or other logical flaws, and it demonstrates a methodical and careful approach to an interviewer.

### Phase 5: Complexity Analysis
A complete solution includes a precise analysis of its performance. This involves articulating the time and space complexity using Big $O$ notation, which describes the algorithm's behavior as the input size grows.

- **Time Complexity:** Analyze the number of operations relative to the input size, N. A single loop over the input is typically $O(N)$. Nested loops often result in $O(N^2)$ however, it is not always the case. Algorithms that repeatedly halve the search space, such as binary search, are $O(log \space N)$.
- **Space Complexity:** Analyze the amount of auxiliary memory used by the algorithm. Constant space, $O(1)$, is used for a fixed number of variables. If a data structure's size (e.g., a hash map or a new array) scales linearly with the input size, the space complexity is $O(N)$.

## Section 2: The Art of Pattern Recognition - A Heuristic Guide
Expert problem-solvers recognize patterns based on subtle clues within a problem's description. This section codifies that intuition into a systematic, quick-reference guide. It acts as a diagnostic tool to map problem characteristics to the most probable algorithmic patterns, accelerating the learning curve for pattern recognition and providing a structured starting point when faced with an unfamiliar problem.

| If the problem involves...                                                                  | Consider using...                   | Reasoning & Keywords                                                                                                                          |
| ------------------------------------------------------------------------------------------- | ----------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| A **sorted** array, list, or matrix. A condition which makes the array monotonic in nature. | **Binary Search**, **Two Pointers** | "Sorted" is the strongest signal. Binary Search for finding an element/boundary. Two Pointers for finding pairs/subsequences.                 |
| Finding a max/min/longest/shortest **contiguous** subarray/substring                        | **Sliding Window**                  | Keywords: "subarray", "substring", "contiguous". Optimizes from $O(N^2)$ to $O(N)$ by avoiding re-computation.                                |
| Finding pairs or triplets in a **sorted array** that meet a condition                       | **Two Pointers** (Opposite Ends)    | Efficiently explores pairs by moving pointers inward, leveraging the sorted order to eliminate search space.                                  |
| A **linked list** with cycles, or finding the middle/Nth from end                           | **Two Pointers** (Fast & Slow)      | The "Floyd's Cycle-Finding Algorithm" is the canonical use case. The relative speed of the pointers reveals properties of the list structure. |
| Generating **all permutations, combinations, or subsets**                                   | **Backtracking**                    | The problem asks for "all possible" solutions, requiring an exhaustive search of the solution space. Backtracking prunes invalid paths.       |
| Finding the **shortest path** in an **unweighted** graph/tree/matrix                        | **Breadth-First Search (BFS)**      | BFS explores layer by layer, guaranteeing that the first time a node is reached, it is via the shortest path.                                 |
| Exploring all paths, checking connectivity, or traversing a tree/graph deeply               | **Depth-First Search (DFS)**        | DFS goes as deep as possible down one path before backtracking. Simpler to implement recursively.                                             |
| Finding the **top/smallest/largest 'K' elements**                                           | **Heap (Priority Queue)**           | A heap is specifically designed to efficiently provide access to the min/max element in a collection in $O(log \space N)$ time.               |
| Optimization problems with **overlapping subproblems** (max/min, count ways)                | **Dynamic Programming (DP)**        | Keywords: "max/min cost", "number of ways", "longest/shortest path". The problem can be broken down into smaller, reusable subproblems.       |
| Needing to find the sum/product of a **range** in an array multiple times                   | **Prefix Sum**                      | Pre-calculating sums allows for $O(1)$ range queries, avoiding repeated $O(N)$ calculations.                                                  |
| Finding the **next greater/smaller element** for each item in an array                      | **Monotonic Stack**                 | The stack maintains a strict order, efficiently finding the next element that breaks that order for all previous elements.                    |
| Dealing with groups/components and checking **connectivity** (e.g., network)                | **Union-Find (DSU)**                | Highly efficient for dynamically merging components and checking if two elements belong to the same component.                                |
| Problems involving string **prefixes**, autocomplete, or spellcheckers                      | **Trie (Prefix Tree)**              | A trie is a specialized tree structure optimized for prefix-based string operations.                                                          |

## Section 3: The Core Patterns - A Deep Dive
This section provides a detailed technical analysis of each of the essential LeetCode patterns. Each pattern is presented as a self-contained module, complete with its core concept, common variations, code templates, and a curated list of practice problems designed to build mastery.

### 1. Two Pointers
#### Core Concept
The Two Pointers technique involves using two integer indices (the "pointers") to traverse a data structure, typically in a single pass. This approach is a powerful optimization for problems that would otherwise require nested loops, reducing the time complexity from $O(N^2)$ to a linear $O(N)$. The fundamental insight is that the movement of the pointers is logical and directional, based on a condition, which allows for the systematic elimination of portions of the search space.

#### Common Subtypes
1. **Opposite Direction Pointers (Converging)**
    - **Use Case:** This subtype is most effective on **sorted arrays** for problems requiring the identification of a pair or triplet that satisfies a specific condition (e.g., summing to a target value). One pointer begins at the start of the array (`left`), and the other begins at the end (`right`).
    - **Logic:** The sorted property of the array is paramount. The sum of the elements at the `left` and `right` pointers is compared to the target. If the sum is too small, the `left` pointer is incremented to introduce a larger value. If the sum is too large, the `right` pointer is decremented to introduce a smaller value. This process continues until the pointers meet or cross, having explored all potential pairs in a single pass.
        
2. **Fast & Slow Pointers (Same Direction)**
    - **Use Case:** This subtype is predominantly used in **linked lists** and sometimes in arrays. It is the standard approach for detecting cycles (Floyd's Cycle-Finding Algorithm), finding the middle element, or determining the Nth element from the end.
    - **Logic:** A "fast" pointer advances more steps per iteration (e.g., two nodes) than a "slow" pointer (e.g., one node). Their relative distance changes predictably. In a linked list with a cycle, the fast pointer is guaranteed to eventually "lap" and meet the slow pointer. When the fast pointer reaches the end of a list, the slow pointer will be at the middle.

#### General Code Template
1. **Opposite Direction Pointers Template**
    ```python
    def two_pointers_opposite(arr, target):
        left, right = 0, len(arr) - 1
        while left < right:
            current_sum = arr[left] + arr[right]
            if current_sum == target:
                # Condition met, return or process result
                return [left, right]
            elif current_sum < target:
                left += 1  # Move towards a larger sum
            else:
                right -= 1 # Move towards a smaller sum
        return -1 # Condition not met
    ```

2. **Fast & Slow Pointers Template (Cycle Detection)**
    ```python
    class ListNode:
        def __init__(self, x):
            self.val = x
            self.next = None
    
    def fast_slow_pointers_cycle_detection(head: ListNode) -> bool:
        slow, fast = head, head
        while fast is not None and fast.next is not None:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                # Cycle detected
                return True
        return False # No cycle
    ```

#### Curated Practice Problems

| Problem                                 | Difficulty | Link                                                                    | Why it's a good example                                                                                                                                                 |
| --------------------------------------- | ---------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 167. Two Sum II - Input Array Is Sorted | Easy       | [Link](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) | The canonical example of opposite-direction pointers on a sorted array.                                                                                                 |
| 125. Valid Palindrome                   | Easy       | [Link](https://leetcode.com/problems/valid-palindrome/)                 | A classic use of opposite-direction pointers to check for symmetry by converging from both ends of a string.                                                            |
| 11. Container With Most Water           | Medium     | [Link](https://leetcode.com/problems/container-with-most-water/)        | A clever application where the greedy choice is to move the pointer of the shorter line inward, as it's the only way to potentially increase the area.                  |
| 15. 3Sum                                | Medium     | [Link](https://leetcode.com/problems/3sum/)                             | Extends the Two Sum II pattern by fixing one number with an outer loop and applying two pointers to the remainder of the sorted array.                                  |
| 42. Trapping Rain Water                 | Hard       | [Link](https://leetcode.com/problems/trapping-rain-water/)              | A complex problem that can be solved optimally with two pointers moving from the ends, tracking the maximum height encountered on each side to calculate trapped water. |

### 2. Sliding Window
#### Core Concept
The Sliding Window pattern is an optimization technique applied to problems involving contiguous subarrays or substrings. It uses two pointers, often named `left` and `right`, to define a "window" over a segment of the data. This window slides through the data structure, expanding and contracting as needed, to find a portion that satisfies a given condition. This method transforms a brute-force approach with nested loops $O(N^2)$ into a single-pass linear solution $O(N)$ by efficiently reusing calculations from overlapping windows.

#### Common Subtypes
1. **Fixed-Size Window**
    - **Use Case:** Problems where the size of the subarray or substring, `k`, is predetermined. The goal is typically to find the window with the maximum sum, minimum average, or some other aggregate property.
    - **Logic:** The window maintains a constant size. As the `right` pointer advances to include a new element, the `left` pointer also advances to exclude the element that is now outside the window. The key to efficiency is updating the window's state in $O(1)$ time by adding the new element's value and subtracting the outgoing element's value, thus avoiding a full re-computation of the window's contents.

2. **Variable-Size (Dynamic) Window**
    - **Use Case:** Problems that ask for the _longest_ or _shortest_ subarray or substring that satisfies a certain property (e.g., longest substring with at most `k` distinct characters, minimum size subarray with a sum greater than or equal to a target).
    - **Logic:** The window dynamically changes size. The `right` pointer always moves forward, expanding the window. When the window's state violates the given condition (becomes "invalid"), the `left` pointer moves forward, contracting the window until it becomes "valid" again. The optimal length (max or min) is updated each time the window is in a valid state.

#### General Code Template
1. **Fixed-Size Window Template**
    ```python
    def fixed_sliding_window(arr, k):
        # Initialize window state with the first k elements
        window_sum = sum(arr[:k])
        max_sum = window_sum
    
        # Slide the window from k to the end
        for right in range(k, len(arr)):
            # Update window sum in O(1): add new element, remove old element
            window_sum += arr[right] - arr[right - k]
            max_sum = max(max_sum, window_sum)
    
        return max_sum
    ```

2. **Variable-Size Window Template (Longest)**
    ```python
    def variable_sliding_window_longest(arr):
        left = 0
        max_length = 0
        # `state` can be a hash map, a counter, etc., to track the window's property
        state = {} 
    
        for right in range(len(arr)):
            # 1. Expand the window by adding arr[right] to the state
            # update_state_add(state, arr[right])
    
            # 2. Contract the window while the condition is invalid
            while not is_valid(state):
                # update_state_remove(state, arr[left])
                left += 1
    
            # 3. Update the answer with the current valid window size
            max_length = max(max_length, right - left + 1)
    
        return max_length
    ```  

#### Curated Practice Problems

| Problem                                           | Difficulty | Link                                                                                  | Why it's a good example                                                                                                                             |
| ------------------------------------------------- | ---------- | ------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| 643. Maximum Average Subarray I                   | Easy       | [Link](https://leetcode.com/problems/maximum-average-subarray-i/)                     | A perfect introduction to the fixed-size sliding window pattern, requiring the calculation of the maximum average over all subarrays of size `k`.   |
| 567. Permutation in String                        | Medium     | [Link](https://leetcode.com/problems/permutation-in-string/)                          | A fixed-size window problem where the state is tracked using a frequency map (hash map) to check for anagrams.                                      |
| 3. Longest Substring Without Repeating Characters | Medium     | [Link](https://leetcode.com/problems/longest-substring-without-repeating-characters/) | The quintessential variable-size sliding window problem. The "invalid" condition is finding a repeating character, tracked with a hash set.         |
| 209. Minimum Size Subarray Sum                    | Medium     | [Link](https://leetcode.com/problems/minimum-size-subarray-sum/)                      | A classic variable-size window problem where the goal is to find the _shortest_ valid window whose sum is `>=` a target.                            |
| 239. Sliding Window Maximum                       | Hard       | [Link](https://leetcode.com/problems/sliding-window-maximum/)                         | A challenging problem combining a fixed-size sliding window with a monotonic queue (deque) to efficiently find the maximum in O(1) for each window. |

### 3. Binary Search
#### Core Concept
Binary Search is a highly efficient searching algorithm designed for **sorted** data structures. Its core principle is "divide and conquer." The algorithm repeatedly divides the search interval in half, comparing the target value to the middle element. If the target is smaller, the search continues in the left half; if larger, it continues in the right half. This process eliminates half of the remaining search space with each comparison, resulting in a logarithmic time complexity of $O(log \space N)$, a significant improvement over the $O(N)$ complexity of a linear search.

#### Common Subtypes
1. **Standard Binary Search:** This is the classic application, used to find if a specific target value exists within a sorted array and, if so, to return its index.

2. **Boundary Search (First/Last Occurrence):** A common variation is to find the first or last occurrence of an element in an array with duplicates, or the first element that is greater than or equal to a target. This requires subtle modifications to the standard template to ensure the search space shrinks correctly while preserving the potential answer.

3. **Binary Search on the Answer:** This advanced technique is applied when the search space is not the input array itself but a monotonic range of possible answers (e.g., minimum time, maximum capacity). A helper function, `check(mid)`, is created to determine if a given answer `mid` is feasible. This creates a boolean condition across the answer space (e.g., `False, False,..., True, True`), which can then be binary searched to find the first `True` value (the optimal answer).

#### General Code Template
This robust template is designed for boundary searches, which can be easily adapted for standard searches. It finds the first index where a given condition becomes true.
```python
def binary_search_boundary(arr, condition_func):
    left, right = 0, len(arr) - 1
    ans = -1  # Initialize with a default "not found" value

    while left <= right:
        mid = left + (right - left) // 2
        # condition_func should be a function that returns True or False
        if condition_func(arr[mid]):
            ans = mid         # Found a potential answer
            right = mid - 1   # Try to find an even better one in the left half
        else:
            left = mid + 1    # Condition not met, search in the right half
    
    return ans
```

#### Curated Practice Problems

| Problem                            | Difficulty | Link                                                                  | Why it's a good example                                                                                                                                            |
| ---------------------------------- | ---------- | --------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 704. Binary Search                 | Easy       | [Link](https://leetcode.com/problems/binary-search/)                  | The most fundamental implementation, essential for mastering the core logic of dividing the search space.                                                          |
| 35. Search Insert Position         | Easy       | [Link](https://leetcode.com/problems/search-insert-position/)         | A simple yet effective problem for practicing boundary search, as it requires finding the position where an element _would be_.                                    |
| 33. Search in Rotated Sorted Array | Medium     | [Link](https://leetcode.com/problems/search-in-rotated-sorted-array/) | A classic variation that requires modifying the binary search logic to first identify which half of the rotated array is sorted before narrowing the search space. |
| 875. Koko Eating Bananas           | Medium     | [Link](https://leetcode.com/problems/koko-eating-bananas/)            | A perfect example of "Binary Search on the Answer." The search is performed on the range of possible eating speeds, not the array of banana piles.                 |
| 4. Median of Two Sorted Arrays     | Hard       | [Link](https://leetcode.com/problems/median-of-two-sorted-arrays/)    | A highly challenging problem that uses binary search on the partition of one array to find the overall median of two arrays in $O(log \space min(m,n))$ time.      |

### 4. Graph Traversals (BFS & DFS)
Graph traversal algorithms are fundamental for problems involving interconnected data, such as networks, matrices, and trees. Breadth-First Search (BFS) and Depth-First Search (DFS) are the two primary methods for exploring a graph's nodes and edges.

#### Core Concept: BFS (Breadth-First Search)
BFS explores a graph layer by layer. Starting from a source node, it visits all of its immediate neighbors first, then the neighbors of those neighbors, and so on. This level-by-level traversal is achieved using a **queue** data structure (First-In, First-Out). Because it explores the closest nodes first, BFS is naturally suited for finding the **shortest path** in an unweighted graph.

#### Core Concept: DFS (Depth-First Search)
DFS explores a graph by going as deep as possible down one path before backtracking. Starting from a source node, it explores one branch completely, then backtracks to explore other branches. This traversal is typically implemented using **recursion** (which implicitly uses the call stack) or an explicit **stack** (Last-In, First-Out). DFS is well-suited for problems involving pathfinding, checking for connectivity, cycle detection, and exploring all possible routes.

#### General Code Template
1. **BFS on Graph Template**
    ```python
    from collections import deque
    
    def bfs(graph, start_node):
        queue = deque([start_node])
        visited = {start_node}
    
        while queue:
            node = queue.popleft()
            # Process node here
            print(node)
    
            for neighbor in graph[node]:
                if neighbor not in visited:
                    visited.add(neighbor)
                    queue.append(neighbor)
    ```

2. **DFS on Graph Template (Recursive)**
    ```python
    def dfs_recursive(graph, node, visited):
        visited.add(node)
        # Process node here
        print(node)
    
        for neighbor in graph[node]:
            if neighbor not in visited:
                dfs_recursive(graph, neighbor, visited)
    
    # Initial call
    # visited = set()
    # dfs_recursive(graph, start_node, visited)
    ```

#### Curated Practice Problems

| Problem                                | Difficulty | Link                                                                     | Why it's a good example                                                                                                                                                                                                                                             |
| -------------------------------------- | ---------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 200. Number of Islands                 | Medium     | [Link](https://leetcode.com/problems/number-of-islands/)                 | A classic matrix traversal problem. Either BFS or DFS can be used to explore and "sink" an island (a connected component of '1's) to count the total number of islands.                                                                                             |
| 102. Binary Tree Level Order Traversal | Medium     | [Link](https://leetcode.com/problems/binary-tree-level-order-traversal/) | The quintessential BFS problem. It requires traversing a tree level by level and storing the nodes at each level, perfectly matching the BFS exploration pattern.                                                                                                   |
| 994. Rotting Oranges                   | Medium     | [Link](https://leetcode.com/problems/rotting-oranges/)                   | A multi-source BFS problem. The search starts from all initially rotten oranges simultaneously, and the number of "levels" in the BFS corresponds to the minutes passed.                                                                                            |
| 133. Clone Graph                       | Medium     | [Link](https://leetcode.com/problems/clone-graph/)                       | Tests a deep understanding of graph traversal and node mapping. A hash map is used to store visited nodes and their clones to avoid infinite loops and redundant work. Both BFS and DFS are viable approaches.                                                      |
| 127. Word Ladder                       | Hard       | [Link](https://leetcode.com/problems/word-ladder/)                       | A challenging problem that requires finding the shortest transformation sequence between two words. This can be modeled as a graph problem where words are nodes and a one-letter difference is an edge, making it a perfect fit for BFS to find the shortest path. |

### 5. Backtracking
#### Core Concept
Backtracking is an algorithmic technique for solving problems recursively by trying to build a solution incrementally, one piece at a time, and removing those solutions that fail to satisfy the constraints of the problem at any point in time. It is a refined brute-force approach that systematically explores the entire solution space. When a path is determined to be invalid, the algorithm "backtracks" to the previous decision point and explores a different path. This method is ideal for problems that require generating all possible solutions, such as permutations, combinations, and subsets.

#### Logic and Structure
The process can be visualized as a decision tree. At each node, a choice is made. The algorithm then recursively explores the consequences of that choice. If a path leads to a dead end or an invalid solution, it returns to the parent node and explores an alternative choice.

The core components of a backtracking algorithm are:
1. **Choice:** A set of available options at the current state.
2. **Constraint:** A rule that determines if a choice is valid.
3. **Goal:** A condition that determines if a complete solution has been found.

#### General Code Template
This template provides a foundational structure for most backtracking problems.
```python
def backtrack(current_state,...other_params):
    # 1. Base Case: Check if a solution is found
    if is_solution(current_state):
        add_solution(current_state)
        return

    # 2. Iterate through all possible choices
    for choice in get_choices(current_state):
        # 3. Apply the choice
        make_choice(current_state, choice)
        
        # 4. Recurse
        backtrack(current_state,...other_params)
        
        # 5. Backtrack: Undo the choice
        undo_choice(current_state, choice)

# Example for generating subsets
def find_subsets(nums):
    result =
    current_subset =

    def backtrack(start_index):
        # Add the current subset to the result
        result.append(list(current_subset))
        
        # Explore further choices
        for i in range(start_index, len(nums)):
            # Make a choice
            current_subset.append(nums[i])
            # Recurse
            backtrack(i + 1)
            # Backtrack
            current_subset.pop()
    
    backtrack(0)
    return result
```

#### Curated Practice Problems

| Problem             | Difficulty | Link                                                   | Why it's a good example                                                                                                                                                                                        |
| ------------------- | ---------- | ------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 78. Subsets         | Medium     | [Link](https://leetcode.com/problems/subsets/)         | The fundamental backtracking problem. It requires generating all possible combinations of elements (the power set), which maps directly to the "choose/don't choose" decision structure of backtracking.       |
| 46. Permutations    | Medium     | [Link](https://leetcode.com/problems/permutations/)    | A classic problem for generating all orderings of a set of elements. It introduces the need to track used elements to avoid duplicates in a single permutation.                                                |
| 39. Combination Sum | Medium     | [Link](https://leetcode.com/problems/combination-sum/) | A variation where elements can be reused. This problem teaches how to control the recursive calls to allow for repeated choices versus unique choices.                                                         |
| 79. Word Search     | Medium     | [Link](https://leetcode.com/problems/word-search/)     | Applies backtracking to a 2D grid (matrix). The algorithm explores paths from each cell to find a word, backtracking when a path no longer matches the target word.                                            |
| 51. N-Queens        | Hard       | [Link](https://leetcode.com/problems/n-queens/)        | A canonical backtracking problem that requires placing N queens on an N×N chessboard without them attacking each other. It perfectly illustrates the concept of pruning the search space based on constraints. |

### 6. Heap (Priority Queue)
#### Core Concept
A Heap is a specialized tree-based data structure that satisfies the heap property: in a **min-heap**, for any given node, its value is less than or equal to the values of its children; in a **max-heap**, its value is greater than or equal to the values of its children. This structure ensures that the minimum (or maximum) element is always at the root of the tree. Heaps are commonly used to implement **Priority Queues**, which are abstract data types that efficiently provide access to the element with the highest (or lowest) priority. Key operations like insertion and deletion of the min/max element have a time complexity of $O(log \space N)$, making heaps ideal for problems involving finding the "top K" or "smallest K" elements.

#### Common Use Cases
- **Top K Elements:** Finding the Kth largest/smallest element, or the top K most frequent items. A min-heap of size K is used to efficiently track the K largest elements seen so far.
- **Merging Sorted Lists:** Merging K sorted lists can be done efficiently by using a min-heap to store the head of each list, always extracting the overall minimum element.
- **Scheduling:** In problems involving task scheduling based on priority, a heap can manage the tasks and always provide the one with the highest priority.

#### General Code Template
Python's `heapq` module provides an efficient implementation of a min-heap. A max-heap can be simulated by storing negated values.
```python
import heapq

# To find the Kth largest element in an array
def find_kth_largest(nums, k):
    # Use a min-heap of size k
    min_heap =
    for num in nums:
        if len(min_heap) < k:
            heapq.heappush(min_heap, num)
        elif num > min_heap:
            heapq.heapreplace(min_heap, num) # Pop smallest and push new item
    
    # The root of the min-heap is the Kth largest element
    return min_heap

# To find the K smallest elements, use a max-heap (by negating values)
def find_k_smallest(nums, k):
    max_heap =
    for num in nums:
        # Push negated value to simulate max-heap
        heapq.heappush(max_heap, -num)
        if len(max_heap) > k:
            heapq.heappop(max_heap)
    
    # Return the negated values from the heap
    return [-x for x in max_heap]
```

#### Curated Practice Problems

| Problem                              | Difficulty | Link                                                                   | Why it's a good example                                                                                                                                                                                 |
| ------------------------------------ | ---------- | ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 215. Kth Largest Element in an Array | Medium     | [Link](https://leetcode.com/problems/kth-largest-element-in-an-array/) | The quintessential "Top K" problem. It can be solved optimally using a min-heap of size K to maintain the K largest elements encountered so far.                                                        |
| 973. K Closest Points to Origin      | Medium     | [Link](https://leetcode.com/problems/k-closest-points-to-origin/)      | A variation of the Top K pattern where the priority is the distance from the origin. A max-heap is used to keep track of the K closest points.                                                          |
| 347. Top K Frequent Elements         | Medium     | [Link](https://leetcode.com/problems/top-k-frequent-elements/)         | Combines hashing (to count frequencies) and a heap (to find the top K frequent elements). A min-heap stores pairs of (frequency, element).                                                              |
| 23. Merge k Sorted Lists             | Hard       | [Link](https://leetcode.com/problems/merge-k-sorted-lists/)            | A classic problem demonstrating the power of heaps for merging. A min-heap is used to efficiently find the smallest element among the heads of all K lists.                                             |
| 295. Find Median from Data Stream    | Hard       | [Link](https://leetcode.com/problems/find-median-from-data-stream/)    | A challenging design problem solved elegantly using two heaps: a max-heap for the lower half of the numbers and a min-heap for the upper half, keeping them balanced to find the median in $O(1)$ time. |

### 7. Dynamic Programming (DP)
#### Core Concept
Dynamic Programming is a method for solving complex problems by breaking them down into a collection of simpler, overlapping subproblems. The results of these subproblems are stored (memoized or tabulated) to avoid redundant computations. DP is applicable when a problem exhibits two key properties: **optimal substructure** (the optimal solution to the overall problem can be constructed from the optimal solutions of its subproblems) and **overlapping subproblems** (the same subproblems are solved multiple times).

#### Common Approaches
1. **Top-Down with Memoization:** This approach uses recursion to solve the problem from the top (the original problem) down to the base cases. A cache (e.g., a hash map or an array) is used to store the results of subproblems. Before computing a subproblem, the algorithm checks if the result is already in the cache; if so, it returns the cached value. This approach often feels more intuitive as it directly follows the recursive structure of the problem.
    
2. **Bottom-Up with Tabulation:** This approach solves the problem iteratively, starting from the smallest subproblems (the base cases) and building up to the original problem. The results are stored in a table (e.g., a 1D or 2D array). Each entry in the table is computed based on previously computed entries. This method can be more space and time-efficient as it avoids recursion overhead.

#### General Code Template
1. **Top-Down with Memoization (Fibonacci)**
    ```python
    def fib_memo(n, memo):
        if n in memo:
            return memo[n]
        if n <= 1:
            return n
    
        memo[n] = fib_memo(n - 1, memo) + fib_memo(n - 2, memo)
        return memo[n]
    
    # Initial call
    # memo = {}
    # result = fib_memo(n, memo)
    ```

2. **Bottom-Up with Tabulation (Fibonacci)**
    ```python
    def fib_tab(n):
        if n <= 1:
            return n
    
        dp =  * (n + 1)
        dp[1] = 1
    
        for i in range(2, n + 1):
            dp[i] = dp[i - 1] + dp[i - 2]
    
        return dp[n]
    ```


#### Curated Practice Problems

| Problem                             | Difficulty | Link                                                                  | Why it's a good example                                                                                                                                                          |
| ----------------------------------- | ---------- | --------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 70. Climbing Stairs                 | Easy       | [Link](https://leetcode.com/problems/climbing-stairs/)                | A classic introductory DP problem that directly maps to the Fibonacci sequence, illustrating the concept of overlapping subproblems perfectly.                                   |
| 198. House Robber                   | Medium     | [Link](https://leetcode.com/problems/house-robber/)                   | A great example of a 1D DP problem where the decision at each step (rob or not rob) depends on the optimal solutions of previous steps.                                          |
| 322. Coin Change                    | Medium     | [Link](https://leetcode.com/problems/coin-change/)                    | A fundamental "unbounded knapsack" type problem that teaches how to build up a DP table representing the minimum coins needed for each amount up to the target.                  |
| 300. Longest Increasing Subsequence | Medium     | [Link](https://leetcode.com/problems/longest-increasing-subsequence/) | A classic DP problem that can be solved in $O(N^2)$ with a simple DP array or optimized to $O(N \space log \space N)$ using a clever combination of DP and binary search.        |
| 1143. Longest Common Subsequence    | Medium     | [Link](https://leetcode.com/problems/longest-common-subsequence/)     | A quintessential 2D DP problem where the state `dp[i][j]` represents the LCS of two strings up to indices `i` and `j`, teaching how to handle two-dimensional state transitions. |

### 8. Trees (General Traversal & Properties)
#### Core Concept
A tree is a non-linear, hierarchical data structure consisting of nodes connected by edges. Each tree has a single root node, and every node (except the root) has exactly one parent. Nodes can have zero or more children. Binary Trees, where each node has at most two children (a left and a right child), are the most common type in interviews. Problems involving trees often test understanding of traversal algorithms and recursive properties like height, depth, and balance.

#### Common Traversal Methods
Traversal is the process of visiting each node in a tree exactly once.
1. **Depth-First Search (DFS) Traversal:**
    - **Pre-order:** Visit the current node, then recursively visit the left subtree, then the right subtree (Root -> Left -> Right).
    - **In-order:** Recursively visit the left subtree, then visit the current node, then the right subtree (Left -> Root -> Right). For a Binary Search Tree (BST), this traversal visits nodes in sorted order.
    - **Post-order:** Recursively visit the left subtree, then the right subtree, then the current node (Left -> Right -> Root). This is useful for problems where a node's value depends on the results from its children (e.g., calculating tree height).

2. **Breadth-First Search (BFS) Traversal:**    
    - **Level-order:** Visits nodes level by level, from left to right within each level. This is implemented using a queue.

#### General Code Template
1. **Node Definition**
    ```python
    class TreeNode:
        def __init__(self, val=0, left=None, right=None):
            self.val = val
            self.left = left
            self.right = right
    ```

2. **In-order Traversal (Recursive DFS)**
    ```python
    def inorder_traversal(root):
        result =
        def dfs(node):
            if not node:
                return
            dfs(node.left)
            result.append(node.val)
            dfs(node.right)
        dfs(root)
        return result
    ```

3. **Level-order Traversal (BFS)**
    ```python
    from collections import deque
    
    def level_order_traversal(root):
        if not root:
            return
    
        result =
        queue = deque([root])
    
        while queue:
            level_size = len(queue)
            current_level =
            for _ in range(level_size):
                node = queue.popleft()
                current_level.append(node.val)
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            result.append(current_level)
    
        return result
    ```

#### Curated Practice Problems

| Problem                                                        | Difficulty | Link                                                                                             | Why it's a good example                                                                                                                                     |
| -------------------------------------------------------------- | ---------- | ------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 104. Maximum Depth of Binary Tree                              | Easy       | [Link](https://leetcode.com/problems/maximum-depth-of-binary-tree/)                              | A fundamental problem for understanding recursion on trees, solvable with both DFS and BFS.                                                                 |
| 226. Invert Binary Tree                                        | Easy       | [Link](https://leetcode.com/problems/invert-binary-tree/)                                        | A classic problem that solidifies understanding of recursive tree manipulation. The solution involves swapping the left and right children at each node.    |
| 100. Same Tree                                                 | Easy       | [Link](https://leetcode.com/problems/same-tree/)                                                 | An excellent exercise in simultaneous traversal of two trees to check for structural and value equality.                                                    |
| 98. Validate Binary Search Tree                                | Medium     | [Link](https://leetcode.com/problems/validate-binary-search-tree/)                               | Tests the core properties of a BST. The solution requires passing down min/max constraints during a DFS traversal to validate the entire subtree structure. |
| 105. Construct Binary Tree from Preorder and Inorder Traversal | Medium     | [Link](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/) | A challenging but essential problem that demonstrates how different traversal orders uniquely define a tree's structure.                                    |

### 9. Linked Lists
#### Core Concept
A Linked List is a linear data structure where elements are not stored in contiguous memory locations. Instead, each element, called a "node," contains data and a pointer (or reference) to the next node in the sequence. The first node is the `head`, and the last node's pointer is `null`. This structure allows for efficient insertions and deletions at the beginning $O(1)$, but accessing an element by index requires traversing the list from the head $O(N)$.

#### Common Subtypes
1. **Singly Linked List:** Each node points only to the next node. Traversal is unidirectional.
2. **Doubly Linked List:** Each node points to both the next and the previous node, allowing for bidirectional traversal.
3. **Circular Linked List:** The last node's `next` pointer points back to the `head`, forming a loop.

#### Key Techniques
1. **Dummy Head Node:** A placeholder node placed before the actual head of the list. This technique simplifies edge cases for insertion and deletion at the beginning of the list, as the head no longer needs to be treated as a special case.
2. **Two Pointers (Fast & Slow):** As covered in the Two Pointers pattern, this is crucial for cycle detection, finding the middle node, and other structural problems.
3. **In-place Reversal:** Reversing a linked list without using extra space. This involves iterating through the list and manipulating `prev`, `curr`, and `next` pointers to reverse the direction of the links.

#### General Code Template
1. **Node and List Definition**
    ```python
    class ListNode:
        def __init__(self, val=0, next=None):
            self.val = val
            self.next = next
    ```

2. **In-place Reversal Template**
    ```python
    def reverse_list(head: ListNode) -> ListNode:
        prev_node = None
        curr_node = head
    
        while curr_node:
            next_node = curr_node.next  # Store the next node
            curr_node.next = prev_node  # Reverse the current node's pointer
    
            # Move pointers one position ahead
            prev_node = curr_node
            curr_node = next_node
    
        return prev_node # New head of the reversed list
    ```

#### Curated Practice Problems

| Problem                              | Difficulty | Link                                                                    | Why it's a good example                                                                                                                                                      |
| ------------------------------------ | ---------- | ----------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 206. Reverse Linked List             | Easy       | [Link](https://leetcode.com/problems/reverse-linked-list/)              | The most fundamental linked list problem, perfect for mastering the `prev`, `curr`, `next` pointer manipulation for in-place reversal.                                       |
| 21. Merge Two Sorted Lists           | Easy       | [Link](https://leetcode.com/problems/merge-two-sorted-lists/)           | A classic problem that teaches how to merge two lists by iteratively comparing nodes. Using a dummy head simplifies the code significantly.                                  |
| 141. Linked List Cycle               | Easy       | [Link](https://leetcode.com/problems/linked-list-cycle/)                | The canonical problem for the fast and slow pointer technique (Floyd's Tortoise and Hare algorithm) to detect a cycle.                                                       |
| 19. Remove Nth Node From End of List | Medium     | [Link](https://leetcode.com/problems/remove-nth-node-from-end-of-list/) | An excellent application of the two-pointer technique where one pointer is advanced `n` steps ahead to create a gap, allowing the other pointer to land on the correct node. |
| 143. Reorder List                    | Medium     | [Link](https://leetcode.com/problems/reorder-list/)                     | A multi-step problem that combines several core linked list skills: finding the middle (fast/slow pointers), reversing the second half, and merging the two halves.          |

### 10. Merge Intervals
#### Core Concept
The Merge Intervals pattern is used for problems involving overlapping intervals. The general approach is to first **sort the intervals** based on their start times. Then, iterate through the sorted intervals and decide whether to merge the current interval with the previous one or to add it as a new, separate interval. This pattern is essential for scheduling problems, geometric problems, and data aggregation tasks.

#### Logic and Structure
1. **Sort:** The crucial first step is to sort the collection of intervals by their starting points. This ensures that we process intervals in an orderly fashion, making it possible to check for overlaps with only the most recently processed interval.
2. **Initialize:** Create a new list or data structure to store the merged intervals. Add the first interval from the sorted list to this new list.
3. **Iterate and Merge:** Loop through the remaining sorted intervals. For each current interval, compare its start time with the end time of the last interval in the merged list.
    - **If Overlap:** If the current interval's start is less than or equal to the last merged interval's end, there is an overlap. Merge them by updating the end of the last merged interval to be the maximum of the two end times.
    - **No Overlap:** If there is no overlap, the current interval is distinct. Add it as a new interval to the merged list.

#### General Code Template
```python
def merge_intervals(intervals):
    if not intervals:
        return
    
    # 1. Sort intervals based on the start time
    intervals.sort(key=lambda x: x)
    
    merged =
    merged.append(intervals)
    
    for i in range(1, len(intervals)):
        current_start, current_end = intervals[i]
        last_merged_start, last_merged_end = merged[-1]
        
        # Check for overlap
        if current_start <= last_merged_end:
            # Merge by updating the end of the last interval in the merged list
            merged[-1][1] = max(last_merged_end, current_end)
        else:
            # No overlap, add as a new interval
            merged.append(intervals[i])
            
    return merged
```

#### Curated Practice Problems

| Problem                        | Difficulty | Link                                                             | Why it's a good example                                                                                                                                                                             |
| ------------------------------ | ---------- | ---------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 56. Merge Intervals            | Medium     | [Link](https://leetcode.com/problems/merge-intervals/)           | The quintessential problem for this pattern. It directly asks to merge all overlapping intervals and is the best starting point.                                                                    |
| 57. Insert Interval            | Medium     | [Link](https://leetcode.com/problems/insert-interval/)           | A variation where a new interval is inserted into an already sorted list of non-overlapping intervals. The core logic of merging still applies.                                                     |
| 252. Meeting Rooms             | Easy       | [Link](https://leetcode.com/problems/meeting-rooms/)             | A simpler application of the pattern. After sorting, one only needs to check if any interval's start time is before the previous interval's end time.                                               |
| 253. Meeting Rooms II          | Medium     | [Link](https://leetcode.com/problems/meeting-rooms-ii/)          | A more complex scheduling problem that asks for the minimum number of rooms required. It can be solved by sorting start and end times separately or by using a min-heap to track meeting end times. |
| 435. Non-overlapping Intervals | Medium     | [Link](https://leetcode.com/problems/non-overlapping-intervals/) | A greedy problem that can be solved using the merge intervals idea. After sorting by end times, the goal is to count how many intervals must be removed to make the rest non-overlapping.           |

### 11. Prefix Sum
#### Core Concept
The Prefix Sum pattern is a pre-computation technique used to answer range query problems on an array efficiently. A prefix sum array, `prefix`, is created where `prefix[i]` stores the sum of all elements from the start of the original array up to index `i`. Once this prefix sum array is built (an $O(N)$ operation), the sum of any subarray from index `i` to `j` can be calculated in $O(1)$ time using the formula `prefix[j] - prefix[i-1]`. This avoids the need for repeated traversals over the same range, drastically improving performance for problems with multiple range sum queries.

#### Logic and Structure
1. **Build the Prefix Sum Array:**
    - Create a new array `prefix` of the same size (or size `n+1` for easier indexing).
    - Initialize `prefix = arr`.
    - Iterate from `i = 1` to `n-1` and calculate `prefix[i] = prefix[i-1] + arr[i]`.
2. **Query a Range Sum:**
    - The sum of the subarray `arr[i:j+1]` (inclusive) is `prefix[j] - prefix[i-1]`.
    - A special case is when the range starts at index 0; the sum is simply `prefix[j]`.

This concept can be extended to 2D matrices, where `prefix[i][j]` stores the sum of the rectangle from `(0,0)` to `(i,j)`.

#### General Code Template
```python
def prefix_sum_example(nums, queries):
    # 1. Build the prefix sum array
    prefix =  * len(nums)
    prefix = nums
    for i in range(1, len(nums)):
        prefix[i] = prefix[i-1] + nums[i]
    
    results =
    for start, end in queries:
        # 2. Query range sum in O(1)
        if start == 0:
            results.append(prefix[end])
        else:
            results.append(prefix[end] - prefix[start - 1])
            
    return results
```

#### Curated Practice Problems

| Problem                             | Difficulty | Link                                                                | Why it's a good example                                                                                                                                                                                             |
| ----------------------------------- | ---------- | ------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 303. Range Sum Query - Immutable    | Easy       | [Link](https://leetcode.com/problems/range-sum-query-immutable/)    | The most direct application of the 1D prefix sum pattern, designed to teach the core concept.                                                                                                                       |
| 560. Subarray Sum Equals K          | Medium     | [Link](https://leetcode.com/problems/subarray-sum-equals-k/)        | A clever and essential variation that combines prefix sums with a hash map to find the number of subarrays that sum to `k` in $O(N)$ time.                                                                          |
| 523. Continuous Subarray Sum        | Medium     | [Link](https://leetcode.com/problems/continuous-subarray-sum/)      | Similar to problem 560, but involves modular arithmetic. It tests the understanding of how prefix sums can be used with remainders.                                                                                 |
| 304. Range Sum Query 2D - Immutable | Medium     | [Link](https://leetcode.com/problems/range-sum-query-2d-immutable/) | Extends the 1D prefix sum concept to a 2D matrix, requiring a more complex formula to calculate the sum of a submatrix in $O(1)$ time.                                                                              |
| 238. Product of Array Except Self   | Medium     | [Link](https://leetcode.com/problems/product-of-array-except-self/) | A creative application of the prefix/suffix concept. The result for each index is the product of all elements to its left (prefix product) multiplied by the product of all elements to its right (suffix product). |

### 12. Monotonic Stack
#### Core Concept
A Monotonic Stack is a stack data structure where the elements are always in a sorted order (either increasing or decreasing). This property is maintained by popping elements from the stack that would violate the monotonic property before a new element is pushed. This pattern is exceptionally effective for problems that involve finding the "next greater element", "previous smaller element" or related scenarios for each element in an array. By processing the array in a single pass, it achieves an optimal $O(N)$ time complexity, as each element is pushed and popped from the stack at most once.

#### Logic and Structure
- **Monotonically Increasing Stack:** Elements in the stack are always in increasing order from bottom to top. When considering a new element, pop all elements from the stack that are greater than the new element. This is useful for finding the _previous smaller_ element.
- **Monotonically Decreasing Stack:** Elements are in decreasing order. When considering a new element, pop all elements from the stack that are smaller than the new element. This is the most common variant and is used to find the _next greater_ element.

#### General Code Template
1. **Next Greater Element (Monotonic Decreasing Stack)**
    ```python
    def next_greater_element(nums):
        stack =  # Will store indices
        result = [-1] * len(nums)
    
        for i in range(len(nums)):
            # While stack is not empty and current element is greater than
            # the element at the index on top of the stack
            while stack and nums[i] > nums[stack[-1]]:
                # The current element is the next greater element for the index on top
                top_index = stack.pop()
                result[top_index] = nums[i]
    
            # Push current index onto the stack
            stack.append(i)
    
        return result
    ```

#### Curated Practice Problems

| Problem                            | Difficulty | Link                                                                  | Why it's a good example                                                                                                                                                                                                                                |
| ---------------------------------- | ---------- | --------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 496. Next Greater Element I        | Easy       | [Link](https://leetcode.com/problems/next-greater-element-i/)         | A great introductory problem that uses a monotonic stack and a hash map to find the next greater element for items in a subset array.                                                                                                                  |
| 739. Daily Temperatures            | Medium     | [Link](https://leetcode.com/problems/daily-temperatures/)             | A classic monotonic stack problem. It asks for the number of days until a warmer temperature, which is equivalent to finding the distance to the next greater element.                                                                                 |
| 503. Next Greater Element II       | Medium     | [Link](https://leetcode.com/problems/next-greater-element-ii/)        | Adds a twist by making the array circular. This is handled elegantly by iterating through the array twice to simulate the wrap-around effect.                                                                                                          |
| 901. Online Stock Span             | Medium     | [Link](https://leetcode.com/problems/online-stock-span/)              | An online version of the "previous greater element" problem. The monotonic stack stores pairs of (price, span) to efficiently calculate the span for each new day.                                                                                     |
| 84. Largest Rectangle in Histogram | Hard       | [Link](https://leetcode.com/problems/largest-rectangle-in-histogram/) | A challenging and famous problem that can be solved optimally using a monotonic (increasing) stack to find the nearest smaller element on both sides for each bar, thus determining the maximum possible width for a rectangle with that bar's height. |

### 13. Union-Find (Disjoint Set Union)
#### Core Concept
The Union-Find, or Disjoint Set Union (DSU), data structure is used to keep track of a set of elements partitioned into a number of disjoint (non-overlapping) subsets. It provides two primary operations:
1. **Find:** Determine which subset a particular element belongs to. This can be used to check if two elements are in the same subset.
2. **Union:** Join or merge two subsets into a single subset.

This data structure is highly optimized for problems involving connectivity, such as determining connected components in a graph, checking for cycles, or network connectivity problems.

#### Optimizations
A naive implementation can be inefficient. Two key optimizations are used to achieve near-constant time complexity on average for its operations:
1. **Path Compression:** During a `find` operation, after finding the root of the set, all nodes along the path are made to point directly to the root. This flattens the tree structure, speeding up future `find` operations for those nodes.
2. **Union by Rank/Size:** When merging two sets, the root of the smaller tree (by rank/height or size) is made a child of the root of the larger tree. This helps to keep the trees from becoming too tall and unbalanced.

#### General Code Template
```python
class UnionFind:
    def __init__(self, size):
        # Each node is its own parent initially
        self.parent = list(range(size))
        # Optional: for union by rank/size
        self.rank = [1] * size

    def find(self, i):
        # Find the root of the set for element i with path compression
        if self.parent[i] == i:
            return i
        self.parent[i] = self.find(self.parent[i]) # Path compression
        return self.parent[i]

    def union(self, i, j):
        # Merge the sets containing i and j
        root_i = self.find(i)
        root_j = self.find(j)
        
        if root_i!= root_j:
            # Union by rank to keep the tree flat
            if self.rank[root_i] > self.rank[root_j]:
                self.parent[root_j] = root_i
            elif self.rank[root_i] < self.rank[root_j]:
                self.parent[root_i] = root_j
            else:
                self.parent[root_j] = root_i
                self.rank[root_i] += 1
            return True # Union was successful
        return False # Already in the same set
```

#### Curated Practice Problems

|Problem|Difficulty|Link|Why it's a good example|
|---|---|---|---|
|547. Number of Provinces|Medium|[Link](https://leetcode.com/problems/number-of-provinces/)|A direct application of Union-Find to count connected components in a graph represented by an adjacency matrix. Each `union` operation merges two cities into the same province.|
|200. Number of Islands|Medium|[Link](https://leetcode.com/problems/number-of-islands/)|While typically solved with DFS/BFS, it can also be solved with Union-Find. Each land cell is a set, and adjacent land cells are unioned. The final number of disjoint sets is the number of islands.|
|684. Redundant Connection|Medium|[Link](https://leetcode.com/problems/redundant-connection/)|A classic problem for using Union-Find to detect a cycle in an undirected graph. As edges are added, if two vertices are already in the same set, the new edge is redundant.|
|990. Satisfiability of Equality Equations|Medium|[Link](https://leetcode.com/problems/satisfiability-of-equality-equations/)|A clever problem where variables are nodes. Equality equations (`a==b`) are used to `union` variables into sets. Inequality equations (`c!=d`) are then checked to see if they violate the set structure.|
|128. Longest Consecutive Sequence|Medium|[Link](https://leetcode.com/problems/longest-consecutive-sequence/)|Although solvable with a hash set, this problem can be framed as a Union-Find problem. Each number is a set, and you `union` a number `x` with `x+1` if `x+1` exists. The answer is the size of the largest set.|

### 14. Trie (Prefix Tree)
#### Core Concept
A Trie, also known as a prefix tree, is a tree-like data structure that stores a dynamic set of strings. It is optimized for efficient retrieval of keys based on their prefixes. In a trie, each node represents a single character, and paths from the root to a node represent a prefix. A special marker in a node (e.g., a boolean flag) indicates the end of a complete word. This structure allows for operations like insertion, search, and prefix-based search (e.g., autocomplete) to be performed in $O(M)$ time, where M is the length of the string, independent of the number of words stored in the trie.

#### Structure
- **Root Node:** An empty node that serves as the starting point.
- **Nodes:** Each node typically contains:
    - A dictionary or array of pointers to its children (e.g., an array of size 26 for lowercase English letters).
    - A boolean flag `isEndOfWord` to signify if the path to this node forms a complete word.

#### General Code Template
```python
class TrieNode:
    def __init__(self):
        self.children = {}  # Mapping from character to TrieNode
        self.isEndOfWord = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word: str) -> None:
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.isEndOfWord = True

    def search(self, word: str) -> bool:
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.isEndOfWord

    def startsWith(self, prefix: str) -> bool:
        node = self.root
        for char in prefix:
            if char not in node.children:
                return False
            node = node.children[char]
        return True
```

#### Curated Practice Problems

| Problem                                         | Difficulty | Link                                                                              | Why it's a good example                                                                                                                                                                          |
| ----------------------------------------------- | ---------- | --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 208. Implement Trie (Prefix Tree)               | Medium     | [Link](https://leetcode.com/problems/implement-trie-prefix-tree/)                 | The fundamental problem for this pattern. It requires implementing the core `insert`, `search`, and `startsWith` methods, providing a solid foundation.                                          |
| 211. Design Add and Search Words Data Structure | Medium     | [Link](https://leetcode.com/problems/design-add-and-search-words-data-structure/) | A variation that adds wildcard matching ('.'). This requires modifying the search function to use backtracking (DFS) when a wildcard is encountered.                                             |
| 212. Word Search II                             | Hard       | [Link](https://leetcode.com/problems/word-search-ii/)                             | A complex problem that combines a Trie with a backtracking search on a 2D grid. The Trie is pre-built with all dictionary words, allowing for efficient pruning of the search paths on the grid. |
| 677. Map Sum Pairs                              | Medium     | [Link](https://leetcode.com/problems/map-sum-pairs/)                              | An interesting extension where each node in the Trie must also store a value (e.g., the sum of all words passing through it) to answer prefix sum queries.                                       |
| 1268. Search Suggestions System                 | Medium     | [Link](https://leetcode.com/problems/search-suggestions-system/)                  | A practical application of Tries for building an autocomplete/search suggestion system. It requires finding up to three words that share a common prefix after each character is typed.          |

### 15. Greedy Algorithms
#### Core Concept
A Greedy algorithm is an approach for solving optimization problems by making the locally optimal choice at each stage with the hope of finding a global optimum. At each step, the algorithm chooses the best available option without considering the future consequences of that choice. This strategy does not work for all optimization problems, but when it does, it often leads to simpler and more efficient solutions than other techniques like Dynamic Programming. A problem must exhibit the **greedy-choice property** (a global optimum can be arrived at by selecting a local optimum) and **optimal substructure** for a greedy approach to be valid.

#### How to Identify
Look for problems that ask to find a minimum or maximum result. Keywords like "minimize cost", "maximize profit" or "fewest number of..." are strong indicators. The key is to determine if a simple, local decision-making rule can lead to the correct overall solution without needing to backtrack or reconsider previous choices.

#### General Approach
1. **Identify the Greedy Choice:** Determine what constitutes the "best" choice at any given step. This often involves sorting the input data based on a specific criterion (e.g., end times for activities, value-to-weight ratios for knapsack items).
2. **Iterate and Build Solution:** Make the greedy choice at each step and build the solution incrementally.
3. **Prove Correctness (Conceptual):** While a formal proof is not required in an interview, one should be able to argue why the greedy strategy works. For example, in the Activity Selection Problem, choosing the activity that finishes earliest always leaves the maximum possible time for other activities.

#### Curated Practice Problems

| Problem                                 | Difficulty | Link                                                                      | Why it's a good example                                                                                                                                                                                                                       |
| --------------------------------------- | ---------- | ------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 860. Lemonade Change                    | Easy       | [Link](https://leetcode.com/problems/lemonade-change/)                    | A straightforward greedy problem. To make change, it's always optimal to use the largest available bills first (e.g., use a $10 bill before two $5 bills).                                                                                    |
| 122. Best Time to Buy and Sell Stock II | Medium     | [Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/) | The greedy choice is to accumulate profit whenever the price on the next day is higher than the current day. This simple local decision leads to the maximum total profit.                                                                    |
| 55. Jump Game                           | Medium     | [Link](https://leetcode.com/problems/jump-game/)                          | A classic greedy problem. At each position, the greedy choice is to jump to the position that offers the maximum reach for the next jump. The goal is to see if the reach can ever extend to the last index.                                  |
| 435. Non-overlapping Intervals          | Medium     | [Link](https://leetcode.com/problems/non-overlapping-intervals/)          | An interval scheduling problem. The greedy choice is to sort intervals by their end times and always select the next interval that does not overlap with the previously selected one. This maximizes the number of non-overlapping intervals. |
| 621. Task Scheduler                     | Medium     | [Link](https://leetcode.com/problems/task-scheduler/)                     | A more complex scheduling problem. The greedy strategy is to execute the most frequent task as often as possible, separated by the cooldown period, and fill the idle slots with other tasks.                                                 |

## Conclusion
Mastering the 15 core patterns provides a robust toolkit for deconstructing the vast majority of algorithmic problems encountered in coding interviews. However, the true mark of expertise lies not just in recognizing these patterns in isolation, but in understanding their interconnectivity. The most challenging problems are rarely solved by a single, straightforward application of one pattern. Instead, they are often composite problems that require a multi-stage solution, where different patterns are used as building blocks.

For instance, the `3Sum` problem is solved by first sorting the array, then iterating through it while applying the Two Pointers pattern to the remaining subarray. The `Sliding Window Maximum` problem combines the Sliding Window structure with a Monotonic Queue to maintain the window's maximum efficiently. This decomposition of a complex problem into a sequence of simpler, pattern-based subproblems is the ultimate goal of this structured learning approach.

By moving beyond the memorization of individual solutions and focusing on the underlying principles and their compositions, one can develop a flexible and powerful problem-solving methodology. This cheat sheet serves as a guide and a reference, but the ultimate objective is to internalize these patterns to the point where they become an intuitive part of one's analytical process, enabling confident and effective performance in any technical interview.