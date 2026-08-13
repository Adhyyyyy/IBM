# IBM OA — MASTER PATTERN NOTEBOOK
# SET 5 — BIT MANIPULATION + MATHEMATICS

## SOURCE BASIS

The IBM question-bank resource lists these Bit Manipulation problems:

- Swap MSB and LSB (2024)
- Detect endianness (2024)
- Single Number
- Number of 1 bits
- Power of two check
- Reverse bits
- Bitwise AND of numbers range
- XOR operation problems

It lists these Mathematics problems:

- HCF without recursion (2024–2025)
- GCD of array (Unspecified)
- Kth Factor of n (Unspecified)
- Circle relationships (2024)
- Prime number check
- Fibonacci generation
- Factorial calculation
- Power function implementation

The resource also gives these exact interview coding questions:

- Swap MSB and LSB of an integer
- Detect Little-endian or Big-endian
- Check whether a number is a power of two using bit operations
- Check whether a number is prime
- Generate Fibonacci series
- Calculate factorial recursively and iteratively 

The source's high-frequency analysis specifically places **bit manipulation problems such as MSB/LSB swap and endianness at 70% frequency**, while the 2024–2025 OA list explicitly contains HCF without recursion. 

---

# SET 5 — BIG PICTURE

SET 5
│
├── BIT MANIPULATION
│      │
│      ├── Binary representation
│      ├── AND
│      ├── OR
│      ├── XOR
│      ├── NOT
│      ├── Left Shift
│      ├── Right Shift
│      ├── Bit extraction
│      ├── Bit setting
│      ├── Bit clearing
│      └── Bit swapping
│
└── MATHEMATICS
       │
       ├── GCD / HCF
       ├── Divisibility
       ├── Factors
       ├── Prime
       ├── Fibonacci
       ├── Factorial
       ├── Power
       └── Geometry / Circle relationships


---

# WHY BIT MANIPULATION?

A number is ultimately stored in binary.

Example:

5

decimal:
5

binary:
101


Therefore:

BIT MANIPULATION
        ↓
Work directly with
binary representation


Instead of thinking:

"How do I calculate this using normal arithmetic?"

we sometimes ask:

> "What happens to the individual bits?"


---

# BINARY FOUNDATION

Suppose:

N = 13

Binary:

1101


Positions:

bit:
  3  2  1  0

     1  1  0  1

values:

     8  4  2  1


Therefore:

13 = 8 + 4 + 1


---

# BIT POSITIONS

For an integer:

      bit positions

      7 6 5 4 3 2 1 0
      ↓ ↓ ↓ ↓ ↓ ↓ ↓ ↓
      0 1 0 1 1 0 0 1

The:

RIGHTMOST BIT
     ↓
LSB
     ↓
Least Significant Bit


The:

LEFTMOST RELEVANT BIT
     ↓
MSB
     ↓
Most Significant Bit


---

# BITWISE OPERATORS

BITWISE
│
├── &
│      ↓
│    AND
│
├── |
│      ↓
│    OR
│
├── ^
│      ↓
│    XOR
│
├── ~
│      ↓
│    NOT
│
├── <<
│      ↓
│    LEFT SHIFT
│
└── >>
       ↓
    RIGHT SHIFT


---

# 1. BITWISE AND

A & B

Truth table:

A B | A&B
───────
0 0 |  0
0 1 |  0
1 0 |  0
1 1 |  1


AND keeps a bit as 1 only when:

BOTH
bits are 1.


---

# IMPORTANT USE

CHECK WHETHER A BIT IS SET

Suppose:

N = 13

1101


Check bit 2:

mask:

0100


N:

1101

mask:

0100

AND:

0100

result != 0

Therefore:

bit 2 is SET.


GENERAL:

(n & (1 << i)) != 0


---

# 2. BITWISE OR

A | B


A B | A|B
───────
0 0 |  0
0 1 |  1
1 0 |  1
1 1 |  1


OR sets the bit if:

AT LEAST ONE
is 1.


---

# USE

SET A BIT

n = n | (1 << i)


Mental model:

OR
 ↓
Turn bit ON


---

# 3. XOR

A ^ B


A B | A^B
───────
0 0 |  0
0 1 |  1
1 0 |  1
1 1 |  0


XOR is 1 when bits are different.


---

# XOR — THREE GOLDEN RULES

x ^ x = 0

x ^ 0 = x

a ^ b ^ a = b


This is why XOR is extremely useful.

---

# XOR CANCELLATION

Suppose:

[4, 1, 2, 1, 2]

Every duplicate appears twice.

XOR everything:

4 ^ 1 ^ 2 ^ 1 ^ 2

Rearrange:

4 ^ (1 ^ 1) ^ (2 ^ 2)

=

4 ^ 0 ^ 0

=

4


Therefore:

