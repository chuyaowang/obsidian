# String Operations

> [Python](Python.md)

## Join

``` python
extracted_text = ''.join(characters)
# output: 档案阿拜多斯高中废校对策委员会
```

This code joins the list of strings in `characters` without anything between them. The empty quotes denote an empty string.

Insert a space and the strings will be joined with a space.

``` python
extracted_text = ' '.join(characters)
# output: 档案 阿拜多斯高中 废校对策委员会
```

## Replace

``` python
string.replace("pattern","replacement")
```

## Find CN characters

[Look here](https://stackoverflow.com/questions/2718196/find-all-chinese-text-in-a-string-using-python-and-regex)

## Find CN and JP characters

``` python
import re

text = 'your text with CN and JP characters'
pattern = '[\u4e00-\u9fff]+|[\u3040-\u309F\u30A0-\u30FF]+'
characters = re.findall(pattern, text)
```

re is python's regex library

## Detect matches

Use the keyword `in`

``` python
"secret" in "I have a secret"
```

[More info](https://realpython.com/python-string-contains-substring/)

## Reverse a string

``` python
'hello world'[::-1]
```

Slice notation takes the form `[start:stop:step]`. In this case, we omit the `start` and `stop` positions since we want the whole string. We also use `step = -1`, which means, "repeatedly step from right to left by 1 character".

For unicode characters like emojis

``` python
reversed_string = "".join(list(grapheme.graphemes(input_string))[::-1])
```