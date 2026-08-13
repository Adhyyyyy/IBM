# IBM OA — MASTER PATTERN NOTEBOOK
# SET 7 — DYNAMIC PROGRAMMING

# SOURCE BASIS

The IBM PYQ Question Bank lists these Dynamic Programming problems:

- Climbing Stairs
- House Robber
- Longest Increasing Subsequence
- Coin Change
- 0/1 Knapsack variations
- Edit Distance
- Longest Common Subsequence
- Maximum Product Subarray
- Decode Ways
- Word Break :contentReference[oaicite:2]{index=2}


The DSA resource defines the core DP concepts as:

- Memoization
- Tabulation
- Identify subproblems

and the major patterns as:

- 1D DP
- 2D DP
- Knapsack
- Subsequence :contentReference[oaicite:3]{index=3}


# SET 7 — BIG PICTURE

DYNAMIC PROGRAMMING
│
├── WHY?
│      │
│      ├── Repeated subproblems
│      ├── Overlapping subproblems
│      └── Avoid repeated work
│
├── FIRST STEP
│      │
│      └── Define STATE
│
├── SECOND STEP
│      │
│      └── Find TRANSITION
│
├── THIRD STEP
│      │
│      └── Define BASE CASE
│
├── FOURTH STEP
│      │
│      └── Compute states
│
├── TOP-DOWN
│      │
│      └── Memoization
│
└── BOTTOM-UP
       │
       └── Tabulation


# THE MOST IMPORTANT DP IDEA

DP is NOT:

"Use an array called dp."


DP is:

PROBLEM
   ↓
BREAK INTO SUBPROBLEMS
   ↓
SAME SUBPROBLEMS REPEAT
   ↓
STORE THEIR ANSWERS
   ↓
REUSE THEM


# DP STORY

WITHOUT DP:

Solve same subproblem
again
again
again
again


WITH DP:

Solve once
   ↓
STORE
   ↓
REUSE


# 83. WHAT IS A DP STATE?

The most important question:

> "What does dp[i] mean?"


Example:

Climbing Stairs


dp[i]

means:

number of ways
to reach stair i.


Therefore:

STATE
=
meaning of dp[i]


# GOLDEN RULE

Before writing code:

WRITE:

dp[i] = __________________


If you cannot fill that blank clearly:

you don't yet understand the DP state.


# 84. MEMOIZATION

MEMOIZATION
│
├── TOP-DOWN
│
├── Start from
│   original problem
│
├── Recursion
│
├── Before solving
│   check dp
│
├── If already solved
│      ↓
│    return stored answer
│
└── Otherwise
       solve
       +
       store


# EXAMPLE

Fibonacci:

F(n)
│
├── F(n-1)
└── F(n-2)


Without memoization:

F(n-2)
may be calculated
multiple times.


With memoization:

dp[n-2]

stores the result.


# TEMPLATE

int solve(int n)
{
    if(base case)
        return answer;

    if(dp[n] != -1)
        return dp[n];

    return dp[n] =
        solve(smaller problem);
}


# MENTAL TRIGGER

RECURSION
+
REPEATED SUBPROBLEMS
        ↓
MEMOIZATION


# 85. TABULATION

TABULATION
│
├── BOTTOM-UP
│
├── Start from
│   base cases
│
├── Fill dp table
│
└── Reach final answer


Example:

Fibonacci:

dp[0] = 0
dp[1] = 1

for i = 2 → n:

    dp[i] =
        dp[i-1] + dp[i-2]


# MEMOIZATION vs TABULATION

MEMOIZATION
│
├── Top-down
├── Recursion
├── Store answers
└── Solve only reached states


TABULATION
│
├── Bottom-up
├── Usually iterative
├── Fill table
└── Build toward final state


# MEMORY TRICK

MEMOIZATION

QUESTION:
"Have I already solved this?"


TABULATION

QUESTION:
"What smaller states do I need
before calculating this one?"


# 86. CLIMBING STAIRS

## SOURCE CONNECTION

Climbing Stairs is explicitly listed in the IBM DP question bank. :contentReference[oaicite:4]{index=4}

---

CLIMBING STAIRS
│
├── STORY
│      └── Reach stair n
│
├── ALLOWED
│      ├── 1 step
│      └── 2 steps
│
├── QUESTION
│      └── Number of ways?
│
├── STATE
│
│      dp[i]
│      =
│      ways to reach stair i
│
├── TRANSITION
│
│      dp[i]
│      =
│      dp[i-1]
│      +
│      dp[i-2]
│
└── BASE


dp[0] = 1
dp[1] = 1


# WHY?

To reach stair i:

You either came from:

i-1

or:

i-2


Therefore:

