# Longest common substring problem

> [Explanation video](https://www.youtube.com/watch?v=hj-HDHwifWs)
> [0. MIT CompBio Manolis Kellis](0.%20MIT%20CompBio%20Manolis%20Kellis.md)
## Introduction

The longest common substring problem involves finding the longest common substring between two strings. The optimal solution to this problem involves [dynamic programming](Dynamic%20Programming.md).

For example: 

```
Find the longest common substring between `ACGTCATCA` and `TAGTGTCA`
```

## The naive approach

Find all substrings of the first string and all substrings of the second string. Then make all possible pairwise comparisons to find the longest common substring.

This is very inefficient for long strings.

## The sliding approach

Slide the second string along the first string one letter each time. After sliding each time, look at the overlapping portion, and determine how many letters that are the same are overlapped.

1st time:

| A   | C   | G   | T   | C   | A   | T   | C   | A   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| A   |     |     |     |     |     |     |     |     |

The overlapping parts are A and A. 
1. A and A are the same;
2. The longest common substring has length 1.

2nd time:

| A   | C   | G   | T   | C   | A   | T   | C   | A   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| C   | A   |     |     |     |     |     |     |     |
The overlapping part is AC and CA. 
1. C and A are not the same;
2. A and C are not the same;
3. The longest common substring is still 1 from the previous step.

6th time:

| A   | C   | G   | T   | C   | A   | T   | C   | A   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| G   | T   | G   | T   | C   | A   |     |     |     |
The overlapping parts are ACGTCA and GTGTCA.
1. A and A are the same;
2. C and C are the same;
3. T and T are the same;
4. G and G are the same;
5. C and T are not the same;
6. A and G are not the same;
7. The longest common substring is now 4.

Keep sliding...

After each sliding, the entire string must be traversed back to find the length of the common substring. This is time consuming. This approach has **quadratic** time complexity.

## The dynamic programming approach

- The dynamic programming approach uses a memoization matrix to store the length of the common substrings.
- Each element records the length of the longest common substring between the strings ending in that position.
- For example, row 3 column 5 is 2, meaning the length of the longest common substring between `GTG` and `ACGTC` is 2.

| A   | C   | G   | T   | C   |
| --- | --- | --- | --- | --- |
|     |     | G   | T   | G   |
- `GT` is the longest common substring

|     | A   | C   | G   | T   | C   | A   | T   | C   | A   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| G   | 0   | 0   | 1   | 0   | 0   | 0   | 0   | 0   | 0   |
| T   | 0   | 0   | 0   | 2   | 0   | 0   | 1   | 0   | 0   |
| G   | 0   | 0   | 1   | 0   | 2   | 0   | 0   | 1   | 0   |
| T   | 0   | 0   | 0   | 2   | 0   | 2   | 1   | 0   | 0   |
| C   | 0   | 1   | 0   | 0   | 3   | 0   | 0   | 2   | 0   |
| A   | 1   | 0   | 0   | 0   | 0   | 4   | 0   | 0   | 3   |

- For each row, imagine sliding the second string ending in the row letter along the columns. Then count the length of common substrings.
	- Using the example above, the 3rd row would be sliding the string `GTG` along the first string.
- However, note that the matrix records the result from sliding shorter substrings in the rows above the current row.
	- The longest common substring between `GT` and `ACGT` is 2.
- Therefore, only need to look at the rightmost letter of both strings, and decide if they match.
	- If they match, add 1 to the number at the i-1,j-1 position;
	- If they don't match, the count equals to the number at the i-1,j-1 position.
	- In the example, the rightmost letters, `G` and `C`, do not match, so the longest common substring is still 2 from the row 2 column 4 position.
- This way, repeated counting is avoided.
- The longest common substring is found to be 4 at row 6 column 6 and `GTCA`.
- This algorithm has O(m\*n) complexity.