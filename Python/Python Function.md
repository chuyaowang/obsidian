# Python Function

> [Python](Python.md)

## Default Argument

DO NOT use mutable types such as list and dictionary as default arguments for a function.
``` python
def add_to(num,target = [1,2,3]):
	target.append(num)
	return target

print(add_to(1))
print(add_to(2))

# Output
# [1,2,3,1]
# [1,2,3,1,2]
```

This is because the list `[1,2,3]` is created when the function is defined, not called. Therefore, each call to the function operates on this existing object.

Instead, use this

``` python
def add_to(num,target = None):
	if target is None:
		target = [1,2,3]
	target.append(num)
	return(target)
```