ways(i)
=
ways(i-1)
+
ways(i-2)


# VISUAL

i
↑

Either:

i-1 → i

or:

i-2 → i


# CONNECTION

CLIMBING STAIRS
      ↓
FIBONACCI-LIKE RECURRENCE
      ↓
1D DP


# IMPORTANT

Do not memorize:

"Climbing Stairs = Fibonacci."


Understand:

> The final move determines which previous states can reach the current state.


This idea generalizes to many DP problems.


# 87. HOUSE ROBBER

## SOURCE CONNECTION

House Robber is explicitly listed in the IBM DP question bank. :contentReference[oaicite:5]{index=5}

---

HOUSE ROBBER
│
├── STORY
│      └── Cannot rob adjacent houses
│
├── CHOICE
│      │
│      ├── ROB current
│      └── SKIP current
│
├── STATE
│
│      dp[i]
│      =
│      maximum money
│      from first i houses
│
├── TRANSITION
│
│      SKIP:
│      dp[i-1]
│
│      ROB:
│      nums[i] + dp[i-2]
│
└── ANSWER

max(
    dp[i-1],
    nums[i] + dp[i-2]
)


# VISUAL

houses:

[2] [7] [9] [3] [1]


At house 9:

Option 1:

skip 9
 ↓
previous answer


Option 2:

rob 9
 ↓
cannot rob 7
 ↓
9 + answer before 7


Therefore:

MAX(skip, take)


# CORE PATTERN

CURRENT ITEM
│
├── TAKE
│      ↓
│    previous compatible state
│
└── SKIP
       ↓
     previous state


# MENTAL TRIGGER

"Choose or skip"
+
"Adjacent cannot both be chosen"


        ↓

TAKE / SKIP DP


# CONNECTION

HOUSE ROBBER
      ↓
TAKE / SKIP


0/1 KNAPSACK
      ↓
TAKE / SKIP


SUBSEQUENCE DP
      ↓
TAKE / SKIP


This is one of the most important connections in Set 7.


# 88. HOUSE ROBBER II

The separate DSA resource includes House Robber II, although the IBM PYQ list retrieved here specifically names House Robber rather than separately naming House Robber II. 

HOUSE ROBBER II
│
└── HOUSES ARE CIRCULAR


Problem:

First and last houses
are adjacent.


Therefore:

Cannot simply run
House Robber on
the entire array.


# KEY TRANSFORMATION

Circular
   ↓
Break into two linear cases


CASE 1:

exclude first


CASE 2:

exclude last


Answer:

max(
    rob(1...n-1),
    rob(0...n-2)
)


# CONNECTION

HOUSE ROBBER
 ↓
LINEAR


HOUSE ROBBER II
 ↓
CIRCULAR
 ↓
TWO LINEAR DP PROBLEMS


# 89. COIN CHANGE

## SOURCE CONNECTION

Coin Change is explicitly listed in the IBM DP question bank. :contentReference[oaicite:7]{index=7}

---

COIN CHANGE
│
├── STORY
│      └── Given coin denominations
│
├── TARGET
│      └── amount
│
├── QUESTION
│      └── Minimum number of coins?
│
├── STATE
│
│      dp[x]
│      =
│      minimum coins
│      needed for amount x
│
├── TRANSITION
│
│      choose coin
│
│      dp[x]
│      =
│      min(
│          dp[x-coin] + 1
│      )
│
└── BASE

dp[0] = 0


# EXAMPLE

coins:

[1,2,5]

amount:

5


Possible:

5

or:

2 + 2 + 1

or:

1+1+1+1+1


Best:

1 coin


Therefore:

dp[5] = 1


# MENTAL MODEL

TARGET
│
├── choose coin
│
├── reduce target
│
└── reuse smaller answer


# TRANSITION

Current amount:

x


If choose coin:

c


Remaining:

x-c


Therefore:

dp[x]
=
dp[x-c] + 1


Take minimum over all valid coins.


# CONNECTION

COIN CHANGE
 ↓
1D DP
 ↓
STATE = AMOUNT


This is different from:

0/1 Knapsack

because coins can generally be reused.


# IMPORTANT DISTINCTION

0/1 KNAPSACK

Each item:
TAKE ONCE


COIN CHANGE

Coin:
can usually be used
multiple times


That difference changes the transition/iteration strategy.


# 90. 0/1 KNAPSACK

## SOURCE CONNECTION

0/1 Knapsack variations are explicitly listed in the IBM DP question bank. :contentReference[oaicite:8]{index=8}

---