DUPLICATES CANCEL.


This leads directly to:

# SINGLE NUMBER


---

# 51. SINGLE NUMBER

## SOURCE CONNECTION

The IBM resource explicitly lists Single Number under Bit Manipulation. :contentReference[oaicite:2]{index=2}

---

SINGLE NUMBER
│
├── STORY
│      └── Every number appears twice
│          except one
│
├── FIRST THOUGHT
│      │
│      ├── HashMap
│      └── Frequency
│
├── BETTER
│      └── XOR
│
├── WHY?
│
│      x ^ x = 0
│
├── PROCESS
│
│      ans = 0
│
│      for each x:
│
│          ans ^= x
│
└── FINAL
       ans = unique number


## MENTAL MODEL

Every pair disappears.

Example:

2 ^ 3 ^ 2 ^ 4 ^ 3

=

(2 ^ 2)
^
(3 ^ 3)
^
4

=

4


---

# CONNECTION

DUPLICATE PROBLEM
      ↓
FREQUENCY MAP

BUT:

Exactly twice
+
Exactly one unique
      ↓
XOR


This is a classic example where recognizing a mathematical property removes the need for extra memory.


---

# 52. POWER OF TWO

## SOURCE CONNECTION

The resource explicitly lists power-of-two checking, and the exact interview coding question asks to check whether a number is a power of two using bit operations. :contentReference[oaicite:3]{index=3}

---

POWER OF TWO
│
├── EXAMPLES
│      │
│      ├── 1
│      ├── 2
│      ├── 4
│      ├── 8
│      ├── 16
│      └── 32
│
├── BINARY
│
│      1  = 0001
│      2  = 0010
│      4  = 0100
│      8  = 1000
│
├── OBSERVATION
│      │
│      └── Exactly ONE bit is 1
│
├── KEY PROPERTY
│
│      n & (n - 1)
│
├── FOR POWER OF TWO
│
│      n:
│      1000
│
│      n-1:
│      0111
│
│      AND:
│      0000
│
└── CONDITION

n > 0
AND
(n & (n-1)) == 0


---

# WHY DOES n & (n-1) WORK?

Example:

n = 8

1000

n-1:

0111

AND:

0000


Example:

n = 12

1100

n-1:

1011

AND:

1000

NOT zero.


Therefore:

Only powers of two have exactly one set bit.


---

# MEMORY TRIGGER

POWER OF TWO
      ↓
ONE SET BIT
      ↓
n & (n-1)
      ↓
ZERO


---

# 53. NUMBER OF 1 BITS

## SOURCE CONNECTION

Listed under Bit Manipulation. :contentReference[oaicite:4]{index=4}

---

NUMBER OF 1 BITS
│
├── STORY
│      └── Count set bits
│
├── SET BIT
│      └── bit = 1
│
├── BASIC
│      │
│      └── Repeatedly inspect
│          least significant bit
│
├── METHOD 1
│      │
│      ├── if (n & 1)
│      │      count++
│      │
│      └── n >>= 1
│
├── METHOD 2
│      │
│      └── n = n & (n-1)
│
└── IMPORTANT PROPERTY

n & (n-1)

removes the LOWEST SET BIT.


---

# EXAMPLE

n = 12

binary:

1100


n & (n-1):

1100
1011
----
1000


Again:

1000
0111
----
0000


We performed the operation twice.

Therefore:

12 has 2 set bits.


---

# CONNECTION

POWER OF TWO:

n & (n-1) == 0


COUNT SET BITS:

Repeatedly:

n = n & (n-1)


Same operation.

Different goal.


---

# 54. REVERSE BITS

## SOURCE CONNECTION

Listed under Bit Manipulation. :contentReference[oaicite:5]{index=5}

---

REVERSE BITS
│
├── STORY
│      └── Reverse binary representation
│
├── CORE IDEA
│      │
│      └── Extract bits from
│          right side
│
│          and construct
│          answer from left/right
│
├── POINTER-LIKE IDEA
│      │
│      ├── Read current bit
│      └── Shift result
│
├── BASIC PROCESS
│
│      result = 0
│
│      repeat fixed number of bits:
│
│      extract last bit
│      ↓
│      result <<= 1
│      ↓
│      result |= bit
│      ↓
│      n >>= 1
│
└── PATTERN
       EXTRACT
          ↓
       SHIFT
          ↓
       BUILD


---

# VISUAL

Suppose:

n:

1011


Read from right:

1

then:

1

then:

0

then:

1


Build:

1
11
110
1101


So:

1011

becomes:

1101


For a fixed-width integer, the exact number of iterations matters.


---

# CONNECTION

REVERSE STRING
      ↓
Read characters
      ↓
Build reversed string


REVERSE BITS
      ↓
Read bits
      ↓
Build reversed binary


