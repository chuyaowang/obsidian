# Dictionary

[Python](Python.md)

## Update dictionary

Method 1:

``` python
d.update({"e1":0.5})
```

Method 2:

``` python
d['e1'] = 0.5
```

Will **not** work:

``` python
d.add({'e1',0.5})
```

## Delete item

``` python
del(d["e2"])
```

Removes the key-value pair of key `e2`.

## Get keys

``` python
d.keys()
```

Returns an iterable of the keys in the dictionary `d`.

## Print values

``` python
for i in d:
	print(d[i],i)
```

The output is the `i`th value in the dictionary `d` followed by the `i`th key.

Also:

``` python
for i in d.keys():
	print(d[i],i)
```