0/1 KNAPSACK
│
├── INPUT
│      ├── weights
│      ├── values
│      └── capacity
│
├── EACH ITEM
│      │
│      ├── TAKE
│      └── SKIP
│
├── IMPORTANT
│      │
│      └── Each item can be
│          used AT MOST ONCE
│
├── STATE
│      │
│      └── dp[i][capacity]
│
└── TRANSITION


SKIP:

dp[i-1][capacity]


TAKE:

value[i]
+
dp[i-1][capacity-weight[i]]


# FORMULA

dp[i][w]
=
max(
    dp[i-1][w],

    value[i]
    +
    dp[i-1][w-weight[i]]
)


# WHY i-1 AFTER TAKE?

Because:

0/1

means:

current item cannot be reused.


Therefore:

take item i
 ↓
move to previous items.


# MENTAL TRIGGER

"Each item can be chosen once"

        ↓

0/1 KNAPSACK


# CONNECTION

HOUSE ROBBER
 ↓
TAKE / SKIP


KNAPSACK
 ↓
TAKE / SKIP


The difference:

House Robber:
adjacency constraint


Knapsack:
capacity constraint


# 91. LONGEST COMMON SUBSEQUENCE

## SOURCE CONNECTION

LCS is explicitly listed in the IBM DP question bank. :contentReference[oaicite:9]{index=9}

---

LCS
│
├── INPUT
│      ├── string A
│      └── string B
│
├── SUBSEQUENCE
│      │
│      └── order maintained
│          but characters
│          need not be adjacent
│
├── STATE
│
│      dp[i][j]
│      =
│      LCS of first i chars
│      of A and first j chars
│      of B
│
├── IF MATCH
│      │
│      A[i-1] == B[j-1]
│      │
│      └── 1 + dp[i-1][j-1]
│
└── IF NOT MATCH
       │
       └── max(
              dp[i-1][j],
              dp[i][j-1]
           )


# EXAMPLE

A:

abcde


B:

ace


LCS:

ace


Length:

3


# MATCH

If:

A[i-1] == B[j-1]


Then:

take character.


dp[i][j]
=
1 + dp[i-1][j-1]


# MISMATCH

If characters differ:

We have two possibilities:

skip A character

OR

skip B character


Therefore:

max(
    dp[i-1][j],
    dp[i][j-1]
)


# MENTAL MODEL

TWO STRINGS
│
├── characters match
│      ↓
│    TAKE BOTH
│
└── characters differ
       ↓
     SKIP ONE SIDE
       ↓
     TAKE MAX


# CONNECTION

LCS
 ↓
2D DP
 ↓
TWO POINTER POSITIONS


# 92. EDIT DISTANCE

## SOURCE CONNECTION

Edit Distance is explicitly listed in the IBM DP question bank. :contentReference[oaicite:10]{index=10}

---

EDIT DISTANCE
│
├── INPUT
│      ├── word1
│      └── word2
│
├── OPERATIONS
│      ├── INSERT
│      ├── DELETE
│      └── REPLACE
│
├── STATE
│
│      dp[i][j]
│      =
│      minimum operations
│      to convert
│      first i chars
│      into first j chars
│
├── MATCH
│      │
│      └── dp[i][j]
│          =
│          dp[i-1][j-1]
│
└── MISMATCH
       │
       └── 1 + min(
              insert,
              delete,
              replace
           )


# TRANSITIONS

INSERT:

dp[i][j-1]


DELETE:

dp[i-1][j]


REPLACE:

dp[i-1][j-1]


Therefore:

dp[i][j]
=
1 + min(
    dp[i][j-1],
    dp[i-1][j],
    dp[i-1][j-1]
)


# MENTAL MODEL

TWO STRINGS
│
├── SAME CHARACTER
│      ↓
│    NO OPERATION
│
└── DIFFERENT
       ↓
     THREE CHOICES
       │
       ├── insert
       ├── delete
       └── replace


# CONNECTION

LCS
 ↓
TWO STRINGS
 ↓
2D DP


EDIT DISTANCE
 ↓
TWO STRINGS
 ↓
2D DP


Both use:

dp[i][j]


But the transition meaning is different.


# 93. LONGEST INCREASING SUBSEQUENCE

## SOURCE CONNECTION

LIS is explicitly listed in the IBM DP question bank. :contentReference[oaicite:11]{index=11}

---

LIS
│
├── STORY
│      └── Find longest
│          strictly increasing
│          subsequence
│
├── SUBSEQUENCE
│      └── elements need not
│          be adjacent
│
├── STATE
│
│      dp[i]
│      =
│      LIS ending at i
│
├── TRANSITION
│
│      for j < i:
│
│      if nums[j] < nums[i]
│
│      dp[i]
│      =
│      max(
│          dp[i],
│          dp[j] + 1
│      )
│
└── ANSWER