Same high-level pattern:

> Extract from one direction → construct in opposite direction.


---

# 55. SWAP MSB AND LSB

## SOURCE CONNECTION

This is explicitly listed as a 2024 live-coding question. The resource also places MSB/LSB manipulation among high-priority bit topics. :contentReference[oaicite:6]{index=6} :contentReference[oaicite:7]{index=7}

---

SWAP MSB AND LSB
│
├── MSB
│      ↓
│   most significant bit
│
├── LSB
│      ↓
│   least significant bit
│
├── FIRST QUESTION
│      │
│      └── What are the two bits?
│
├── LSB
│      │
│      └── n & 1
│
├── MSB
│      │
│      └── Find highest set-bit position
│
├── THEN
│      │
│      └── Swap their values
│
└── PATTERN
       BIT EXTRACTION
          +
       BIT SET/CLEAR


---

# BASIC BIT OPERATIONS

CHECK BIT:

(n >> i) & 1


SET BIT:

n | (1 << i)


CLEAR BIT:

n & ~(1 << i)


TOGGLE BIT:

n ^ (1 << i)


These four operations are the foundation for many bit problems.


---

# BIT OPERATION MEMORY TREE

BIT i
│
├── CHECK
│      ↓
│   (n >> i) & 1
│
├── SET
│      ↓
│   n | (1 << i)
│
├── CLEAR
│      ↓
│   n & ~(1 << i)
│
└── TOGGLE
       ↓
    n ^ (1 << i)


---

# MSB vs LSB

LSB:

rightmost bit

Example:

101101

      ↑
     LSB


MSB:

leftmost relevant bit

101101
↑
MSB


Important:

For signed integers, the interpretation of the MSB can involve the sign bit.

For this IBM problem, first understand the requested integer representation and bit width.


---

# 56. DETECT ENDIANNESS

## SOURCE CONNECTION

This is explicitly listed as a 2024 live-coding question. :contentReference[oaicite:8]{index=8}

---

ENDIANNESS
│
├── QUESTION
│      └── How are multiple bytes
│          stored in memory?
│
├── BIG-ENDIAN
│      │
│      └── Most Significant Byte
│          stored first
│
├── LITTLE-ENDIAN
│      │
│      └── Least Significant Byte
│          stored first
│
└── KEY
       BYTE ORDER


---

# IMPORTANT DISTINCTION

Endianess is about:

BYTES

not individual bits.


Suppose:

0x12345678


BIG-ENDIAN memory:

12
34
56
78


LITTLE-ENDIAN memory:

78
56
34
12


---

# C/C++ DETECTION IDEA

Store an integer.

Look at the address of its first byte.

If the first byte contains the least significant part:

LITTLE-ENDIAN


If it contains the most significant part:

BIG-ENDIAN


Common conceptual method:

int x = 1;

Look at first byte.


If first byte is:

1

then:

LITTLE-ENDIAN


If first byte is:

0

and later byte contains 1:

BIG-ENDIAN


---

# MENTAL TRIGGER

ENDIANNESS
      ↓
MEMORY
      ↓
BYTE ORDER

Do NOT confuse:

Endianess
with
bit order.


---

# 57. BITWISE AND OF NUMBERS RANGE

## SOURCE CONNECTION

Listed under Bit Manipulation. :contentReference[oaicite:9]{index=9}

---

BITWISE AND RANGE
│
├── STORY
│      └── AND all numbers
│          from left to right
│
├── NAIVE
│      │
│      └── AND every number
│
├── KEY OBSERVATION
│      │
│      └── Bits that change within
│          the range eventually become 0
│
├── CORE IDEA
│      │
│      └── Find common binary prefix
│
├── PROCESS
│      │
│      ├── right shift both numbers
│      ├── until equal
│      └── shift result back
│
└── PATTERN
       COMMON BINARY PREFIX


---

# EXAMPLE

5:

101


7:

111


AND:

101
110
100

Result:

4


The common prefix is:

1


Restore its position:

100


---

# MEMORY TRIGGER

AND over a range
      ↓
Only bits that stay 1
throughout the entire range survive.


---

# 58. XOR OPERATION PROBLEMS

## SOURCE CONNECTION

The resource explicitly includes "XOR operation problems." :contentReference[oaicite:10]{index=10}

---

XOR
│
├── x ^ x = 0
├── x ^ 0 = x
├── order can be rearranged
└── duplicate values cancel


---

# COMMON XOR PATTERNS

XOR
│
├── Single Number
│
├── Find missing number
│
├── Swap without temporary variable
│
└── Problems where pairs cancel


---

# XOR + MISSING NUMBER

Suppose:

Numbers expected:

0,1,2,3,4

Array:

0,1,3,4


XOR all expected values
AND
XOR all array values.


Everything appearing in both cancels.

