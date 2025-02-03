# Python List

> [Python](Python.md)

## Divide each element by a number

[Source]

### With list comprehension

``` python
l = [1,2,3]
divisor = 2
res = [x // divisor for x in l]
```

## List indexing

### Forward indexing

Forward indexing starts at 0.

``` python
a = range(10)
a[2] = 2 
```

because `range` creates a list of `0,1,2,...,9`, not including the last number, which is 10! `a[2]` corresponds to 2 in the list.

### Reverse indexing

Reverse indexing starts at -1.

``` python
a = range(10,0,-2)
a[-2] = 4
```

because `range(10,0,-2)` creates a list `10,8,6,4,2`, `a[-2]` is the second number from the back, which is 4.

### Range indexing

Range indexing starts at the first number but does not include the last number.

``` python
a = range(10)
print(a[2:4])
```

The output is `[2,3]`. Since the sliced list only includes the numbers at index 2 and 3.

## Get index of min or max

One maximum
```python
index_min = min(range(len(values)), key=values.__getitem__)
```

- `range(len(values))` gives the indices of the values in the list
- `key=values.__getitem__` makes the function compare the actual numbers in the list rather than its indices
- this returns the index corresponding to the minimum value

When there are multiple maxima
```python
index_max = [i for i,v in enumerate(scores) if v==max_score]
```

or

``` python
max_value = max(scores)
index_max = scores.index(max_value)
```
Max or min of a matrix defined as nested list, similarly with list comprehension
``` python
matrix = [
[3, 5, 9],
[1, 6, 9],
[8, 4, 7]
]

# Step 1: Find the maximum value in the matrix
max_value = max(max(row) for row in matrix)

# Step 2: Find all positions (row, col) where the value equals max_value
max_positions = [(i, j) for i, row in enumerate(matrix) for j, value in enumerate(row) if value == max_value]

print(f"Maximum value is {max_value} at positions {max_positions}")
```

## A matrix of zeros

``` python
score_matrix = [[0] * N for _ in range(M)]
```

## Match items to other items 

Uses [Python Dictionary](Python%20Dictionary.md)

``` python
max_indices = [0,2,3]
map_dict = {0:2,1:1,2:3,3:-1}
code_indices = [map_dict.get(x,x) for x in max_indices]
```

- `map_dict.get(x,x)` means get the item in the dictionary `map_dict` using `x` as the key. If x is not a key in `map`, put `x` in the list `code_indices`.

## Function map

The `map()` function is used to apply a given function to every item of an iterable, such as a list or tuple, and returns a `map` object (which is an iterator).

Example: get the max value of every sublist under `my_list`. For this purpose also see [Get index of min or max](#Get%20index%20of%20min%20or%20max). List comprehension is more versatile.
``` python
list(map(max,my_list))
```

## List from iterable

Can create a list from an iterable using `list` function.

``` python
list(range(1,10))
```