max(dp[i])


# EXAMPLE

[10, 9, 2, 5, 3, 7, 101, 18]


One LIS:

2 5 7 101


length:

4


# MENTAL MODEL

CURRENT ELEMENT
│
├── Look backward
│
├── Find smaller previous elements
│
└── Extend the best sequence


# IMPORTANT

dp[i]

does NOT mean:

"LIS of first i elements"


It means:

"LIS ending exactly at i."


This distinction is critical.


# CONNECTION

LIS
 ↓
SUBSEQUENCE
 ↓
LOOK BACKWARD
 ↓
1D DP


LCS
 ↓
SUBSEQUENCE
 ↓
TWO STRINGS
 ↓
2D DP


Both are subsequence problems,
but their states differ.


# 94. MAXIMUM PRODUCT SUBARRAY

## SOURCE CONNECTION

Maximum Product Subarray is explicitly listed in the IBM DP question bank. :contentReference[oaicite:12]{index=12}

---

MAX PRODUCT SUBARRAY
│
├── STORY
│      └── contiguous subarray
│          with maximum product
│
├── KEY PROBLEM
│      │
│      └── Negative number
│          can change
│          minimum → maximum
│
├── THEREFORE
│      │
│      ├── max product ending here
│      └── min product ending here
│
├── STATE
│      │
│      ├── maxHere
│      └── minHere
│
└── WHY MIN?

negative × negative
=
positive


# EXAMPLE

[-2, 3, -4]


At -2:

max = -2
min = -2


At 3:

max = 3
min = -6


At -4:

The previous minimum:

-6

× -4

=

24


Therefore:

maximum becomes 24.


# MENTAL MODEL

NORMAL DP
 ↓
Track best


PRODUCT + NEGATIVES
 ↓
Best can come from
WORST previous value


Therefore:

TRACK BOTH:

MAX
+
MIN


# CONNECTION

Maximum Subarray Sum
 ↓
Kadane
 ↓
track maximum


Maximum Product Subarray
 ↓
Kadane-like
but negative numbers
require minimum too.


# IMPORTANT

This is an excellent example of:

> "The state must store everything needed for the future."


If you store only max:

you lose the negative minimum
that may become the next maximum.


# 95. DECODE WAYS

## SOURCE CONNECTION

Decode Ways is explicitly listed in the IBM DP question bank. :contentReference[oaicite:13]{index=13}

---

DECODE WAYS
│
├── STORY
│      └── Map numbers to letters
│
│          1 → A
│          2 → B
│          ...
│          26 → Z
│
├── QUESTION
│      └── Number of valid decodings?
│
├── STATE
│
│      dp[i]
│      =
│      number of ways to decode
│      first i characters
│
├── ONE DIGIT
│      ↓
│    valid if non-zero
│
├── TWO DIGITS
│      ↓
│    valid if between
│    10 and 26
│
└── TRANSITION

dp[i]
=
ways using last one digit
+
ways using last two digits


# EXAMPLE

"12"


Possible:

1 2
A B

12
L


Answer:

2


# MENTAL MODEL

At every position:

Can I decode
ONE character?

Can I decode
TWO characters?


Therefore:

ONE-STEP
+
TWO-STEP


# CONNECTION

CLIMBING STAIRS
│
├── 1 step
└── 2 steps


DECODE WAYS
│
├── 1 digit
└── 2 digits


Same structural idea:

CURRENT POSITION
 ↓
possible previous positions


But Decode Ways has
VALIDITY CONDITIONS.


# IMPORTANT EDGE CASE

"0"

Cannot independently represent
a letter.


Therefore:

zero handling is critical.


Examples:

10 → valid


01 → invalid under standard decoding rules.


# 96. WORD BREAK

## SOURCE CONNECTION

Word Break is explicitly listed in the IBM DP question bank. :contentReference[oaicite:14]{index=14}

---

WORD BREAK
│
├── INPUT
│      ├── string s
│      └── dictionary
│
├── QUESTION
│      └── Can s be segmented
│          into dictionary words?
│
├── STATE
│
│      dp[i]
│      =
│      whether first i characters
│      can be segmented
│
├── BASE
│
│      dp[0] = true
│
├── TRANSITION
│
│      find j < i
│
│      if:
│
│      dp[j] == true
│      AND
│      s[j...i-1] is dictionary word
│
│      then:
│
│      dp[i] = true
│
└── ANSWER

dp[n]


# EXAMPLE

s:

leetcode


dictionary:

["leet", "code"]


leet
 ↓
code


Therefore:

true


# MENTAL MODEL

STRING
│
├── choose a prefix
│
├── if dictionary word
│
└── solve remaining suffix


