
https://www.scaler.in/double-hashing/

https://www.scaler.com/topics/quadratic-probing/
# Hash Functions

Hash functions are essential for efficient data storage and retrieval in hash tables. They transform input keys into hash values, which are used as indexes in a hash table. This document outlines several types of hash functions and their characteristics.

## Types of Hash Functions

### 1. Division Method

The Division Method is one of the simplest and most common approaches to generating a hash value.

**Formula:**  
h(K) = k mod M  
(where k = key value and M = size of the hash table)

**Advantages:**
- Simple and fast computation.
- Works well for various values of M.

**Disadvantages:**
- Can lead to poor performance if consecutive keys map to consecutive hash values.
- Choosing an appropriate M is critical for performance.

**Example:**  
For k = 1320 and M = 11:  
h(1320) = 1320 mod 11 = 0

---

### 2. Mid-Square Method

This method involves squaring the key and extracting the middle digits as the hash value.

**Formula:**  
h(K) = middle(k × k)  
(where k = key value)

**Advantages:**
- Most digits of the key contribute to the hash value.
- Reduces the impact of the first or last digits.

**Disadvantages:**
- Large keys can lead to excessively large hash values.
- Potential for collisions.

**Example:**  
For a hash table with 200 memory locations and r = 2:  
For k = 50:  
50 × 50 = 2500  
Thus, h(50) = 25 (extracting the middle two digits).

---

### 3. Folding Method

This method involves breaking the key into parts and summing them to generate the hash value.

**Formula:**  
s = k₁ + k₂ + ... + kₙ  
h(K) = s  
(where s = sum of the parts of key k)

**Advantages:**
- Segments the key into manageable pieces for hashing.
- Distribution of keys is independent of their order.

**Disadvantages:**
- May result in inefficiency if many collisions occur.

**Example:**  
For k = 54321:  
Split into k₁ = 54, k₂ = 32, k₃ = 1:  
s = 54 + 32 + 1 = 87  
Thus, h(k) = 87.

---

### 4. Multiplication Method

This method uses a constant to generate the hash value through multiplication.

**Formula:**  
h(K) = floor(M × (kA mod 1))  
(where M = size of the hash table, k = key value, and A = constant value 0 < A < 1)

**Advantages:**
- Versatile and applicable for a range of values.
- Efficient for tables where the size is a power of two.

**Disadvantages:**
- Requires careful selection of the constant A for optimal results.

**Example:**  
For k = 1234, A = 0.35784, M = 100:  
h(1234) = floor[100(1234 × 0.35784 mod 1)]  
Calculating:  
= floor[100(0.57456)] = 57  
Thus, h(1234) = 57.

---

## Choosing a Good Hash Function

Creating an effective hash function is crucial for ensuring that keys are evenly distributed across the hash table. A good hash function should:
- Be quick and easy to compute.
- Effectively resolve collisions.
- Ensure a uniform distribution of hash values.


## Types of Hash Functions
Many hash functions use alphanumeric or numeric keys. The main hash functions cover -  

1.Division Method.  
2.Mid Square Method.  
3.Folding Method.  
4.Multiplication Method.  
Let's examine these methods in more detail. 

1. Division Method

The division method is the simplest and easiest method used to generate a hash value. In this hash function, the value of k is divided by M and uses the remainder as obtained. 

Formula - h(K) = k mod M 

(where k = key value and M = the size of the hash table) 

Advantages	Disadvantages
This method works well for any value of M	This may lead to poor performance as consecutive keys are mapped to consecutive hash values in the hash table.
The division approach is extremely quick because it only calls for one operation.	There are situations when choosing the value of M requires particular caution.
 Example: 
```c
k = 1320 
M = 11 
h (1320) = 1320 mod 11 
= 0
```

2. Mid-Square Method

The steps involved in computing this hash method include the following - 

Squaring the value of k ( like k*k) 
Extract the hash value from the middle r digits. 
Formula - h(K) = h(k x k)

 (where k = key value ) 

Advantages	Disadvantages
Since most or all of the key value's digits contribute to the outcome, this strategy performs well. The middle digits of the squared result are produced by a process in which all of the essential digits participate.	One of this method's constraints is the size of the key; if the key is large, its square will have twice as many digits.
The top or bottom digits of the original key value do not predominate in the outcome.	Chance of repeated collisions.
 Example:

Let's take the hash table with 200 memory locations and r = 2, as decided on the size of the mapping in the table.  
```c
k = 50 
Therefore, 
k = k x k 
= 50 x 50 
= 2500 
Thus, 
h(50) = 50
```
3. Folding Method

There are two steps in this method:  

The key-value k should be divided into a specific number of parts, such as k1, k2, k3,..., kn, each having the very same number of digits aside from the final component, which may have fewer digits than the remaining parts. 
Add each component separately. The last carry, if any, is disregarded to determine the hash value. 

Formula - k = k1, k2, k3, k4, ….., kn 

s = k1+ k2 + k3 + k4 +….+ kn 

h(K)= s

(Where, s = addition of the parts of key k) 

Advantages	Disadvantages
Breaks up the key value into precise equal-sized segments for an easy hash value	Sometimes inefficient if there are too many collisions
Independent of distribution in a hash table	
Example:
```c
k = 54321 
k1 = 54 ; k2 = 32 ; k3 = 1 
Therefore, 
s = k1 + k2 + k3 
= 54 + 32+ 1 
= 87 
Thus, 
h (k) = 87

```
4. Multiplication Method

Steps to follow:

Pick up a constant value A (where 0 < A < 1) 
Multiply A with the key value 
Take the fractional part of kA 
Take the result of the previous step and multiply it by the size of the hash table, M. 
Formula - h(K) = floor (M (kA mod 1)) 

(Where, M = size of the hash table, k = key value and A = constant value) 

Advantages	Disadvantages
It may be applied to any number between 0 and 1, albeit some numbers tend to produce better results than others.	When the table size is a power of two, the multiplication technique is typically appropriate since multiplication hashing makes it possible to compute the index by key quickly.

Example: 
```c
k = 1234 
A = 0.35784 
M = 100 
So,  
h (1234) = floor [ 100(1234 x 0.35784 mod 1)] 
= floor [ 100 ( 441.57456 mod 1)] 
= floor [100 ( 0. 57456)] 
= floor [ 57.456] 
= 57 
Thus, 
h (1234) = 57

```
C. Choosing a Good Hash Function  
Creating an effective hash function that distributes the added item's index value evenly across the database is important. 
Quick and easier to compute according to the requirements. 
An approach to successfully resolve collisions in hash tables is essential for generating an index for a key whose hash index corresponds to an existing spot. 
What is a Hash C

# Hash Functions in Data Structures and Algorithms

Hash functions play a crucial role in efficient data retrieval and storage within hash tables. This document outlines the main types of hash functions, their formulas, advantages, disadvantages, and examples.

| **Hash Function**      | **Formula**                                           | **Advantages**                                             | **Disadvantages**                                       | **Example**                               |
|------------------------|-------------------------------------------------------|-----------------------------------------------------------|--------------------------------------------------------|-------------------------------------------|
| **1. Division Method** | `h(K) = k mod M`                                     | - Works well for various values of M                      | - May lead to clustering                               | `k = 1320, M = 11` <br> `h(1320) = 0`    |
|                        |                                                       | - Extremely quick due to a single operation               | - Care needed when choosing M                          |                                           |
| **2. Mid-Square Method** | `h(K) = middle(k * k)`                             | - Uses all digits of the key value                        | - Key size may lead to excessive digits                | `k = 50` <br> `h(50) = 50`                |
|                        |                                                       | - Better distribution                                      | - Potential for repeated collisions                     |                                           |
| **3. Folding Method**  | `h(K) = s` <br> `s = k1 + k2 + k3 + ... + kn`      | - Segments the key into equal-sized parts                 | - Can be inefficient if too many collisions occur      | `k = 54321` <br> `h(k) = 87`             |
|                        |                                                       | - Independent of distribution in the hash table           |                                                        |                                           |
| **4. Multiplication Method** | `h(K) = floor(M * (k * A mod 1))`              | - Applicable to various numbers between 0 and 1          | - Best when the table size is a power of two          | `k = 1234, A = 0.35784, M = 100` <br> `h(1234) = 57` |

## Choosing a Good Hash Function

Creating an effective hash function is crucial for even distribution of items across the hash table. Key considerations include:
- The function should be quick and easy to compute.
- Effective collision resolution strategies must be in place.
