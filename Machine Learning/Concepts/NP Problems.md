# P, NP, NP hard, NP complete problems

[Medium blog](https://medium.com/@p.yun1994/p-np-np-hard-and-np-complete-problems-fe679bd1cf9c)
Review [Big O Notation](Machine%20Learning/Concepts/Big%20O%20Notation.md)

## A polynomial time algorithm

The concepts of P, NP, NP complete, and NP hard problems all have to do with an algorithm being polynomial time. It means that for an input of length _n_, the algorithm computes the solution in time $O(n^k)$ for some _constant_ k.

For example, we are interested in finding the maximum number in a list of numbers. One approach would be:

1. **Start** by assuming the first number is the maximum.
2. **Go through each number** in the list one by one.
3. **Compare** the current number with your current maximum.
4. **Update** the maximum if the current number is larger.
5. **Finish** when you’ve checked all the numbers.

For a sequence of 5 numbers, we make at most 4 comparisons. Since the algorithm run time is bounded by $n^k$, where k=1, we say that this algorithm runs in polynomial time.

## Deterministic vs. non-deterministic algorithm

- Deterministic algorithm: follows fixed, well defined steps, always the same output given the same input
- Non-deterministic: some guessing and randomness involved in the algorithm. Read more below.

## P problems

- P is the set of decision problems (problems with yes/no answers) that can be solved by a **deterministic** algorithm in **polynomial** time. In other words, if the size of the input is $n$, the algorithm solves the problem in time $O(n^k)$ for some constant $k$.
- Problems in P are considered efficiently solvable or "tractable." 
- For example, sorting numbers or finding the greatest common divisor are classic problems in P.
- P problems also takes **polynomial time** to verify an answer.

## NP problems

- **Definition 1**: NP problems can be solved by **N**on-deterministic **P**olynomial time algorithms
	- **Non-deterministic** refers to an non-deterministic Turing machine, which can take multiple directions in each computational step. If an algorithm can pick the right step every time, the problem can be solved in **polynomial** time
	- However, in reality computation is _deterministic_. Non-deterministic algorithms are only theoretical constructs, like a line with no thickness. The algorithm cannot always make perfect guesses, and all the possibilities need to be checked (in an efficient or inefficient way). This makes the run time slower than polynomial time
- **Definition 2**: A given solution of a NP problem can be _verified_ in **polynomial** time.
- The 2 definitions are **equivalent**:
	- If a problem can be solved by a nondeterministic polynomial-time algorithm, then its solution can be verified in polynomial time. This is by the very definition of NP. The nondeterministic algorithm "guesses" a solution, and if it exists, it can verify it within polynomial time.
	- If a solution can be verified in polynomial time, then there is a nondeterministic polynomial-time algorithm to find the solution. The nondeterministic algorithm can nondeterministically "guess" the certificate and then check it deterministically in polynomial time.
- Example: the Boolean Satisfiability Problem (SAT), where you determine if there exists an assignment of truth values to variables that makes a Boolean formula true, is a canonical NP problem.

> [!info]- SAT problem example
> Consider the following simple Boolean satisfiability (SAT) problem:
> 
> $F = (A \lor B) \land (\lnot A \lor B)$
> 
> ### Explanation:
> 
> - **Formula Structure:**  
>     This formula is in Conjunctive Normal Form (CNF) with two clauses:
>     
>     1. $A \lor B$
>     2. $\lnot A \lor B$
> - **The SAT Question:**  
>     Is there an assignment of truth values to the variables AA and BB that makes the entire formula FF true?
>     
> - **How to Solve:**
>     
>     - **Clause 1:** $A \lor B$ is true if at least one of $A$ or $B$ is true.
>     - **Clause 2:** $\lnot A \lor B$ is true if either $A$ is false or $B$ is true.
>     
>     Notice that **in both clauses, the variable BB appears in a positive form**. This means that if you set $B = \text{true}$, both clauses are satisfied regardless of whether $A$ is true or false.
>     
> - **Conclusion:**  
>     The formula $F$ is satisfiable because there exists at least one assignment that makes it true (for example, $B = \text{true}$ and $A$ can be either true or false).
>     
> 
> This simple example illustrates the essence of a Boolean satisfiability problem: given a logical formula, determine whether there is a way to assign truth values to its variables such that the entire formula evaluates to true.

> [!info]- Example: non-deterministic process
> ![[Media/NP Problems 2025-03-04 03.04.48.excalidraw]]
> > You need to pass 3 sets of doors (red, blue, and yellow), and you have 3 keys. Each key can open only 1 door in each set of doors. There is no information on the doors to indicate which door is the correct door. In the luckiest case, you can _guess_ all 3 correct doors in a row, and you will pass the doors in 3 steps. However, in the unluckiest case, you will have to try all the keys in all the doors.
> 
> > Here, for a given sets of doors, the steps it takes to pass through the doors depend on your luck, and this makes it a **non-deterministic** process.

### Deterministic vs. non-deterministic polynomial time

- When given without 'non-deterministic', polynomial time means deterministic polynomial time.
- The interest in NP-hardness lies in the fact that we have no evidence that these nondeterministic approaches can be efficiently simulated by deterministic algorithms.

### Different difficulty levels of NP problems

- All NP problems share the trait that **their solution can be verified in polynomial time**
- However, the difficulty of finding the solution **varies**
- The easiest subset of NP problems are the [P problems](#P%20problems), which can always be solved in polynomial time
- The most difficult ones are the NP complete problems, explained below.
- **P=NP**: a hypothesis that is **not proved** and will have tremendous implications if proved; says that all problems that takes polynomial time to verify a solution can be solved in polynomial time.
	- For example, if solving your password is as easy as verifying your password, your browser history is in grave danger!
	- one of the biggest open questions in computer science

## NP complete

- NP-complete problems are the "hardest" problems in NP. 
- If a polynomial-time algorithm can be found for any NP-complete problem, it proves $\text{P} = \text{NP}$.
- Examples:
	- **SAT (Boolean Satisfiability Problem):** The first problem proven to be NP-complete.
	- **Traveling Salesman (decision version):** Given a bound, determine if there exists a route shorter than or equal to that bound.
	- **Clique Problem:** Given a graph and a number k, decide whether the graph contains a clique of size $k$.

## Problem reduction

![[Media/NP Problems 2025-03-04 11.14.56.excalidraw]]

- A **reduction function** can take an instance of one problem (A in NP) and transform it into an instance of another problem (B in NP-hard). This function must run in _polynomial_ time.
	- The point of reduction is that an efficient solution to B means an efficient solution to A.
	- If it does not run in polynomial time, the overhead is too much. The point of reduction is lost.
- In the conversion, the answer to the problem is conserved. B has the same answer as A.
- If a polynomial time solution for B can be found, this solution can be composed with the reduction into a polynomial time solution for A.
- A systematic way (a polynomial time reduction) exists to convert an [NP problem](#NP%20problems) into an instance of the NP hard problem.
- Reduction does not have to be between NP and NP hard. NP complete problems are reduced to each other to prove they share the same level of difficulty.

### Many-to-one reduction

- Conversion can be done in different manners; one of them is called many-to-one
- An instance of problem A maps to an instance of problem B, one input one output.
- However, multiple inputs can map to the same output.

## NP hard

- Any NP problem can be reduced into a NP hard problem, but not all NP hard problems are NP.
	- NP-hard problems are _at least_ as difficult as the hardest problems in NP.
	- NP-hard problems do not necessarily belong to NP. They may not even be decision problems; they can be optimization problems or others where verifying a solution in polynomial time isn’t guaranteed.
	- NP complete problems are those NP hard problems that are also NP: whose solutions can be verified in polynomial time and can be solved using non-deterministic polynomial time algorithm.
	- To clarify, even though some NP-hard problems (for example, some optimization problems) are not in NP (their solutions cannot be verified in polynomial time), they can still be reduced to from NP problems by definition.
- Solving an NP-hard problem in polynomial time would mean that you could solve all NP problems in polynomial time, since any NP problem can be transformed into an NP-hard one.
	- Analogy: If student B knows everything student A knows, the student B is at least as smart as student A.
	- This also proves $\text{P} = \text{NP}$

### NP vs. NP hard

> Since all NP problems can be reduced to NP hard problems, why don't we just call NP problems NP hard problems?

- Different focus:
	- NP problems focus on the verifiability of the solution, not necessarily its difficulty
	- NP hard describes the difficulty. Since all NP problems can be reduced to NP hard problems, they are at least as difficult as NP problems.
- There are different difficulties of NP problems. Only the NP complete problems, the most difficult NP problems, are considered NP hard. Calling them all NP hard would blur this difference.
- There are NP hard problems that are not in NP


### Proving a problem is NP-hard

- A often heard concept is _proving_ a problem is _NP hard_
- It means to construct a _conversion function_, and show that it converts a known NP problem to the problem being proved.
- Proving NP hardness of a problem proves the problem is at least as hard as the hardest problems (NP complete) in NP. If this problem can be solved in polynomial time, then all NP problems would be solvable in polynomial time, proving $\text{P} = \text{NP}$
- However, since $\text{P} = \text{NP}$ is not proven yet, it means $\text{P} \ne \text{NP}$, so no polynomial time solution exists for NP hard problems. Hence NP hard problems are considered _intractable_ for large inputs.
- Why proving NP hardness is necessary:
	- **understanding computational limits**: a NP hard problem likely does not have a polynomial time solution;
	- **algorithm design and practical approaches**: a more practical approach to design an algorithm for an NP hard problem would be to seek approximate solutions, use heuristics, or special-case solutions that work well enough for practical applications
	- **theoretical importance**: contribution to our understanding of the boundaries between tractable and intractable problems.

![[Media/NP Problems 2025-03-03 13.01.13.excalidraw]]

## Tractability for large inputs

- P problems: tractable
- NP complete, NP hard: intractable, approximation, heuristics, or special case solutions need to be used
- NP intermediate: neither P nor NP complete
	- no polynomial time algorithm
	- but may be solvable using quasi-polynomial or sub-exponential algorithms for moderate-sized inputs

## Venn diagram: a summarization

- P problems can be solved and their solution verified in deterministic polynomial time
- NP problems can be solved in non-deterministic polynomial time and their solutions verified in polynomial time
- P is a subset of NP
- All NP problems can be converted to NP-hard problems. 
- NP hard problems are at least as difficult as NP complete problems
- NP hard problems are not necessarily NP
- Those problems that are both NP and NP hard are considered NP complete.
- Solving a NP hard problem in deterministic polynomial time = solving a NP complete problem in deterministic polynomial time = solving a NP problem in deterministic polynomial time = proving $\text{P} = \text{NP}$
	- not proven yet!

## Examples

Here's a clear example for each complexity class:

---

### P Example: Primality Testing

- **Problem:** Given an integer n, decide whether it is prime.
- **Why It's in P:**  
    The AKS primality test, discovered in 2002, runs in polynomial time, meaning that as the size of the input (the number of digits in n) grows, the time to decide primality increases only polynomially.

---

### NP Example: Integer Factorization

- **Problem:** Given an integer n, find its prime factors.
- **Why It's in NP:**  
    If someone provides a set of factors as a certificate, you can verify their correctness (by multiplying them back together) in polynomial time. Despite this efficient verification, no known algorithm can factor all integers in polynomial time.
- **Note:**  
    Although factorization is in NP, it is not known to be NP-complete.

---

### NP-Hard Example: TSP (Optimization Version)

- **Problem:** Given a list of cities and distances between each pair, determine the shortest possible route that visits each city exactly once and returns to the origin city.
- **Why It's NP-Hard:**  
    The optimization version of the Traveling Salesman Problem is NP-hard because solving it (or even approximating it within certain bounds) is at least as hard as the hardest problems in NP. Note that while the decision version (does a tour exist with cost $\leq B$?) is NP-complete, the optimization version does not necessarily lie in NP.

---

### NP-Complete Example: 3-SAT

- **Problem:** Given a Boolean formula in conjunctive normal form (CNF) where each clause has exactly three literals, determine whether there exists an assignment of truth values that satisfies the formula.
- **Why It's NP-Complete:**
    - **In NP:** If a satisfying assignment is given, it can be verified in polynomial time.
    - **NP-Hardness:** Every problem in NP can be reduced to 3-SAT in polynomial time (as shown by the Cook-Levin theorem), making it one of the canonical NP-complete problems.

---

Each example illustrates a different aspect of computational complexity, highlighting the distinctions between problems that are efficiently solvable (P), those that are verifiable efficiently (NP), the hardest problems that might be even harder than NP (NP-hard), and those that are both verifiable efficiently and as hard as any NP problem (NP-complete).