Equivalent viewpoint:

Can I reach position i
from an earlier valid position j?


# CONNECTION

WORD BREAK
 ↓
POSITION DP


DECODE WAYS
 ↓
POSITION DP


CLIMBING STAIRS
 ↓
POSITION DP


All ask:

> What valid states can reach the current position?


# SET 7 — DP PATTERN MAP

DP
│
├── 1D DP
│      │
│      ├── Climbing Stairs
│      ├── House Robber
│      ├── Coin Change
│      ├── LIS
│      ├── Decode Ways
│      └── Word Break
│
├── 2D DP
│      │
│      ├── LCS
│      ├── Edit Distance
│      └── 0/1 Knapsack
│
├── TAKE / SKIP
│      │
│      ├── House Robber
│      └── 0/1 Knapsack
│
├── SUBSEQUENCE
│      │
│      ├── LIS
│      └── LCS
│
├── STRING DP
│      │
│      ├── LCS
│      ├── Edit Distance
│      ├── Decode Ways
│      └── Word Break
│
└── SPECIAL STATE
       │
       └── Maximum Product
           ↓
         max + min


# SET 7 — THE MOST IMPORTANT DP QUESTION

Whenever you see a new DP problem:

ASK:

1. What changes?

2. What information from the past
   affects my current decision?

3. What should dp[state] mean?

4. What choices do I have?

5. Which previous states lead to
   this current state?

6. What are the base cases?

7. Can I compute smaller states first?


# DP SOLVING FRAMEWORK

PROBLEM
   ↓
1. DEFINE STATE
   ↓
2. DEFINE CHOICES
   ↓
3. WRITE TRANSITION
   ↓
4. BASE CASE
   ↓
5. MEMOIZATION
   ↓
6. TABULATION
   ↓
7. SPACE OPTIMIZATION


# STEP 1 — DEFINE STATE

Examples:

Climbing Stairs:

dp[i]
=
ways to reach i


House Robber:

dp[i]
=
max money from first i houses


Coin Change:

dp[x]
=
minimum coins for amount x


LIS:

dp[i]
=
LIS ending at i


LCS:

dp[i][j]
=
LCS of first i and first j


Edit Distance:

dp[i][j]
=
minimum operations between prefixes


Word Break:

dp[i]
=
whether first i chars can be segmented


# STEP 2 — FIND CHOICES

CLIMBING STAIRS

1 step
OR
2 steps


HOUSE ROBBER

take
OR
skip


KNAPSACK

take
OR
skip


COIN CHANGE

choose a coin


LCS

match
OR
skip one side


EDIT DISTANCE

insert
OR
delete
OR
replace


DECODE WAYS

one digit
OR
two digits


WORD BREAK

choose a valid word


# STEP 3 — TRANSITION

Current state
        ↓
Which previous states
can produce it?


This is the heart of DP.


# SET 7 — STATE CONNECTION MAP

CLIMBING STAIRS
│
└── dp[i]
     ↓
   previous positions


DECODE WAYS
│
└── dp[i]
     ↓
   previous 1/2 positions


WORD BREAK
│
└── dp[i]
     ↓
   previous valid cut positions


HOUSE ROBBER
│
└── dp[i]
     ↓
   i-1 / i-2


These are structurally related.


# SET 7 — TAKE / SKIP FAMILY

HOUSE ROBBER
│
├── TAKE
│      ↓
│    i-2
│
└── SKIP
       ↓
     i-1


0/1 KNAPSACK
│
├── TAKE
│      ↓
│    previous item
│    + remaining capacity
│
└── SKIP
       ↓
     previous item


The common mental structure:

CURRENT ITEM
│
├── TAKE
│
└── SKIP


But the state differs according to the constraint.


# SET 7 — SUBSEQUENCE FAMILY

LIS
│
└── One sequence
     ↓
   previous elements


LCS
│
└── Two sequences
     ↓
   two positions


KEY DIFFERENCE:

LIS
=
one-dimensional state


LCS
=
two-dimensional state


# SET 7 — STRING DP FAMILY

STRING DP
│
├── LCS
│      ↓
│    compare two strings
│
├── Edit Distance
│      ↓
│    transform one string
│
├── Decode Ways
│      ↓
│    valid digit grouping
│
└── Word Break
       ↓
    valid dictionary cuts


# SET 7 — STORY DECODING CHEAT SHEET

