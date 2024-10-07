# Longest Increasing Subsequence Problem

The **Longest Increasing Subsequence (LIS)** algorithm is used to find the longest subsequence within a given sequence of numbers where the subsequence’s elements are in increasing order. The elements of the subsequence do not need to be contiguous within the original sequence, but their relative order must remain the same.

## Problem Definition

Given an array of integers `arr[]`, the goal is to find the longest subsequence such that all the elements in the subsequence are in increasing order.

### Example:

For the array `[10, 22, 9, 33, 21, 50, 41, 60, 80]`, the longest increasing subsequence is `[10, 22, 33, 50, 60, 80]`. The length of this subsequence is 6.

## Approach 1: Dynamic Programming (DP) Solution

The simplest approach to solve the problem uses dynamic programming. This algorithm has a time complexity of **O(n²)**, where `n` is the length of the array.

Here’s how the DP approach works:

### Steps:

1. **Initialize a DP table**:
   - Create a `dp[]` array where `dp[i]` represents the length of the longest increasing subsequence that ends at index `i`.
   - Initialize all `dp[i]` values to 1, since every element by itself is an increasing subsequence of length 1.

2. **Nested Loop for Subsequence**:
   - For each element `arr[i]`, look at all previous elements `arr[j]` (where `j < i`).
   - If `arr[j] < arr[i]`, then you can extend the subsequence ending at `j` by adding `arr[i]`, which means:
     $dp[i] = \max(dp[i], dp[j] + 1)$

3. **Find Maximum Length**:
   - Once the `dp[]` array is filled, the length of the LIS is the maximum value in `dp[]`.

### Example:

For the array `[10, 22, 9, 33, 21, 50, 41, 60, 80]`, the `dp[]` array would evolve as follows:

```
Initial dp[]: [1, 1, 1, 1, 1, 1, 1, 1, 1]

Comparing pairs:
    arr[1] > arr[0] → dp[1] = 2
    arr[3] > arr[1] → dp[3] = 3
    arr[3] > arr[0] → dp[3] = 3
    arr[4] > arr[0] → dp[4] = 2
    arr[5] > arr[3] → dp[5] = 4
    arr[7] > arr[3] → dp[7] = 5
    arr[8] > arr[5] → dp[8] = 6
    ...

Final dp[]: [1, 2, 1, 3, 2, 4, 4, 5, 6]
```
The LIS is the maximum value in `dp[]`, which is 6.

> Time Complexity: **O(n²)**

---

## Approach 2: Optimized Solution using Binary Search (Patience Sorting)

The more efficient algorithm uses a combination of [Greedy method](Greedy%20Algorithm.md) and [Binary Search](Binary%20Search.md). This approach improves the time complexity to **O(n log n)**.

### Steps:

1. **Initialize an empty array `lis[]`**:
   - This array will store the smallest possible tail of increasing subsequences of various lengths.

2. **Iterate through the array**:
   - For each element `arr[i]`, use binary search to find the position where `arr[i]` should be inserted in `lis[]`. This helps maintain the increasing property.
   - If `arr[i]` is greater than the largest element in `lis[]`, append it.
   - If `arr[i]` can replace an element in `lis[]` (i.e., there's a smaller or equal element), replace it to maintain the smallest possible tails.

3. **Result**:
   - The length of `lis[]` at the end gives the length of the longest increasing subsequence.

### Example:

For the array `[10, 22, 9, 33, 21, 50, 41, 60, 80]`:

```
Initial lis[]: []

Element 10: Append 10 → lis = [10]
Element 22: Append 22 → lis = [10, 22]
Element 9: Replace 10 with 9 → lis = [9, 22]
Element 33: Append 33 → lis = [9, 22, 33]
Element 21: Replace 22 with 21 → lis = [9, 21, 33]
Element 50: Append 50 → lis = [9, 21, 33, 50]
Element 41: Replace 50 with 41 → lis = [9, 21, 33, 41]
Element 60: Append 60 → lis = [9, 21, 33, 41, 60]
Element 80: Append 80 → lis = [9, 21, 33, 41, 60, 80]
```

The length of `lis[]` is 6, which is the length of the LIS.

>  Time Complexity: **O(n log n)**

---

## Key Insights:

- **Dynamic Programming (O(n²))** is simple to implement but slower for large arrays.
- **Patience Sorting (O(n log n))** uses binary search to optimize the search for subsequence lengths, providing a much faster solution for larger datasets.

Both approaches yield the same result, but the binary search method is more efficient when the input size grows.