# Hash Functions in Data Structures and Algorithms

Hash functions play a crucial role in efficient data retrieval and storage within hash tables. This document outlines the main types of hash functions, their formulas, advantages, disadvantages, and examples.

| **Hash Function**      | **Formula**                                           | **Advantages**                                             | **Disadvantages**                                       | **Example**                               |
|------------------------|-------------------------------------------------------|-----------------------------------------------------------|--------------------------------------------------------|-------------------------------------------|
| **1. Division Method** | ( h(K) = k \mod M \)                                | - Works well for various values of \( M \)               | - May lead to clustering                               | \( k = 1320, M = 11 \) <br> \( h(1320) = 0 \) |
|                        |                                                       | - Extremely quick due to a single operation               | - Care needed when choosing \( M \)                   |                                           |
| **2. Mid-Square Method** | \( h(K) = \text{middle}(k \times k) \)            | - Uses all digits of the key value                        | - Key size may lead to excessive digits                | \( k = 50 \) <br> \( h(50) = 50 \)        |
|                        |                                                       | - Better distribution                                      | - Potential for repeated collisions                     |                                           |
| **3. Folding Method**  | \( h(K) = s \) <br> \( s = k_1 + k_2 + k_3 + \ldots + k_n \) | - Segments the key into equal-sized parts                 | - Can be inefficient if too many collisions occur      | \( k = 54321 \) <br> \( h(k) = 87 \)     |
|                        |                                                       | - Independent of distribution in the hash table           |                                                        |                                           |
| **4. Multiplication Method** | \( h(K) = \text{floor}(M \times (k \times A \mod 1)) \) | - Applicable to various numbers between 0 and 1          | - Best when the table size is a power of two          | \( k = 1234, A = 0.35784, M = 100 \) <br> \( h(1234) = 57 \) |

## Choosing a Good Hash Function

Creating an effective hash function is crucial for even distribution of items across the hash table. Key considerations include:
- The function should be quick and easy to compute.
- Effective collision resolution strategies must be in place.