STORY
│
├── "Number of ways to climb"
│      ↓
│    1D DP
│
├── "Cannot rob adjacent"
│      ↓
│    TAKE / SKIP DP
│
├── "Minimum coins"
│      ↓
│    COIN CHANGE
│
├── "Each item used once"
│      ↓
│    0/1 KNAPSACK
│
├── "Longest increasing subsequence"
│      ↓
│    LIS DP
│
├── "Common subsequence of two strings"
│      ↓
│    LCS
│
├── "Minimum operations to transform strings"
│      ↓
│    EDIT DISTANCE
│
├── "Maximum product contiguous subarray"
│      ↓
│    MAX + MIN
│
├── "Number of valid decodings"
│      ↓
│    1-digit / 2-digit DP
│
└── "Can string be split into dictionary words?"
       ↓
    WORD BREAK DP


# SET 7 — PRIORITY

## TIER 1 — FOUNDATION

These should be mastered first because they teach the core DP mechanics.

├── [ ] 83. Climbing Stairs
├── [ ] 84. Memoization
├── [ ] 85. Tabulation
├── [ ] 86. House Robber
└── [ ] 87. Coin Change


# TIER 2 — CORE DP

├── [ ] 88. 0/1 Knapsack
├── [ ] 89. Longest Common Subsequence
├── [ ] 90. Longest Increasing Subsequence
└── [ ] 91. Edit Distance


# TIER 3 — STRING / SPECIAL DP

├── [ ] 92. Decode Ways
├── [ ] 93. Word Break
└── [ ] 94. Maximum Product Subarray


# SOURCE-BASED NOTE

The IBM source lists all ten DP problems but does not provide individual frequency percentages for them in the retrieved material. Therefore the above Tier ordering is a learning/prerequisite ordering, NOT an IBM frequency ranking. :contentReference[oaicite:15]{index=15}


# SET 7 — CHECKLIST

SET 7 — DYNAMIC PROGRAMMING
│
├── FOUNDATIONS
│      ├── [ ] DP state
│      ├── [ ] Recurrence
│      ├── [ ] Base case
│      ├── [ ] Memoization
│      └── [ ] Tabulation
│
├── 1D DP
│      ├── [ ] Climbing Stairs
│      ├── [ ] House Robber
│      ├── [ ] Coin Change
│      ├── [ ] LIS
│      ├── [ ] Decode Ways
│      └── [ ] Word Break
│
├── 2D DP
│      ├── [ ] 0/1 Knapsack
│      ├── [ ] LCS
│      └── [ ] Edit Distance
│
└── SPECIAL
       ├── [ ] Maximum Product Subarray
       └── [ ] House Robber II
           (general DSA extension)


# SET 7 — COMPLEXITY CHEAT SHEET

CLIMBING STAIRS
    ↓
O(n)


HOUSE ROBBER
    ↓
O(n)


COIN CHANGE
    ↓
O(amount × number of coins)


0/1 KNAPSACK
    ↓
O(n × capacity)


LCS
    ↓
O(n × m)


EDIT DISTANCE
    ↓
O(n × m)


LIS — basic DP
    ↓
O(n²)


LIS — optimized method
    ↓
O(n log n)


DECODE WAYS
    ↓
O(n)


WORD BREAK
    ↓
depends on implementation,
commonly O(n²) plus
dictionary lookup cost


MAX PRODUCT SUBARRAY
    ↓
O(n)


# SET 7 — SPACE COMPLEXITY

1D DP

Usually:

O(n)


Can often be optimized to:

O(1)


Example:

Climbing Stairs

Only need:

previous 2 states.


HOUSE ROBBER

Only need:

dp[i-1]
dp[i-2]


Therefore:

O(1) space possible.


2D DP:

LCS
Edit Distance
Knapsack


Often:

O(n × m)


or:

O(n × capacity)


Can sometimes be reduced to one dimension.


# SET 7 — COMMON DP TRAPS

├── [ ] Defining dp[i] incorrectly
├── [ ] Missing base cases
├── [ ] Wrong transition
├── [ ] Confusing subsequence with substring
├── [ ] Reusing a 0/1 item accidentally
├── [ ] Forgetting impossible states
├── [ ] Mishandling zero in Decode Ways
├── [ ] Tracking only max in Maximum Product
├── [ ] Confusing LIS state with prefix LIS
└── [ ] Optimizing space before understanding state


# SET 7 — SUBSEQUENCE vs SUBSTRING

SUBSEQUENCE
│
├── Order maintained
└── Characters/elements
    do NOT need to be adjacent


SUBSTRING
│
└── Must be contiguous


Example:

"abcde"


"ace"

is a:

SUBSEQUENCE


but NOT:

SUBSTRING.


This distinction is essential for:

LIS
LCS


# SET 7 — DP EDGE CASES

CLIMBING STAIRS
├── [ ] n = 0
└── [ ] n = 1


HOUSE ROBBER
├── [ ] empty
├── [ ] one house
└── [ ] two houses


