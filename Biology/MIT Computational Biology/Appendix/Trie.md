# Trie

[Blog](https://medium.com/basecs/trying-to-understand-tries-3ec6bede0014).

## Introduction

- **Purpose**: Understanding the tradeoffs of data structures and algorithms.
- **Focus**: Tries, a data structure created to balance running time and space efficiency.

## Definition and Origin

- **Trie**: A tree-like data structure used to store a dynamic set of strings.
- **Etymology**: Derived from "retrieval"; pronounced "try" to distinguish from "tree".
- **History**: First considered in computing by René de la Briandais in 1959.

## Structure of a Trie

- **Nodes**: Store letters of an alphabet.
- **Root Node**: Empty, with links to child nodes representing possible alphabetic values.
- **Child Nodes**: Number of child nodes depends on the alphabet size (e.g., 26 for English).

## Node Composition

- **Single Node**: Contains a value (which might be null) and an array of references to child nodes (also might be null).
- **Root Node**: Has an array with 26 references for the English alphabet, initially all null.

## Building a Trie

- **Insertion**: Adding words involves creating nodes for each letter and linking them.
- **Example**: Inserting "pie" involves creating nodes for 'p', 'i', and 'e', and setting the value at the last node.

## Searching in a Trie

- **Search Hit**: Traversing nodes to find a value for a given key.
- **Search Miss**: If a node points to null, the key does not exist in the trie.

## Deleting from a Trie

- **Steps**: 
  1. Find the node containing the value and set it to null.
  2. Check if all pointers to other nodes are null; if so, remove the node.

## Comparison with Hash Tables

- **Similarities**: Both use arrays under the hood.
- **Differences**: 
  - Tries do not need a hash function.
  - Tries can have many null pointers, leading to higher memory usage.

## Advantages of Tries

- **Efficiency**: Constant time search, insertion, and deletion.
- **Predictable Array Size**: Always 26 references for the English alphabet.

## Time Complexity

- **Creation**: Worst-case runtime is $O(mn)$, where $m$ is the length of the longest key and \(n\) is the total number of keys.
- **Operations**: Searching, inserting, and deleting have a runtime of $O(an)$, where $a$ is the length of the word and $n$ is the total number of words.

## Applications

- **Autocomplete**: Used in search engines for efficient retrieval of subsets of words.
- **Spell Checkers**: Matching algorithms and radix sort implementations.