Only missing number remains.


This connects:

SET 1
Find Missing Number

to:

SET 5
XOR.


---

# XOR SWAP

Classic identity:

a = a ^ b
b = a ^ b
a = a ^ b


This swaps values without a temporary variable under appropriate conditions.


But for normal production code:

a temporary variable is generally clearer.

For IBM preparation:

understand the XOR property,
don't blindly use the trick.


---

# 59. HCF WITHOUT RECURSION

## SOURCE CONNECTION

This is an exact 2024–2025 OA question:

> "Compute the highest common factor (HCF) of two positive integers without using recursion." :contentReference[oaicite:11]{index=11}

---

HCF / GCD
│
├── HCF
│      ↓
│   Highest Common Factor
│
├── SAME CONCEPT
│      ↓
│     GCD
│
├── KEY ALGORITHM
│      └── EUCLIDEAN ALGORITHM
│
├── EQUATION
│
│      gcd(a,b)
│
│      =
│
│      gcd(b, a % b)
│
└── STOP
       when b == 0


---

# EUCLIDEAN ALGORITHM

Example:

gcd(48,18)


48 % 18 = 12

Therefore:

gcd(48,18)
=
gcd(18,12)


18 % 12 = 6

gcd(18,12)
=
gcd(12,6)


12 % 6 = 0

gcd(12,6)
=
6


Answer:

6


---

# ITERATIVE VERSION

while(b != 0)
{
    int rem = a % b;
    a = b;
    b = rem;
}

return a;


This directly satisfies:

WITHOUT RECURSION.


---

# WHY DOES IT WORK?

The common divisors of:

a and b

are the same as the common divisors of:

b and a % b


Therefore:

gcd(a,b)
=
gcd(b,a%b)


The numbers shrink quickly.


---

# COMPLEXITY

O(log(min(a,b)))


This is much better than checking every number up to min(a,b).


---

# MEMORY TRIGGER

GCD / HCF
      ↓
EUCLIDEAN
      ↓
a % b
      ↓
replace
      ↓
until b = 0


---

# 60. GCD OF ARRAY

## SOURCE CONNECTION

The source explicitly lists:

> Given an array of integers, find the GCD of the array. If GCD is 1, return -1. :contentReference[oaicite:12]{index=12}

---

GCD OF ARRAY
│
├── FIRST TWO
│      ↓
│    gcd(a,b)
│
├── THEN
│      ↓
│    gcd(previous, next)
│
├── RECURRING IDEA
│
│      result = gcd(result, arr[i])
│
└── FINAL
       result = GCD of entire array


---

# EXAMPLE

Array:

[12, 18, 24]


Start:

gcd = 12


Then:

gcd(12,18)
=
6


Then:

gcd(6,24)
=
6


Answer:

6


If final gcd == 1:

return -1


according to the source's specified problem statement. :contentReference[oaicite:13]{index=13}


---

# CONNECTION

GCD OF TWO
      ↓
EUCLIDEAN ALGORITHM

GCD OF ARRAY
      ↓
Repeatedly apply
Euclidean algorithm.


This is an important pattern:

> Reduce a many-element problem into repeated two-element operations.


---

# 61. KTH FACTOR OF N

## SOURCE CONNECTION

The source lists "The kth Factor of n" as an unspecified-year OA question. :contentReference[oaicite:14]{index=14}

---

KTH FACTOR
│
├── STORY
│      └── Find kth positive divisor
│          of n
│
├── FACTOR
│      │
│      └── d divides n
│
│          n % d == 0
│
├── NAIVE
│      │
│      └── Check 1 → n
│
├── OPTIMIZATION
│      │
│      └── Factors occur in pairs
│
│          d
│          n/d
│
└── IMPORTANT
       √n


---

# FACTOR PAIRS

For:

n = 36


Factor pairs:

1 × 36

2 × 18

3 × 12

4 × 9

6 × 6


Notice:

Once we pass √36 = 6,

we are seeing the paired factors again.


Therefore:

Check only up to √n.


---

# BUT KTH FACTOR HAS AN ORDER ISSUE

Suppose factors are:

1,2,3,4,6,9,12,18,36


If we only enumerate up to √n,
we don't automatically get the kth factor in ascending order.

Therefore:

Need careful handling of the two factor groups.


This is why:

"Use √n"

does NOT mean:

"return the kth factor immediately."


---

# MENTAL MODEL

FACTORS
│
├── SMALL FACTORS
│      ↓
│    d
│
└── PAIRED LARGE FACTORS
       ↓
     n/d


For kth factor:

1.
Find factor pairs.

2.
Preserve ascending order.

3.
Determine kth.


---

# CONNECTION

PRIME CHECK
      ↓
Check divisors up to √n

KTH FACTOR
      ↓
Find factors up to √n
      +
