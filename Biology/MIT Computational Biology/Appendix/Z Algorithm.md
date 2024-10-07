# Z Algorithm

> [Z algorithm](https://www.youtube.com/watch?v=MFK0WYeVEag)

An algorithm for pattern searching without gaps.

## Problem

Find all occurrences of a pattern P with length $\lvert{P}\rvert$ in a long text T with length $\lvert{T}\rvert$.

## Naive Algorithm

Make comparisons by moving T along P. This has $O(\lvert{P}\rvert*\lvert{T}\rvert)$ complexity.

## KMP Algorithm

KMP algorithm is $O(\lvert{P}\rvert+\lvert{T}\rvert)$.

## Z Algorithm

### Z value

Z score: given a string $S$, $Z_i(s)$ is the length of the longest substring in $S$ starting at position $i$ that matches the prefix of S.

> [!note] Example
> String: `aabcaabxaaz`
> 
> Start indexing at 1
> $Z_{2}$ = 1, number of matches between  `abcaabxaaz` and `aabcaabxaaz`
> $Z_3$ = 0, number of matches between `bcaabxaaz` and `aabcaabxaaz`
> $Z_5$ = 3, number of matches between `aabxaaz` and `aabcaabxaaz`
> $Z_1$ is just the length of S

### How to use it to solve the problem

Concatenate a string $S$ with $P$ and $T$: $S = PT$.

Find all $Z_i$ values in $S$, and any $Z_i\ge\lvert{P}\rvert$ identifies an occurrence of $P$ in $T$.

Alternatively, $S = P\$T$; the dollar sign can be any symbol that is not in P or T. This way the number of matches can never exceed $\lvert{P}\rvert$, and the above statement can be changed to: Find all $Z_i$ values in $S$, and any $Z_{i}= \lvert{P}\rvert$ identifies an occurrence of $P$ in $T$.

If we can find Z values using $O(\lvert{P}\rvert+\lvert{T}\rvert)$ complexity, then the match can be found with $O(\lvert{P}\rvert+\lvert{T}\rvert)$ complexity.

#### Z boxes

The algorithm finds $Z_i$ from $i=2$ to $i=\lvert{S}\rvert$.

Given a position $i$ in the string $S$. A Z box is a range beginning at $S_i$ extending by the [Z value](#Z%20value). Shown in this picture, the boxes are Z boxes. ![](Pasted%20image%2020240527195554.png)
Since the z boxes are the longest common substring, we know that the immediate next character after the z box is not the same as the corresponding character in the prefix. ($y\ne{x}$ in the picture) 

Define $r$ to be the rightmost position in all the z boxes found. Define $l$ to be the leftmost position in the current z box that defines $r$.

####  The algorithm

`aaaabx`

Compute $Z_2$: compare the substring beginning at $i=2$ with the prefix, $Z_2=3$
$Z_2$ must be computed explicitly.

In the worst case scenario, it would take $\lvert{S}\rvert$ comparisons to calculate $Z_2$. The algorithm must be improved to avoid making S comparisons at every character, otherwise the complexity would be $O(\lvert{S}\rvert^2)$

Let's say we have $Z_2$ to $Z_{k-1}$, we want to compute $Z_k$ now:

- Case 1: $k > r$, meaning k is outside the rightmost z box. In this case, $Z_k$ must be explicitly computed like $Z_2$
- Case 2: $k \le r$, meaning k is inside the z box. Let the entire z box be $\alpha$, the part of the box beginning at k be $\beta$. There is a corresponding $\alpha'$ at the prefix. The corresponding k in the prefix is called $k'$ 
	- Case 2a: $Z_{k'}$, the Z value of $k'$, is less than $\lvert\beta\rvert$. This sub-z box is called $\gamma'$. In this case, the character immediately after $\gamma'$, called $p$, is different from the character in the corresponding position in the prefix, called $q$. Since p is part of $\alpha'$, there is also a p in $\alpha$ immediately after $\gamma$. As $p$ is different from the $q$ in the prefix, $Z_{k}= Z_{k'}$. ![](Pasted%20image%2020240529175447.png)
		- In this case, calculating $Z_k$ involves only comparing previously computed $Z_{k'}$ and $\lvert\beta\rvert$, it does not need extra character comparison.
	- Case 2b: $Z_{k'}>\lvert\beta\rvert$, meaning $\lvert{\gamma}\rvert>\lvert{\beta}\rvert$. The character immediate after $\beta$ must be different from the character immediately after $\alpha$ ($x\ne{y}$). Since the prefix also has a $\beta$ followed by $y$, $z_{k}=\lvert{\beta}\rvert$. ![](Pasted%20image%2020240529205521.png)
		- In this case, no character comparison is done.
	- Case 2c: $Z_{k'}=\lvert\beta\rvert$. We know that $p\ne{x}$ and $p\ne{q}$, but we cannot infer anything about $q$ and $x$. Explicit comparisons must be made to know about characters beyond $\alpha$. ![](Pasted%20image%2020240529210931.png)

#### Time analysis

The algorithm does at most $O(\lvert{S}\rvert)$ comparisons.

Proof: focus on r; r only increases and never decreases.

In case 1, $k>r$. A new z box can be created, and r increases.
In case 2a and 2b, no new comparison is made, r does not increase.
In case 2c, r increases if ${x}={q}$. It can increase more if the next characters also match.

In any iteration, r stays the same or moves to the right by the amount at least as large as the number of matches.

Also in any iteration where some comparisons are done, the iteration ends when the first mismatch occurs.

We can bound the number of comparisons in the entire algorithm. 
Every comparison is either a match or a mismatch.
Each iteration has at most 1 mismatch. There are $\lvert{S}\rvert$ iterations. Hence, the number of mismatches is $\le\lvert{S}\rvert$.
Every time there is a match, r moves to the right by at least the amount of matches. $r$ never moves to the left and beyond $\lvert{S}\rvert$. Hence, the number of matches is $\le\lvert{S}\rvert$.
Therefore, the number of comparisons is $\le2\lvert{S}\rvert$. This is indeed a linear algorithm.

### Application of Z Algorithm

 Given a string S and a string T, want to know if S is a rotation of T.
 S: `abxyzq`
 T: `yzqabx`
 S can be reached by moving `abx` before `yzq` in T

Naive solution: move each character to the front and make comparisons. This would take $n^2$ time.

Linear solution: takes $O(n)$ time. Run Z algorithm on `S$TT`. i.e. `abxyzq$yzqabxyzqabx` and look for any $Z_i=\lvert{S}\rvert$ in $i>\lvert{S}\rvert+1$.