https://www.youtube.com/watch?v=ni_w-rdItG8
https://www.youtube.com/watch?v=uKreghMwLLE
[BWT and LF mapping](https://www.youtube.com/watch?v=gqM3j2IRQH4)
[Alignment using BWT](https://www.youtube.com/watch?v=RXjc4wDV9BE)

[the paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC2705234/#SEC2.3)

## Alignment using BWT

![](Pasted%20image%2020241216003516.png)

Align `aac` to BWT string `gc$aac`:
- Start with the last letter `c`
- Update the top and bottom pointers to 4 and 5 (start indexing at 0)
	- 4 and 5 begins with `c`
- Look for lines between top and bottom where the last letter is `a` , the second last character in the query.
	- both lines ends with `a`
- these 2 `a`s correspond to the 2nd and 3rd `a` in the 1st column
- update top and bottom to 2 and 3
- Look for lines between top and bottom where the last letter is `a`
	- line 3 ends with `a`
- This corresponds to the 1st `a` in the 1st column. Update top and bottom to  1 and 1
- We found a match!
- If there was no match for the query, backtrack to a previous position and try a different base (this is more time consuming)