factor pairs


Same mathematical observation.


---

# 62. PRIME NUMBER CHECK

## SOURCE CONNECTION

The resource lists prime checking, and the exact interview coding list includes "Check if a number is prime." :contentReference[oaicite:15]{index=15}

---

PRIME
│
├── DEFINITION
│      │
│      └── Exactly two positive divisors:
│
│          1
│          n
│
├── EDGE CASES
│      │
│      ├── n < 2 → not prime
│      └── 2 → prime
│
├── NAIVE
│      │
│      └── test 2 → n-1
│
├── OPTIMIZED
│      │
│      └── test up to √n
│
└── WHY?
       If n has a factor greater
       than √n, its paired factor
       must be less than √n.


---

# EXAMPLE

n = 29


√29 ≈ 5.38


Only test:

2
3
4
5


No divisor.

Therefore:

29 is prime.


---

# COMPLEXITY

O(√n)


---

# CONNECTION

PRIME
   ↓
DIVISOR
   ↓
√n


KTH FACTOR
   ↓
DIVISOR
   ↓
√n


This is one mathematical idea appearing in multiple questions.


---

# 63. FIBONACCI

## SOURCE CONNECTION

The resource explicitly lists Fibonacci generation, and the exact interview list includes generating the Fibonacci series. :contentReference[oaicite:16]{index=16}

---

FIBONACCI
│
├── DEFINITION
│      │
│      └── Each number =
│          sum of previous two
│
├── SEQUENCE
│
│      0 1 1 2 3 5 8 13 ...
│
├── EQUATION
│
│      F(n) = F(n-1) + F(n-2)
│
├── ITERATIVE
│      │
│      ├── a = 0
│      ├── b = 1
│      └── repeatedly generate next
│
├── RECURSIVE
│      │
│      └── direct definition
│
└── IMPORTANT
       Simple recursion repeats work.


---

# ITERATIVE MENTAL MODEL

a     b
↓     ↓

0     1


next:

a + b

then shift:

a = b
b = next


Sequence:

0 1
1 1
1 2
2 3
3 5
5 8


---

# CONNECTION TO DP

Fibonacci is the simplest example of:

OVERLAPPING SUBPROBLEMS


Naive recursion:

F(n)
├── F(n-1)
│   ├── ...
│   └── ...
└── F(n-2)
    ├── ...
    └── ...


Same subproblems are recalculated.


Therefore:

FIBONACCI
      ↓
DP foundation


This connection becomes important in Set 7.


---

# 64. FACTORIAL

## SOURCE CONNECTION

The resource explicitly lists factorial calculation, and the exact interview list asks for factorial recursively and iteratively. :contentReference[oaicite:17]{index=17}

---

FACTORIAL
│
├── DEFINITION
│
│      n! =
│      n × (n-1) × ... × 1
│
├── BASE CASE
│      │
│      └── 0! = 1
│
├── RECURSIVE
│      │
│      └── n! = n × (n-1)!
│
└── ITERATIVE
       │
       └── repeated multiplication


---

# RECURSION

factorial(5)

=

5 × factorial(4)

=

5 × 4 × factorial(3)

=

5 × 4 × 3 × factorial(2)

=

5 × 4 × 3 × 2 × factorial(1)

=

120


---

# ITERATIVE

result = 1

for i = 2 → n:

result *= i


---

# CONNECTION

FACTORIAL
   ↓
RECURSION
   ↓
BASE CASE
   +
REDUCE INPUT


This same recursion structure appears later in:

- Trees
- DFS
- Backtracking
- DP


---

# 65. POWER FUNCTION

## SOURCE CONNECTION

The source lists power function implementation. :contentReference[oaicite:18]{index=18}

---

POWER
│
├── BASIC
│      │
│      └── x^n
│
├── NAIVE
│      │
│      └── multiply x
│          n times
│
├── COMPLEXITY
│      O(n)
│
├── OPTIMIZED
│      └── EXPONENTIATION BY SQUARING
│
├── IDEA
│
│      x^n
│
│      if n even:
│
│      x^n
│      =
│      (x^(n/2))²
│
│      if n odd:
│
│      x^n
│      =
│      x × x^(n-1)
│
└── COMPLEXITY
       O(log n)


---

# EXAMPLE

2^8


Instead of:

2 × 2 × 2 × 2 × 2 × 2 × 2 × 2


Think:

2^8
=
(2^4)^2

2^4
=
(2^2)^2

2^2
=
(2^1)^2


The exponent keeps getting halved.


---

# CONNECTION

BINARY
   ↓
HALVING
   ↓
EXPONENTIATION BY SQUARING


This is conceptually related to:

BINARY SEARCH

because both exploit:

> repeatedly reduce the search/work by half.


---

# 66. CIRCLE RELATIONSHIPS

