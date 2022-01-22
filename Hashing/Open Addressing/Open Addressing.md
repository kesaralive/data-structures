# Open Addressing

Like separate chaining, open addressing is a method for handling collisions. In Open Addressing, all elements are stored in the hash table itself. So at any point, the size of the table must be greater than or equal to the total number of keys (Note that we can increase table size by copying old data if needed).

- Insert(k): Keep probing until an empty slot is found. Once an empty slot is found, insert k.

- Search(k): Keep probing until slot’s key doesn’t become equal to k or an empty slot is reached.

- Delete(k): Delete operation is interesting. If we simply delete a key, then the search may fail. So slots of deleted keys are marked specially as “deleted”.

The insert can insert an item in a deleted slot, but the search doesn’t stop at a deleted slot.

### Open Addressing is done in the following ways:

1. **Linear Probing:** In linear probing, we linearly probe for next slot. For example, the typical gap between two probes is 1 as seen in the example below.

> Let hash(x) be the slot index computed using a hash function and S be the table size

    If slot hash(x) % S is full, then we try (hash(x) + 1) % S
    If (hash(x) + 1) % S is also full, then we try (hash(x) + 2) % S
    If (hash(x) + 2) % S is also full, then we try (hash(x) + 3) % S
    ..................................................
    ..................................................

### Challenges in Linear Probing

- **Primary Clustering:** One of the problems with linear probing is Primary clustering, many consecutive elements form groups and it starts taking time to find a free slot or to search for an element.
- **Secondary Clustering:** Secondary clustering is less severe, two records only have the same collision chain (Probe Sequence) if their initial position is the same.

2.  **Quadratic Probing:** We look for i<sup>2</sup>'th slot in i'th iteration.

        let hash(x) be the slot index computed using hash function.
        If slot hash(x) % S is full, then we try (hash(x) + 1*1) % S
        If (hash(x) + 1*1) % S is also full, then we try (hash(x) + 2*2) % S
        If (hash(x) + 2*2) % S is also full, then we try (hash(x) + 3*3) % S
        ..................................................
        ..................................................

3.  **Double Hashing:** We use another hash function hash2(x) and look for i\*hash2(x) slot in i'th rotation.

        let hash(x) be the slot index computed using hash function.
        If slot hash(x) % S is full, then we try (hash(x) + 1*hash2(x)) % S
        If (hash(x) + 1*hash2(x)) % S is also full, then we try (hash(x) + 2*hash2(x)) % S
        If (hash(x) + 2*hash2(x)) % S is also full, then we try (hash(x) + 3*hash2(x)) % S
        ..................................................
        ..................................................

### Comparison of above three:

- Linear probing has the best cache performance but suffers from clustering. One more advantage of Linear probing is easy to compute.
- Quadratic probing lies between the two in terms of cache performance and clustering.
- Double hashing has poor cache performance but no clustering. Double hashing requires more computation time as two hash functions need to be computed.

### Performance of Open Addressing:

Like Chaining, the performance of hashing can be evaluated under the assumption that each key is equally likely to be hashed to any slot of the table (simple uniform hashing)

        m = Number of slots in the hash table
        n = Number of keys to be inserted in the hash table

        Load factor α = n/m  ( < 1 )

        Expected time to search/insert/delete < 1/(1 - α)

        So Search, Insert and Delete take (1/(1 - α)) time

# Refferences

1. [YouTube](https://www.youtube.com/playlist?list=PLqM7alHXFySGwXaessYMemAnITqlZdZVE)
2. [Courses](http://courses.csail.mit.edu/6.006/fall11/lectures/lecture10.pdf)
3. [CSE](https://www.cse.cuhk.edu.hk/irwin.king/_media/teaching/csc2100b/tu6.pdf)