COIN CHANGE
├── [ ] amount = 0
├── [ ] impossible amount
└── [ ] coin > amount


KNAPSACK
├── [ ] capacity = 0
├── [ ] no items
└── [ ] item weight > capacity


LCS
├── [ ] empty string
└── [ ] completely different strings


EDIT DISTANCE
├── [ ] one empty string
└── [ ] both empty


LIS
├── [ ] one element
├── [ ] strictly decreasing
└── [ ] all equal


MAX PRODUCT
├── [ ] zero
├── [ ] negative numbers
└── [ ] multiple negatives


DECODE WAYS
├── [ ] 0
├── [ ] 10
├── [ ] 20
├── [ ] invalid leading zero
└── [ ] 26


WORD BREAK
├── [ ] empty string
├── [ ] no valid segmentation
└── [ ] overlapping dictionary words


# SET 7 — CORE DP TEMPLATE

## MEMOIZATION

```cpp
int solve(int state)
{
    if(base_case)
        return base_answer;

    if(dp[state] != -1)
        return dp[state];

    dp[state] = transition;
    return dp[state];
}



TABULATION
vector<int> dp(n + 1);

dp[base] = base_answer;

for(int i = start; i <= n; i++)
{
    dp[i] = transition;
}

return dp[n];
SET 7 — 2D DP TEMPLATE
vector<vector<int>> dp(
    n + 1,
    vector<int>(m + 1, 0)
);

for(int i = 1; i <= n; i++)
{
    for(int j = 1; j <= m; j++)
    {
        // transition
    }
}
SET 7 — DP DEBUGGING SYSTEM

If your DP answer is wrong:

CHECK IN THIS ORDER:

What exactly does dp[state] mean?

Are the base cases correct?

Can every transition reach
the state?

Are impossible states handled?

Are you taking:

min?

max?

sum?

boolean OR?

Are you accidentally reusing
an item that should be used once?

Are indices shifted correctly?

SET 7 — OPERATOR CONNECTION

DP answers often combine states using:

COUNTING
↓
SUM

MINIMUM
↓
MIN

MAXIMUM
↓
MAX

POSSIBILITY
↓
OR / BOOLEAN

Therefore:

Before coding, ask:

"What am I optimizing or counting?"

SET 7 — DP OPERATION MAP

CLIMBING STAIRS
↓
COUNT
↓
SUM

COIN CHANGE
↓
MINIMUM
↓
MIN

HOUSE ROBBER
↓
MAXIMUM
↓
MAX

KNAPSACK
↓
MAXIMUM VALUE
↓
MAX

LCS
↓
MAXIMUM LENGTH
↓
MAX

EDIT DISTANCE
↓
MINIMUM OPERATIONS
↓
MIN

WORD BREAK
↓
POSSIBILITY
↓
BOOLEAN

DECODE WAYS
↓
COUNT
↓
SUM

SET 7 — MOST IMPORTANT CONNECTIONS
CONNECTION 1 — RECURSION → DP

RECURSION
│
├── repeated calls
│
└── overlapping subproblems
↓
MEMOIZATION
↓
TABULATION

This is why understanding recursion matters before DP.

CONNECTION 2 — FIBONACCI → CLIMBING STAIRS

FIBONACCI:

F(i)

F(i-1)
+
F(i-2)

CLIMBING STAIRS:

dp[i]

dp[i-1]
+
dp[i-2]

Same recurrence structure.

But:

the state meaning is different.

Fibonacci:

value of sequence

Climbing:

number of ways

CONNECTION 3 — HOUSE ROBBER → KNAPSACK

HOUSE ROBBER:

TAKE
or
SKIP

KNAPSACK:

TAKE
or
SKIP

But:

House Robber:
adjacent restriction

Knapsack:
capacity restriction

Same decision pattern.

CONNECTION 4 — LCS → EDIT DISTANCE

Both:

TWO STRINGS
↓
2D STATE
↓
dp[i][j]

LCS:

match
or
skip

Edit Distance:

match
or
insert/delete/replace

CONNECTION 5 — DECODE WAYS → CLIMBING STAIRS

CLIMBING:

move 1
or
move 2

DECODE:

use 1 digit
or
use 2 digits

Both:

CURRENT POSITION
↓
possible previous positions

But Decode Ways adds:

VALIDITY CONDITIONS.

CONNECTION 6 — LIS → LCS

LIS:

one sequence

LCS:

two sequences

Both:

SUBSEQUENCE

Both:

maintain order

But:

LIS:
one-dimensional state

LCS:
two-dimensional state

CONNECTION 7 — MAX PRODUCT → KADANE

Maximum Subarray:

track:

maxHere

Maximum Product:

track:

maxHere
+
minHere

Why?

NEGATIVE × NEGATIVE

POSITIVE

SET 7 — MASTER STORY

DP
│
├── "Repeated subproblems"
│ ↓
│ STORE ANSWERS
│
├── "Number of ways"
│ ↓
│ SUM STATES
│
├── "Minimum"
│ ↓
│ MIN STATES
│
├── "Maximum"
│ ↓
│ MAX STATES
│
├── "Can it be done?"
│ ↓
│ BOOLEAN DP
│
├── "Take or skip"
│ ↓
│ DECISION DP
│
├── "Two strings"
│ ↓
│ 2D STRING DP
│
├── "Subsequence"
│ ↓
│ LIS / LCS FAMILY
│
├── "Each item once"
│ ↓
│ 0/1 KNAPSACK
│
├── "Negative products"
│ ↓
│ MAX + MIN
│
└── "Positions can be reached
in different ways"
↓
POSITION DP

SET 7 — FINAL RECOGNITION RULES
DP starts with state definition, not code.
Write what dp[i] means before implementing.
If recursion repeats the same subproblem, think memoization.
Memoization = top-down.
Tabulation = bottom-up.
Climbing Stairs = previous reachable states.
House Robber = take/skip with adjacency constraint.
Coin Change = minimum over choices.
0/1 Knapsack = take/skip + capacity + item used once.
LCS = two strings + 2D DP.
LIS = one sequence + subsequence ending at i.
Edit Distance = insert/delete/replace.
Maximum Product = track both max and min.
Decode Ways = one-digit/two-digit transitions with validity.
Word Break = valid previous cut + dictionary word.
Subsequence ≠ substring.
Do not optimize space before understanding the full DP table.
A DP state must contain enough information to determine future decisions.
If the future depends on something you discarded from the state, your state is incomplete.
The recurrence is simply the mathematical description of how the current state is produced from previous states.
SET 7 — COMPLETE MENTAL STORY

RECURSION
↓
REPEATED SUBPROBLEMS
↓
MEMOIZATION
↓
TABULATION
↓
DEFINE STATE
↓
FIND TRANSITION
↓
BASE CASE
↓
SOLVE

CLIMBING STAIRS
↓
POSITION DP

HOUSE ROBBER
↓
TAKE / SKIP

COIN CHANGE
↓
MINIMUM CHOICE

0/1 KNAPSACK
↓
TAKE / SKIP + CAPACITY

LIS
↓
SUBSEQUENCE + LOOK BACK

LCS
↓
TWO STRINGS + 2D

EDIT DISTANCE
↓
TWO STRINGS + OPERATIONS

MAX PRODUCT
↓
MAX + MIN

DECODE WAYS
↓
ONE / TWO DIGIT

WORD BREAK
↓
VALID PREFIX / CUT

SET 7 — WHAT YOU SHOULD BE ABLE TO SEE

"Number of ways to reach n"
↓
1D DP

"Cannot choose adjacent"
↓
TAKE / SKIP

"Minimum number of coins"
↓
MIN DP

"Each item only once"
↓
0/1 KNAPSACK

"Longest increasing subsequence"
↓
LIS

"Longest common subsequence"
↓
2D DP

"Transform one string into another"
↓
EDIT DISTANCE

"Maximum product"
↓
MAX + MIN

"Decode a numeric string"
↓
1 / 2 digit DP

"Split into dictionary words"
↓
WORD BREAK

SET 7 — REVISION STRATEGY

The DSA resource specifies this spaced-repetition schedule:

Day of solve
↓
Understand pattern fully

Day 3
↓
Re-solve from scratch
without hints

Day 7
↓
Re-solve in 10 minutes
speed drill

Day 21
↓
Mental walkthrough

It also recommends writing 3 lines after each topic:

What type of problem triggers this pattern?
What's the template?
What's the trap/edge case?
SET 7 — FINAL CHECKLIST

[ ] I can explain what DP is.

[ ] I know what an overlapping subproblem is.

[ ] I can identify a DP state.

[ ] I can write a recurrence.

[ ] I can define base cases.

[ ] I understand memoization.

[ ] I understand tabulation.

[ ] I can convert simple recursion to memoization.

[ ] I can convert memoization to tabulation.

[ ] I can solve Climbing Stairs.

[ ] I can solve House Robber.

[ ] I can solve Coin Change.

[ ] I can solve 0/1 Knapsack.

[ ] I can solve LCS.

[ ] I can solve LIS.

[ ] I can solve Edit Distance.

[ ] I can solve Maximum Product Subarray.

[ ] I can solve Decode Ways.

[ ] I can solve Word Break.

[ ] I can identify the pattern without being told.