## SOURCE CONNECTION

The exact 2024 OA list includes:

> Given multiple circles specified by (x,y,r), determine the relationship between two circles: concentric, touching, intersecting or disjoint. :contentReference[oaicite:19]{index=19}

---

CIRCLE RELATIONSHIP
│
├── INPUT
│      │
│      ├── center 1: (x1,y1)
│      ├── radius 1: r1
│      ├── center 2: (x2,y2)
│      └── radius 2: r2
│
├── FIRST QUESTION
│      │
│      └── Distance between centers?
│
├── DISTANCE
│
│      d² =
│      (x1-x2)²
│      +
│      (y1-y2)²
│
├── COMPARE WITH
│      │
│      ├── r1 + r2
│      └── |r1-r2|
│
└── CLASSIFY


---

# IMPORTANT CASES

CONCENTRIC
│
└── centers are identical


TOUCHING
│
├── external:
│      d = r1 + r2
│
└── internal:
       d = |r1-r2|


INTERSECTING
│
└── circles have two intersection points


DISJOINT
│
└── no intersection


---

# AVOID UNNECESSARY SQRT

Instead of:

d = sqrt(dx² + dy²)

you can compare:

d²

with:

(r1+r2)²

and:

(r1-r2)²


This avoids floating-point square roots.


---

# MENTAL MODEL

TWO CIRCLES
    ↓
CENTER DISTANCE
    ↓
COMPARE WITH
RADIUS SUM / DIFFERENCE
    ↓
CLASSIFY


---

# SET 5 — MASTER BIT PATTERN MAP

BIT MANIPULATION
│
├── CHECK BIT
│      ↓
│   (n >> i) & 1
│
├── SET BIT
│      ↓
│   n | (1 << i)
│
├── CLEAR BIT
│      ↓
│   n & ~(1 << i)
│
├── TOGGLE BIT
│      ↓
│   n ^ (1 << i)
│
├── XOR
│      │
│      ├── duplicate cancellation
│      ├── Single Number
│      └── Missing Number
│
├── n & (n-1)
│      │
│      ├── remove lowest set bit
│      ├── count set bits
│      └── power of two
│
├── SHIFT
│      │
│      ├── << 
│      └── >>
│
├── MSB / LSB
│      ↓
│   bit extraction / manipulation
│
└── ENDIANNESS
       ↓
    byte order in memory


---

# SET 5 — MASTER MATHEMATICS MAP

MATHEMATICS
│
├── GCD / HCF
│      ↓
│   EUCLIDEAN ALGORITHM
│
├── GCD ARRAY
│      ↓
│   repeated GCD
│
├── PRIME
│      ↓
│   divisors up to √n
│
├── KTH FACTOR
│      ↓
│   factor pairs
│      ↓
│   √n
│
├── FIBONACCI
│      ↓
│   recurrence
│
├── FACTORIAL
│      ↓
│   recurrence / iteration
│
├── POWER
│      ↓
│   exponentiation by squaring
│
└── CIRCLE
       ↓
    distance geometry


---

# SET 5 — MOST IMPORTANT CONNECTIONS

## CONNECTION 1 — XOR

SET 1:

Missing Number
       ↓
Can use XOR

SET 5:

Single Number
       ↓
XOR

Therefore:

XOR
 ↓
CANCEL PAIRS


---

# CONNECTION 2 — n & (n-1)

POWER OF TWO

n & (n-1) == 0


COUNT SET BITS

repeat:

n = n & (n-1)


Same identity.

Different problem.


---

# CONNECTION 3 — √n

PRIME
 ↓
Check divisors to √n


KTH FACTOR
 ↓
Find factor pairs to √n


Same mathematical observation.


---

# CONNECTION 4 — GCD

HCF of two
      ↓
Euclidean algorithm


GCD of array
      ↓
Repeated Euclidean algorithm


---

# CONNECTION 5 — RECURSION

Fibonacci
     ↓
recurrence


Factorial
     ↓
recurrence


Power
     ↓
recurrence / divide and conquer


These become foundations for:

DP
Trees
Backtracking
Divide and Conquer


---

# SET 5 — STORY DECODING CHEAT SHEET

STORY
│
├── "Every number appears twice except one"
│      ↓
│    XOR
│
├── "Power of two"
│      ↓
│    one set bit
│      ↓
│    n & (n-1)
│
├── "Count set bits"
│      ↓
│    n & (n-1)
│
├── "Reverse bits"
│      ↓
│    extract + shift + build
│
├── "MSB / LSB"
│      ↓
│    bit positions
│
├── "Endian"
│      ↓
│    BYTE ORDER
│
├── "GCD / HCF"
│      ↓
│    Euclidean algorithm
│
├── "GCD of array"
│      ↓
│    repeated GCD
│
├── "Prime"
│      ↓
│    divisors up to √n
│
├── "Kth factor"
│      ↓
│    factor pairs
│
├── "Fibonacci"
│      ↓
│    previous two values
│
├── "Factorial"
│      ↓
│    repeated multiplication
│
├── "Power"
│      ↓
│    exponentiation by squaring
│
└── "Circle relationship"
       ↓
    center distance
       ↓
    compare radii


