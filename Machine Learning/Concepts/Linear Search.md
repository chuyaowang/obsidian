# Linear Search

[Medium blog](https://medium.com/scriptserpent/understanding-algorithms-simple-search-vs-binary-search-in-python-a7dcbee89986)

``` python
def linear_search(data, target):  
  for index, item in enumerate(data):  
    if item == target:  
      return index  # Found the target  
  return -1  # Target not in the collection
```

**Explanation:**

The `linear_search` function takes a collection of data (`data`) and the element you're searching for (`target`).

It uses the `enumerate` function within a `for` loop to both get the index and the value of each item in the `data` collection.

If the current `item` matches the `target`, the function returns the index where it was found.

If the entire loop runs without finding a match, the function returns -1.

**Time complexity**: O(n)