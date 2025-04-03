# Hash Table

[Blog](https://medium.com/basecs/taking-hash-tables-off-the-shelf-139cbf4752f0))

## Organizing Data

- **Book Collection as a Dataset**: Comparing a disorganized book collection to a dataset.
- **Library Organization**: The necessity of methodical organization in libraries.

## Data Structures for Organization

- **Arrays and Linked Lists**: 
  - **Arrays**: Require contiguous memory blocks.
  - [Linked List](Linked%20List.md): Do not need contiguous memory; memory can be scattered.
  - **Search Efficiency**: Linear time \(O(n)\) for searching in arrays and linked lists.
  - **Binary Search**: Possible with sorted data, achieving logarithmic time \(O(\log n)\).

## Hash Tables

- **Components**: 
  - **Array**: Holds the data.
  - **Hash Function**: Determines where data will be stored and retrieved.
- **Efficiency**: 
  - **Constant Time**: \(O(1)\) for search, insertion, and deletion.
  - **Mapping**: Relationship between keys and values.
- **Example**: 
  - **Hash Table Size**: 12 slots (hash buckets).
  - **Hash Function**: Uses modulo operator to determine the index.

## Collisions

- **Definition**: Occurs when two elements are assigned to the same hash bucket.
- **Handling Collisions**: 
  - **Phonebook Example**: Alphabetical organization leading to multiple entries per letter.
  - **Equal Distribution**: Importance of a good hash algorithm for even data distribution.

## Practical Applications

- **Libraries**: Use of the Dewey Decimal Classification System as a hash table with 10 buckets.
- **Real-World Efficiency**: 
  - **Constant Time Search**: Quick data retrieval without iterating through the entire dataset.
  - **Insertion and Deletion**: Efficient due to reliance on the hash function.

## Conclusion

- **Importance of Hash Tables**: Their efficiency and widespread use in organizing data.
- **Next Steps**: Further exploration of hash functions and collision resolution.

## Further reading

1. [Basics of Hash Tables](https://www.hackerearth.com/practice/data-structures/hash-tables/basics-of-hash-tables/tutorial/), Prateek Garg
2. [Data Structure and Algorithms — Hash Table](https://www.tutorialspoint.com/data_structures_algorithms/hash_data_structure.htm), Tutorialspoint
3. [Hash Tables](https://www.cs.auckland.ac.nz/software/AlgAnim/hash_tables.html), Professor John Morris
4. [CS210 Lab: Hash Table](http://www.cs.uregina.ca/Links/class-info/210/Hash/),University of Regina, Dept. of Computer Science
5. [Hash Tables](http://www.sparknotes.com/cs/searching/hashtables/section1.rhtml), SparkNotes
6. [Introduction to Hash Table](http://cs.boisestate.edu/~scutchin/cs321_spring2015/lectures/0305_hashtables.pdf)s, Professor Steve Cutchin


