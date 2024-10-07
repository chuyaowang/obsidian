# Binary Search

[Medium blog](https://medium.com/scriptserpent/understanding-algorithms-simple-search-vs-binary-search-in-python-a7dcbee89986)

Binary search works for **sorted data** only.

``` python
def binary_search(data, target):  
	low = 0  
	high = len(data) - 1  
	while low <= high:  
		mid = (low + high) // 2 # Integer division  
		if data[mid] == target:  
			return mid # Target found  
		elif data[mid] < target:  
			low = mid + 1 # Search in the upper half  
		else:  
			high = mid - 1 # Search in the lower half  
	return -1 # Target not found
```

**Explanation**:

Like [Linear Search](Linear%20Search.md), this function takes a sorted collection (`data`) and a `target` to find.

It initializes `low` and `high` pointers to mark the start and end of the search interval.

In each iteration, it calculates the `mid` index and compares the value at `data[mid]` with the `target`:
	If a match is found, it returns the `mid` index.
	If the `target` is larger, it adjusts the `low` pointer to start searching in the upper half.
	If the `target` is smaller, it adjusts the `high` pointer to search in the lower half.

**Time complexity**: O($log(n)$)