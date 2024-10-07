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