---

# SET 5 — PRIORITY

## TIER 1 — DIRECT OA / INTERVIEW EVIDENCE

├── [ ] 51. Swap MSB and LSB
├── [ ] 52. Detect Endianness
├── [ ] 53. Power of Two Using Bits
├── [ ] 54. HCF Without Recursion
├── [ ] 55. Circle Relationships
├── [ ] 56. Prime Check
├── [ ] 57. Fibonacci
└── [ ] 58. Factorial


The source explicitly reports these among exact OA/interview questions. 


---

## TIER 2 — HIGH-VALUE PATTERN PROBLEMS

├── [ ] 59. Single Number
├── [ ] 60. Number of 1 Bits
├── [ ] 61. Reverse Bits
├── [ ] 62. XOR Problems
├── [ ] 63. GCD of Array
├── [ ] 64. Kth Factor of n
└── [ ] 65. Power Function


---

## TIER 3 — EXTENSION

└── [ ] 66. Bitwise AND of Numbers Range


These are explicitly present in the broader question bank but are not all separately reported as exact OA questions in the source. :contentReference[oaicite:21]{index=21}


---

# SET 5 — CHECKLIST

SET 5 — BIT + MATH
│
├── BIT FUNDAMENTALS
│      ├── [ ] Binary representation
│      ├── [ ] AND
│      ├── [ ] OR
│      ├── [ ] XOR
│      ├── [ ] NOT
│      ├── [ ] Left shift
│      └── [ ] Right shift
│
├── BIT PROBLEMS
│      ├── [ ] 51. Swap MSB / LSB
│      ├── [ ] 52. Detect Endianness
│      ├── [ ] 53. Power of Two
│      ├── [ ] 59. Single Number
│      ├── [ ] 60. Number of 1 Bits
│      ├── [ ] 61. Reverse Bits
│      ├── [ ] 62. XOR Problems
│      └── [ ] 66. Bitwise AND Range
│
└── MATHEMATICS
       ├── [ ] 54. HCF Without Recursion
       ├── [ ] 63. GCD of Array
       ├── [ ] 64. Kth Factor
       ├── [ ] 55. Circle Relationships
       ├── [ ] 56. Prime Check
       ├── [ ] 57. Fibonacci
       ├── [ ] 58. Factorial
       └── [ ] 65. Power Function


---

# SET 5 — COMPLEXITY CHEAT SHEET

SINGLE NUMBER
    ↓
O(n)


POWER OF TWO
    ↓
O(1)


COUNT SET BITS
    ↓
O(number of set bits)
or O(log n) for basic shifting


PRIME CHECK
    ↓
O(√n)


GCD
    ↓
O(log min(a,b))


GCD ARRAY
    ↓
O(n log V)
approximately,
where V is value magnitude


FIBONACCI ITERATIVE
    ↓
O(n)


FACTORIAL ITERATIVE
    ↓
O(n)


POWER — NAIVE
    ↓
O(n)


POWER — FAST
    ↓
O(log n)


CIRCLE RELATIONSHIP
    ↓
O(1)


---

# SET 5 — IMPORTANT EDGE CASES

## BIT

├── [ ] n = 0
├── [ ] n = 1
├── [ ] negative integers
├── [ ] integer width
└── [ ] signed vs unsigned behavior


## PRIME

├── [ ] n < 2
├── [ ] n = 2
└── [ ] even numbers


## GCD

├── [ ] a = 0
├── [ ] b = 0
└── [ ] both zero if input permits


## FACTOR

├── [ ] n = 1
├── [ ] perfect square
└── [ ] kth factor doesn't exist


## FIBONACCI

├── [ ] n = 0
├── [ ] n = 1
└── [ ] integer overflow


## FACTORIAL

├── [ ] 0! = 1
├── [ ] 1! = 1
└── [ ] overflow for large n


## POWER

├── [ ] exponent = 0
├── [ ] exponent = 1
├── [ ] negative exponent if supported
└── [ ] overflow / floating-point behavior


---

# SET 5 — CORE BIT OPERATIONS TO MEMORIZE

