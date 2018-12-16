<extoc></extoc>

# Hash Table

- (key, value) pairs
- **NO duplicate keys**
- Hash Table is a general data structure
    - `HashMap` and `HashSet` are its implementationclasses in Java.
- **hash collision**
    - **close addressing** 
        - separate **chaining** - use singly linked list
    - **open addressing** - 
        - **probe** - put in the next available bucket
            - Linear probing - low cache miss when load factor is low.
            - Quadratic probing
            - Double hashing
- Data Overload
    - **rehashing**

## Problems

__P1. Top k frequent words__

- Step 1 - iterate over the composition for each word and count the words' frequencies using a hashtable.
- Step 2 - maintain a min heap of size k and get top k frequent candidates

__P2. find the one missing number in an unsorted array__

__P3. find the common numbers between two sorted arrays a[N] b[M]__


## Hash Set

Eg. __P. Kth Smallest Sum From Two Sorted Array__
can be used to store visited nodes.
time complexity $$O(n)$$ -> $$O(k)$$

## Bloom Filter

- A Bloom filter is a data structure designed to tell you, rapidly and memory-efficiently, whether an element is present in a **set**.
- To add an element to the Bloom filter, we simply hash it a few times and set the bits in the bit vector at the index of those hashes to 1.
- The base data structure of a Bloom filter is a **Bit Vector**
    - To add an element to the Bloom filter, we simply **hash it a few times** and **set the bits** in the bit vector at the index of those hashes to 1.
- The price paid for this efficiency is that a Bloom filter is a **probabilistic data structure**
    - the element either is **definitely not** in the set or **may be** in the set.
    - If the bloom filter says yes, it could be not in the set.
    - If the bloom filter says no, it must not be in the set.





