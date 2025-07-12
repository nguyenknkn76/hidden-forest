#  DATA STRUCTURES AND ALGORITHMS

# Complexities Analysis
## Basics
- Why is analysis of algo important?
- Order of growth: 
`c < loglog n < log n < n^1/2  < n < n Log n < n^2 < 2^n < n^n`
- Asymptotic analysis
- Worst, average and best case analysis of algo
## Big O Notation
`O(n!) > O(c^n) > O(n^c) > O(n.logn) > O(n) > O(logn) > O(1)`
![BigONotation](./assets//BigONo.png)

# Array
- Definition: 
  - collection of items of the same var type
  - stored at contiguous memory locations

- Basic terminologies of Array
  - arr index
  - arr element
  - arr length

```js
// declaration of arr
let arr = []
// init arr
let arr = [1, 2, 3]
```

- Why do we need array? The idea of an array is to represent many instances in one variable.
- Types of arr: 
  - basic sized: fixed size arr, dynamic sized arr
  - basic dimensions: one-dimensional arr, multi-dimensional arr

## Operations on Array
```
1. array traversal
2. insertion 
3. deletion 
4. searching
  4.1. linear search
  4.2. binary search
```
## Applications of Array
```
**1. Application**
- Storing and accessing data ~ O(1)
- Searching ~ O(logn)
- Matrices: 2-D array
- Implementing other data structures: stacks, queues
- Dynamic programing
- Data buffers

**2. Advantages**
- Efficient and fast access
- Memory efficiency: store elemens in contiguous memory
- Versatility: can store many type of data
- Compatibility with hardware

**3. Disadvantages** 
- Fixed size
- Memory allocation issues
- Insertion and deletion challenges: requiers shifting subsequent elements
- Limited data type support: limiting use with complex data types
- Lack of flexibility: < liked lists, trees
```

# Searching Algo
## Linear Search ~ O(n)
## Binary Search ~ O(logn)

# Sorting Algo
## Intro
- Why sorting algo are important? reduces complexity of a problem → application: searching algo, data algo, divide and conquer methods, and dsa
  - print big dataset (want to arrange them)
  - data sorted, can get max-item, min-item ~ O(1) 
  - binary search 
 
- Sorting basics
  - In-place sorting
  - Internal sorting
  - External sorting
  - Stable sorting
  - Hybrid sorting
- Types of sorting techniques
![sorting techniques](./assets/SortingTYPE.png)
- Some of the most common sorting algo: Selection sort, Bubble sort, Insertion Sort, Cycle Sort, Merge Sort, 3-way Merge Sort, Quick sort, Heap sort and Counting sort
- Some other: ([read more here](https://www.geeksforgeeks.org/dsa/introduction-to-sorting-algorithm/))

### Comparison of Complexity Analysis of Sorting Algorithms
| Sorting Algorithm         | Best Case    | Average Case | Worst Case   | Memory | Stable | Method Used           |
|---------------------------|--------------|--------------|--------------|--------|--------|------------------------|
| Quick Sort                | O(n log n)   | O(n log n)   | O(n²)        | log n  | No     | Partitioning          |
| Merge Sort                | O(n log n)   | O(n log n)   | O(n log n)   | n      | Yes    | Merging               |
| Heap Sort                 | O(n log n)   | O(n log n)   | O(n log n)   | 1      | No     | Selection             |
| Insertion Sort            | O(n)         | O(n²)        | O(n²)        | 1      | Yes    | Insertion             |
| Tim Sort                  | O(n)         | O(n log n)   | O(n log n)   | n      | Yes    | Insertion & Merging   |
| Selection Sort            | O(n²)        | O(n²)        | O(n²)        | 1      | No     | Selection             |
| Shell Sort                | O(n log n)   | O(n⁴⁄³)      | O(n³⁄²)      | 1      | No     | Insertion             |
| Bubble Sort               | O(n)         | O(n²)        | O(n²)        | 1      | Yes    | Exchanging            |
| Tree Sort                 | O(n log n)   | O(n log n)   | O(n log n)   | n      | Yes    | Insertion             |
| Cycle Sort                | O(n²)        | O(n²)        | O(n²)        | 1      | No     | Selection             |
| Strand Sort               | O(n)         | O(n²)        | O(n²)        | n      | Yes    | Selection             |
| Cocktail Shaker Sort      | O(n)         | O(n²)        | O(n²)        | 1      | Yes    | Exchanging            |
| Comb Sort                 | O(n log n)   | O(n²)        | O(n²)        | 1      | No     | Exchanging            |
| Gnome Sort                | O(n)         | O(n²)        | O(n²)        | 1      | Yes    | Exchanging            |
| Odd–even Sort             | O(n)         | O(n²)        | O(n²)        | 1      | Yes    | Exchanging            |

## Application
```
**1. Application**
- Quick finding k-th smallest or largest: ~ O(1)
- Searching algo: binary search, ternary search 
- Data management: sorted data → ez to search, retrieve, analyze
- Database optimization: improvees query performance 
- Machine learning: prepare data for training models
- Data analysis
- Operating system 

**2. Advantages**
- Efficiency: easier and faster to search, retrieve, and analyze info
- Improved performance: algo↑ → performance↑ 
- Simplified data analysis
- Reduced memory consumption
- Improved data visualization

**3. Disadvantages**
- Insertion
- Algo selection
- For some problems, hasing > sorting
```
## Sorting Algo (~detail)

# Hashing
This is a technique that efficiently stores and retrieves data for quick access
  - using **hash func** for mapping data to index in hash table → fast retrive info based on key
  - achieve 3 operations (search, insert, delete) ~ O(1)
  - distinct items(keys) and dictionaries (key value pairs)

## Intro
### General
- 3 operations (search, insert, del) ~ O(1) → better than arr, linked list
- app: dictionaries, frequency counting, maintaining data
- Situation where hash is not used?
  - when data needs to be sorted for operation (search, insert, del) → using **BST**
  - when keys are strings and need prefix op (like autocomplete or dictionary lookups) → using a **trie** 
  - when op (like floor and ceiling) are required → using **BST**
→ if ur app depends on the **order of elements** or involves **string manipulation** → hash table is NOT the optimal solution

- Component of Hashing: key, hash func, hash table
- How does hashing work? b/c `key ---hash-func---> index(in-hash-table)` 
  → ez to find location that value be stored in
  → good to store (key, value) pair
- What is hash func? 
- **Collision** in hashing? conflix when many keys **have same hash value** (read more: [collision techniques](https://www.geeksforgeeks.org/dsa/collision-resolution-techniques/))
- **Load Factor** in hashing? `Load Factor = Total elements in hash table/ Size of hash table`
- **Rehashing**? the load factor > predefinded value → hashs again AND stores value in the new hash table

## Applications 
```
Hashing is a powerful technique that enables search, insert, and delete operations in average constant time (~ O(1)).
**1. Common use cases:**
- Database indexing: data retrieval↑
- Dictionaries: word lookup↑
- Password storage: store hashed passwords (NOT plain text)
- Network routing: determines *optimal paths* for data packets
- Bloom Filters: appications in spam filtering, recommendation sys
- Cryptography: digital signatures, MACs, key derivation functions
- Load balancing: distributes network requests (~via consistent hashing)
- Blockchain
- Image processing
- File comparison: verifies file integrity (e.g: MD5, SHA-1)
- Fraud detection: detects malicious activity in cybersecurity tools.
- Caching
- Symbol tables
- Associative arrays: fast key-based lookup (in SQL)

**2. More specialized applications:**
- Message Digest: using hash func (like SHA-256) → verifies the integrity 
- Password Verification
- Data Structures: HashMap, dict, uncordered_map
- Compiler Operations
- Rabin-Karp Algorithm
- Mapping file name to path: `file_name → file_path`
- Graphics
```

## Separate Chaining 
This is `collision handling technique`. Multiple keys have same hash value → be stored in linked list(/dynamic arr) at same index of table.

**Advantages**
- ez to implement 
- hash table NEVER fill up 
- less depend on hash func or load factor
- good when **number of key**, **frequency of key insert(del)** is **unknown**

**Disadvantages**
- cache performance↓ (b/c using linked list)
- some slot in hash table **unused** → memory waste
- **chain(~too long)** → search time **~O(n)**
- extra memory for storing links

**Performance**
- Load factor: lf = `no of keys / no slots in table`
- Search/Del ~ O(lf)
- Insert ~ O(1)

**Data Structures for Chains**
Below are the common data structures used to store chains in separate chaining:
| Structure              | Search         | Delete         | Insert         | Cache Friendly |
|------------------------|----------------|----------------|----------------|----------------|
| **Linked List**        | O(len)         | O(len)         | O(1)           | NO             |
| **Dynamic Array**      | O(len)         | O(len)         | O(1)*          | OK              |
| **Self-Balancing BST** | O(log(len))    | O(log(len))    | O(log(len))    | NO            |
> *Insert in dynamic arrays is generally O(1), unless resizing occurs.

## Open Addressing (or Closed Hashing)
It is `collision resolution technique`. All elements are stored directly inside the table itself. When collision occurs → look for the next available slot (probing)

**Basic Operations**
- Insert(k)
- Search(k)
- Delete(k): NOT deleteing → mark as 'deleted' (search logic: unaffected)

**Probing Methods**
```
**1. Linear Probing**
- Checks the next sequential slot: `(hash(x) + i) % tableSize`
- adv: simple, cache friendly
- dis: clustering 

**2. Quadratic Probing **
- Checks increasingly spaced slots: `(hash(x) + i²) % tableSize`
- adv: reduce clustering (< linear probing)
- dis: might skip over some slots

**3. Double Hashing**
- Uses a second hash function: (hash1(x) + i × hash2(x)) % tableSize
- adv: spreads keys and avoids clustering 
- dis: cache↓, computation cost↑
```
**Comparison Between Separate Chaining and Open Addressing**
| No. | Criteria                                | Separate Chaining                                      | Open Addressing                                             |
|-----|------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------|
| 1   | Implementation Complexity                | Simpler to implement                                   | Requires more computation                                   |
| 2   | Table Capacity                           | Hash table never fills up — chains can grow indefinitely | Table may become full                                       |
| 3   | Sensitivity to Hash Function             | Less sensitive                                         | More sensitive to clustering and load factor               |
| 4   | Suitability Based on Key Frequency       | Good when key frequency is unknown                    | Best when key frequency and volume are known               |
| 5   | Cache Performance                        | Poor (keys stored via linked list)                    | Better (data stored within one array)                      |
| 6   | Space Utilization                        | May waste space (some slots never used)               | Utilizes all slots regardless of hash matches              |
| 7   | Extra Memory Usage                       | Requires extra space for links                        | No additional memory for links                             |
> **Note:** Chaining suffers from poor cache performance because linked lists require memory jumps, making it harder for the CPU to predict and cache access. Open addressing benefits from contiguous memory access.

**Performance of Open Addressing**
- Load factor: `lf = no-of-keys/ table-size`
- Expected time (search, insert, del): O\left(\frac{1}{1 - \alpha}\right)
> **Note**: lf approaches 1 → performance↓

# Two Pointer Technique

# Window Sliding Techique

# Prefix Sum Technique

# String
## Intro 
- It is a sequence of characters. In languages(Java, Python, JS), strings are generally **immutable**
- Strings are stored in contiguous memory blocks like arrays.

**Common String Operation**
- string length
- character search
- substring check
- insert char
- del char
- string equality 
- string cancatenation
- string reversal
- string rotation
- palindrome check

## Applications
```
**1. Applications**
**Common Applications**
- Plagiarism Detection
- Encoding/Decoding (Ciphering)
- Information Retrieval
- Approximate Suffix-Prefix Overlap
- Network Communication
- File Handling
- Text Analysis

**Real-time Applications**
- Spam Filtering
- Bioinformatics
- Intrusion Detection
- Search Engines

**2. Advantages**
- Text Processing: search, format, replace, manipulate text ez.
- Data Representation: encode (numbers, dates, times) as strings.
- Ease of Use: simple syntax
- Cross-Language Support
- Memory Efficient: ez allocation

**3. Disadvantages**
- High Memory Consumption: with large strings.
- Immutability: leading to overhead.
- Performance Bottlenecks: slower than another data structures
- Encoding/Decoding Issues: encodings can be complex.
- Security Risks: vulnerable to injection attacks or buffer overflows if misused
```

## Subsequence and Substring
**Substring**
- A substring is a part of a string consisting of contiguous characters.
- For a string of length n, the number of non-empty subsequences is: `\frac{n(n+1)}{2}` 

**Subsequence**
- A subsequence is a sequence that can be formed from the original string by removing zero or more characters while preserving the original order.
- For a string of length n, the number of non-empty subsequences is: `2^n - 1`

**Key diff**
- Substring → characters must be **adjacent**
- Subsequence → characters can be **non-adjacent**, but must maintain **original order**

## Some sus content about String
![alt text](./assets/SUSContentOfString.png)
> Can see that sus shit on the bottom at Geek4geek
> Click → [here](https://www.geeksforgeeks.org/dsa/introduction-to-strings-data-structure-and-algorithm-tutorials/) ← to start getting headaches x.x

# Recursion
# Matrix/Grid

# Linked List
**Comparison: Linked List vs Array**
| Feature             | Linked List                                | Array                                     |
|---------------------|---------------------------------------------|-------------------------------------------|
| Data Structure       | Non-contiguous                             | Contiguous                                 |
| Memory Allocation    | Allocated one by one per element           | Allocated as a block for entire array      |
| Insertion/Deletion   | Efficient (constant time at ends)          | Inefficient (may require shifting)         |
| Access               | Sequential (must traverse from head)       | Random (direct index access possible)      |
> Both structures are used to implement abstract data types like stacks, queues, and deques, but they differ significantly in performance and memory behavior.

## Single Linked List
## Doubly Linked List
## Circular Linked List
## Applications
```

```
## Operations

# Stack
# Queue
# Deque
# Tree 
# Heap
# Graph
# Greedy Algo
# Dynamic Programming
# Advanced DSA

# Other Algo
## Bitwise Algo
## Backtracking Algo
## Devide and Conquer
## Branch and Bound 
## Geometric Algo
## Randomized Algo

> Read more about: 
> - [Hashing vs BST](https://www.geeksforgeeks.org/advantages-of-bst-over-hash-table/)
> - [Hashing vs Trie](https://www.geeksforgeeks.org/advantages-trie-data-structure/)

> Missing content:
> - [Searching Algo](#searching-algo)
> - [Sorting Algo ~ Detail](#sorting-algo-detail)
> - [Two Pointer Technique](#two-pointer-technique)
> - [Window Sliding Technique](#window-sliding-techique)
> - [Prefix Sum Technique](#prefix-sum-technique)