```cpp
// Check bit i
(n >> i) & 1

// Set bit i
n | (1 << i)

// Clear bit i
n & ~(1 << i)

// Toggle bit i
n ^ (1 << i)

// Remove lowest set bit
n & (n - 1)

// Check power of two
n > 0 && (n & (n - 1)) == 0



SET 5 — CORE MATH TEMPLATES TO MEMORIZE
GCD
while (b != 0) {
    int rem = a % b;
    a = b;
    b = rem;
}
return a;
PRIME
if (n < 2)
    return false;

for (int i = 2; i * i <= n; i++) {
    if (n % i == 0)
        return false;
}

return true;
FIBONACCI
int a = 0, b = 1;

for (int i = 0; i < n; i++) {
    cout << a << " ";

    int next = a + b;
    a = b;
    b = next;
}
FACTORIAL
long long ans = 1;

for (int i = 2; i <= n; i++) {
    ans *= i;
}

return ans;
SET 5 — FINAL RECOGNITION RULES
Exactly one unique among pairs → XOR.
Power of two → exactly one set bit.
Exactly one set bit → n & (n-1) == 0.
Remove lowest set bit → n & (n-1).
Check bit i → (n >> i) & 1.
Set bit i → n | (1 << i).
Clear bit i → n & ~(1 << i).
Toggle bit i → n ^ (1 << i).
MSB/LSB → think bit positions.
Endianness → think byte order in memory.
HCF/GCD → Euclidean algorithm.
GCD of array → repeatedly apply GCD.
Prime → test divisors only up to √n.
Factors → factor pairs.
Kth factor → don't forget ordering after using √n optimization.
Fibonacci → previous two values.
Factorial → repeated multiplication / recursion.
Fast power → exponentiation by squaring.
Circle relationship → center distance + radius sum/difference.
When a problem says "without recursion", use an iterative formulation.
SET 5 — COMPLETE MENTAL STORY

IBM STORY
│
├── "Unique number"
│ ↓
│ XOR
│
├── "Power of two"
│ ↓
│ ONE SET BIT
│
├── "Number of 1s"
│ ↓
│ SET-BIT COUNT
│
├── "MSB / LSB"
│ ↓
│ BIT POSITION
│
├── "Endian"
│ ↓
│ BYTE ORDER
│
├── "HCF"
│ ↓
│ EUCLIDEAN ALGORITHM
│
├── "GCD array"
│ ↓
│ REPEATED GCD
│
├── "Prime"
│ ↓
│ √n DIVISOR CHECK
│
├── "Kth factor"
│ ↓
│ FACTOR PAIRS
│
├── "Fibonacci"
│ ↓
│ TWO PREVIOUS VALUES
│
├── "Factorial"
│ ↓
│ PRODUCT / RECURSION
│
├── "Power"
│ ↓
│ EXPONENTIATION BY SQUARING
│
└── "Circle relationship"
↓
DISTANCE GEOMETRY

SET 5 — CONNECTION TO PREVIOUS SETS

SET 1
│
└── Missing Number
↓
XOR
↓
SET 5
│
└── Single Number

SET 1
│
└── Prime Check
↓
√n
↓
SET 5
│
├── Prime
└── Kth Factor

SET 2
│
└── Frequency
↓
SET 4
│
└── Frequency + Heap

SET 3
│
└── Recursion
↓
SET 5
│
├── Fibonacci
├── Factorial
└── Power

SET 5 — FINAL VISUAL MAP

BIT
│
├── REPRESENTATION
│ ↓
│ binary
│
├── OPERATIONS
│ ├── AND
│ ├── OR
│ ├── XOR
│ ├── NOT
│ ├── SHIFT
│ └── MASK
│
├── IDENTITIES
│ ├── x ^ x = 0
│ ├── x ^ 0 = x
│ └── n & (n-1)
│
└── APPLICATIONS
├── Single Number
├── Power of Two
├── Count Bits
├── Reverse Bits
├── MSB/LSB
└── Range AND

MATH
│
├── DIVISORS
│ ├── Prime
│ └── Factors
│
├── GCD
│ ├── HCF
│ └── GCD Array
│
├── RECURRENCE
│ ├── Fibonacci
│ └── Factorial
│
├── EXPONENT
│ └── Fast Power
│
└── GEOMETRY
└── Circle Relations

SET 5 — COMPLETION TARGET

Before moving to Set 6, you should be able to see:

"Only one appears once"
        ↓
XOR


"Power of 2?"
        ↓
n & (n-1)


"Count set bits"
        ↓
repeated n & (n-1)


"Swap MSB and LSB"
        ↓
extract bit positions
        ↓
set/clear bits


"Little or Big endian?"
        ↓
byte order in memory


"HCF"
        ↓
Euclidean algorithm


"GCD of array"
        ↓
repeated GCD


"Prime?"
        ↓
√n divisor check


"Kth factor?"
        ↓
factor pairs


"Fibonacci?"
        ↓
previous two


"Factorial?"
        ↓
product / recursion


"Fast power?"
        ↓
halve exponent


"Circle relationship?"
        ↓
distance between centers
+
radius comparison
