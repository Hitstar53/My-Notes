This session was taken as part of Amazon's Enabling Abilities Program

Mock Interview 1: (Bad)
Problem Definition:
![[Pasted image 20240626184144.png]]

Notes:
1. Doesn't ask questions/doubts.
2. Stuttering, doesn't talk much, don't think aloud.
3. Directly jumped to solving.

Basic Approach:
1. Traverse through the array for each element run another loop in the array and check if the element appears again, using a flag, this is O(N^2) time complexity due to 2 loops
2. Inserting an element at start will result in shifting n elements ahead, O(N) complexity.

Better Approach:
1. Use a hashmap, maintain count of each element in the array, so loop is run only once, then retrieve key with value '1', O(N) time complexity.
2. Insert at the end, O(1) time complexity.


Mock Interview 2: (Good)
Problem Definition:
![[Pasted image 20240626185509.png]]

Notes:
1. Asked size of expected input array, large array so linear search wont work. Use Binary search somehow on this array.
2. Thinking aloud, explaining yourself while coming up with a solution.
3. First Asked questions, understood all points and then jumped to the approach.
4. Structure the solution like a pseudo code. Makes it easier to translate algo into code.

Better Approach:
1. There are 2 subarrays which are actually sorted in this circular sorted array, so binary search can be used with some additions in logic, 0(Log N) Time Complexity.
2. Case 1: Mid = x -> return mid
3. Case 2: left array sorted: 
	1. Case 2.1: element in sorted segment: discard other - right
	2. Case 2.2: element not there: discard left
4. Case 3: right array sorted:
	1. Case 2.1: element in sorted segment: discard other half - left
	2. Case 2.2: element not there: discard right
5. Consider Edge cases, if interviews asks to debug an error in the code, review the full code using edge cases to see where it breaks or what is missing.

# Takeaway Points
![[Pasted image 20240626191520.png]]
![[Pasted image 20240626192305.png]]
![[Pasted image 20240626192448.png]]
![[Pasted image 20240626192813.png]]
![[Pasted image 20240626193117.png]]
![[Pasted image 20240626193410.png]]
