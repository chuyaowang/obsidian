# The Big O Notation

> [Cheatsheet](https://www.bigocheatsheet.com/)

A way to express the time, space, and communication etc. complexity of algorithms.
- O(n) means linear time with respect to the input

## Definition

Let f (n) and g(n) be functions from positive integers to positive reals. We say f = O(g) (which means that “f **grows** no faster than g”) if there is a constant c > 0 such that $f(n) ≤ c\cdot g(n)$.
- Or $\frac{f(n)}{g(n)}\le c$

The constant let us disregard what happens for small values of n.
- Compare $f_1(n)=n^2$ and $f_2(n)=2n+20$
- For $n<5$, $f_1$ is better, but $f_2$ scale better for larger numbers
- We want $f_2$

The Big O notation allows us to see $f_2$ is better:
- $\frac{f_2(n)}{f_1(n)}=\frac{2n+20}{n^2}\leq22$
- $\frac{f_1(n)}{f_2(n)}=\frac{n^2}{2n+20}$ cannot be bound by any constant $c$

## Other Definitions

Definition: Let f (n) and g(n) be functions from positive integers to positive reals. f = Ω(g) means g = O(f ).

Definition: Let f (n) and g(n) be functions from positive integers to positive reals. f = Θ(g) means f = O(g) and f = Ω(g).

Example: 2n + 20 = Θ(n + 1) and n 2 = Ω(n + 1).

## Common Rules

- Multiplicative constants can be omitted: $14n^2$ becomes $n^2$ . 
- $n^a$ dominates $n^b$ if $a > b$: for instance, $n^2$ dominates $n$. 
- Any exponential dominates any polynomial: $3n$ dominates $n^5$ . 
- Likewise, any polynomial dominates any logarithm: n dominates $\log(n)^3$ . This also means, for example, that $n^2$ dominates $n\log(n)$.