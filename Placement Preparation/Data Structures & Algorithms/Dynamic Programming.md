## Overview of Solving a DP Question:
1. Visualize the problem using an Example: Use a DAG or Decision Tree.
2. Identify which DP Pattern, the problem belongs to.
3. Determine State Variables. (What to be kept track of to reach optimal solution)
4. Find an appropriate Sub-Problem.
5. Find a relationship between subproblems. (How to go from 1 sp -> next sp)
6. Generalize the above relationship for 'n' subproblems.
7. Identify the Base Case and Decision Statement.
8. Implement by solving subproblems in Order.
	1. Always make a "cache" can be a matrix (if 2D) or a Hashmap (if 1D)
	2. Code out the main function, manipulate state variables, add decision conditions and return Base Case.
9. Optimize solution if needed. (Use Memoization)

## Types of Dynamic Programming:
1. 1-Dim DP: only 1 array or list of 'n' items
2. 2-Dim DP: A matrix of (i,j) or more than 1 array/list of items

## Top 5 DP Patterns:
1. Based on Fibonacci Numbers:
	1. Climbing Stairs
	2. House Robber
2. 0/1 Knapsack
	1. Target Sum
	2. Partial Equal Subset Sum
3. Unbound Knapsack
	1. Coin Change I & II
	2. Min. cost for tickets
4. Longest Common Subsequence
	1. Longest Increasing Subsequence (LIS)
	2. Edit Distance
	3. Distinct Subsequences
	4. Longest Palindromic subsequence
	5. Palindromic substrings
5. Shortest Path
	1. Unique paths I & II

## An Example:
