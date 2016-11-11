
# Algorithms
Notes and homework for Coursera's "Algorithms" online class :books:

## Divide and Conquer, Sorting and Searching, and Randomized Algorithms

### Introduction

#### Why study algorithms?

foobar

#### Integer multiplication

input: 2 n-digit numbers x and y
output: the product x.y

Primitive operation (for now): add or multiply 2 single-digit numbers.

Algo is "correct": the algo will eventually terminate and give the correct answer.

What about the amount of time needed?

upshot: nOperations <= some constant
upshot: can we do better?

#### Karatsuba multiplication

**Example:**
x = 5678, a = 56, b = 78
y = 1234, c = 12, d = 34

step1: a.c = 672
step2: d.b = 2652
step3: (a+b)(c+d) = 6164
step4: (3) - (2) - (1) = 2840
step5: (1) * 10^4 + (2) + (4) * 10^2 = 7006652, the output

**Recursive algorithm:**
write x = 10^(n/2) * a + b, y = 10^(n/2) * c + d where a, b, c, d are n/2-digit numbers.

x.y = ...
    = 10^n * ac + 10^(n/2) * (ad + bc) + bd (¤)

idea: recursively compute ac, ad, bc, bd then compute ¤

step1: recursively compute ac
step2: recursively compute bd
step3: recursively compute (a + b)(c + d) = ac + ad + bc + bd
Gauss's trick: (3) - (1) - (2) = ad + bc

upshot: only need 3 recursive multiplications and some additions

#### About the course

spoilers

#### Merge Sort: Motivation and Example

Improves over Selection, Insertion, Bubble sorts
Good example for worst case behavior and asymptotic analysis

Recursion tree methods --> "Master method"

input: array of n numbers
output: array of n numbers, sorted from min to max

Assumption: numbers are distincts (does not change much)

#### Merge Sort: Pseudocode / Merge Sort: Analysis

ignore base cases

```
C = output[length = n]
A = first sorted array [n/2]
B = second sorted array [n/2]
i = 1
j = 1

for k = 1 to n
  if A(i) < B(j)
    C(k) =  A(i)
    i++
  else
    C(k) = B(j)
    j++
end
```

Running time ? n numbers to sort

Upshot: <= 4n + 2
        <= 6n (since n >= 1)

Claim: merge sort requires <= 6n * (log(n) + 1) operations to sort n

At each level j=0,1,...,log(n) there are 2^j subproblems each of size n/(2^j)

#### Guiding Principles for Analysis of Algorithms

- worst case analysis
- don't pay attention to constant factors and lower order terms
- asymptotic analysis (focus on large input sizes)

Fast algorithm ~= worst-case running time grows slowly with input size

Holy grail: linear runnning time

### Asymptotic analysis

#### The gist

Importance: vocabulary, "sweet spot", sharp enough to differentiate algo

High-level idea: suppress constant factors and lower-order terms.

constant factors: too system-dependant
lower-order terms: irrelevant for large input

--> 6n(log(n) + 1) ==> nlog(n)

**examples:**

- One loop: does an array contains a given integer  --> O(n)
- Two loops: does A or B contain t? --> O(n)
- Two nested loops: do A and B have a number in common --> O(n²)
- Two nested loops (II): does A have duplicate entries --> O(n²)

#### Big-Oh Notation

T(n) = function on N

`T(n) = O(f(n)) <--> E c, n0 > 0 / T(n) <= c * f(n) A n >= n0`

#### Basic Examples

##### Example 1

Claim:  if T(n) = a_k * n^k + ... + a_0 * n^0
        then T(n) = O(n^k)

Proof: choose n0 = 1 and c = |a_k|+...+|a_0|

##### Examples 2

Claim: A k >= 1, n^k != O(n^(k-1))

Proof: by contradiction. Suppose n^k = O(n^(k-1))
`E c, n0 > 0 / n^k <= c * n^(k -1), A n >= 0`
ie `n <= c, A n >= 0`

#### Big Omega and Theta

Omega notation:
`T(n) = Om(f(n)) <--> E c, n0 / T(n) >= c * f(n) A n >= n0`

Theta notation: O(f(n)) AND Om(f(n))
`T(n) = th(f(n)) <--> E c1, c2, n0 / c1 * f(n) <= T(n) <= c2 * f(n) A n >= n0`

Little Oh notation:
`T(n) = o(f(n)) <--> A c > 0, E n0 / T(n) <= c * f(n) A n >= n0`
