# Dynamic Programming

[0. MIT CompBio Manolis Kellis](0.%20MIT%20CompBio%20Manolis%20Kellis.md)
[2. MIT CompBio - Dynamic Programming](2.%20MIT%20CompBio%20-%20Dynamic%20Programming.md)

## The Fibonacci Numbers

- The Fibonacci numbers are defined as Fib(n) = Fib(n-1) + Fib(n-2).
- It can be calculated top down or bottom up.
- To calculate Fib(4), the top down approach will calculate Fib(3) and Fib(2). However, this will involve calculating Fib(2) 2 times, as Fib(3) = Fib(2) + Fib(1). This approach has $2^n$ complexity.
- The bottom up approach calculates from Fib(0) to Fib(4). The lower numbers are stored in a table. This way, the previous results are immediately available when needed. This eliminates repeated computation.

## Hallmarks of Dynamic Programming

- **Optimal substructure**: the optimal solution to the problem is made of optimal solutions to sub-problems.
- **Overlapping subproblems**: limited number of distinct subproblems, repeated many times.

### Optimization using dynamic programming

- Optimal choice made locally: the solution to the subproblem is chosen to be the one with the highest defined *score*;
- Score is typically added through the search space;
- A traceback is done at the end to find the optimal path from individual choices.

### Middle of the difficultly range 

- Easy: [greedy](Greedy%20Algorithm.md) choices at each step makes up the best solution.
- Dynamic programming: requires a traceback to find the optimum.
- Harder: the subproblems are structured such that they depend on each other.

> [!info] Subproblems that depend on each other
> For example, if we are finding the shortest path in a graph. If the edge weights are dynamic, we cannot use the solution to subproblems stored in a table, since the answer may change at a later time.

> [!note] Greedy Algorithm vs. Dynamic Programming
> [Greedy algorithm](Greedy%20Algorithm.md) and dynamic programming are both suitable to problems with optimal substructure and overlapping subproblems.
> 
> Greedy algorithm should be used when locally optimum choices lead to globally optimum solutions, while dynamic programming should be used when the globally optimum solution can only be reached by tracing back every possible choice that are recorded.

## Memoization vs. Tabulation

> [Guide](https://www.geeksforgeeks.org/what-is-memoization-a-complete-tutorial/)

Memoization is the top-down approach of dynamic programming. It uses recursion and saves the answer to subproblems for reuse. The advantage is that when not all subproblems need to be solved, memoization is usually faster.

Tabulation is the bottom-up approach of dynamic programming. It solves every subproblem and stores the answer for reuse. This avoids recursive function calls and return statements. Tabulation is more suitable if all subproblems must be solved at least once.

## General Recipe

The dynamic programming approach has a general recipe:
1. Finding matrix parameterization of the problem: # of dimensions, variables
2. Sub-problem space:  make sure the sub-problems space is finite, not exponential
	1. If not all subproblems are solved, use memoization
	2. If subproblem reuse is not extensive, maybe dynamic programming is an overkill
3. Traversal order: sub-results ready when you need them
4. Recursion formula: larger problems is a function of subparts; fib(3) = fib(2) + fib(1) 
5. Remember choices: typically F() includes min() and max()
	1. Need representation for storing pointers
	2. Need a polynomial solution space
6. Trace-back: fill in the table of results and traceback to find optimal solution

