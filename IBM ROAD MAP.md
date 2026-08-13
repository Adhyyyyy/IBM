# IBM Online Assessment — Priority-Based Coding & DSA Preparation Roadmap

## 1. What the evidence actually tells us

The uploaded IBM question bank identifies:

* Array and String problems as approximately **60% of coding questions**.
* Linked-list problems as appearing in **85% of technical interviews**.
* Bit manipulation as a high-priority area.
* SQL queries as a recurring assessment/interview area.
* Greedy and Heap questions in the 2025 OA examples.
* The explicitly reported OA questions include IPv4→IPv6, last-word length, circle relationships, consecutive-error counting, Dutch National Flag, pair sum, stock buy/sell, word concatenation, palindrome, pangram, HCF, divisible triplets/subarrays, pattern printing, greedy resource allocation, max heap, SQL joins, if/else logic, duplicates, linked-list removal, GCD, palindrome construction and kth factor.

Recent independent experiences confirm that IBM's exact OA format varies by drive. Examples include:

* 2025 campus OA: 2 coding questions, described as very easy, involving anagram and priority queue.
* Another 2025 campus drive: first coding assessment had Greedy + Max Heap; a later assessment had if/else, SQL JOIN and pattern printing.
* A 2024 IBM experience reported 2 coding questions: IPv4→IPv6 and last-word length.
* Another experience reported stock buy/sell and reverse linked list variants.
* A 2025 Reddit candidate reported a 2-question HackerRank screening with linked-list and string-manipulation questions.

Therefore, **no responsible preparation plan can assign a guaranteed numerical probability of selection**. What we can do is increase your coverage of the patterns most strongly represented in the available evidence.

---

# 2. The strategy

We will use eight progressive sets.

The order is intentional:

**Set 1 → highest immediate OA ROI**

Then each subsequent set expands the range of patterns you can recognize.

The goal is not merely:

> "I solved this exact problem."

The goal is:

> "IBM changed the story, but I immediately recognize the underlying pattern."

For every problem we will train:

**Story → decode → pattern → intuition → brute force → optimization → code → edge cases → complexity → timed re-solve**

---

# SET 1 — IBM Direct OA Core

## Priority: 🔥🔥🔥🔥🔥

This is the first set you should complete.

These are either explicitly reported OA questions or extremely close to the recurring basic patterns in the resource.

### Strings

1. Length of Last Word
2. Pangram
3. Reverse String
4. String Compression
5. Valid Parentheses
6. Longest Substring Without Repeating Characters
7. Group Anagrams
8. Concatenated-Word String

### Arrays / Hashing

9. Pair With Given Sum / Two Sum
10. Print All Duplicates
11. Find Missing Number
12. Remove Duplicates From Sorted Array
13. Common Elements in Three Sorted Arrays

### Basic Algorithms

14. Best Time to Buy and Sell Stock
15. Maximum Subarray — Kadane
16. Dutch National Flag
17. Binary Search
18. Prime Check

### Why Set 1 comes first

The PDF explicitly places many of these in the reported OA questions and says arrays/strings represent about 60% of coding questions.

**Target after Set 1:**

You should be able to see a basic IBM story and identify:

* frequency counting
* hashing
* two pointers
* traversal
* Kadane
* binary search
* simple string parsing

almost immediately.

---

# SET 2 — Hashing + Sliding Window + Prefix/Sum Patterns

## Priority: 🔥🔥🔥🔥🔥

This set is extremely important because IBM can disguise simple algorithms inside practical stories.

19. Count Subarrays Whose Sum Is Divisible by K
20. Count Triplets Whose Sum Is Divisible by K
21. Subarray Sum Equals K
22. Longest Substring Without Repeating Characters
23. Group Anagrams
24. Two Sum variations
25. Count Vowels / Character Frequency
26. Array Frequency / Duplicate Detection
27. Common Elements in Sorted Arrays
28. Container With Most Water
29. Three Sum

### Pattern recognition targets

You must learn to see:

```text
"appears repeatedly"
        ↓
HashMap / frequency

"within a window"
        ↓
Sliding Window

"sum of a range"
        ↓
Prefix Sum

"sum divisible by K"
        ↓
Prefix Sum + Modulo

"pair"
        ↓
Hashing / Two Pointer

"triplet"
        ↓
Sorting + Two Pointer
```

The PDF explicitly reports divisible-subarray and divisible-triplet questions and includes the same patterns in its DSA bank.

---

# SET 3 — Linked List Core

## Priority: 🔥🔥🔥🔥½

30. Create Linked List Node
31. Reverse Linked List — Iterative
32. Reverse Linked List — Recursive
33. Detect Cycle — Floyd
34. Find Middle Node
35. Merge Two Sorted Linked Lists
36. Remove Nth Node From End
37. Intersection of Two Linked Lists
38. Add Two Numbers Represented by Lists
39. Flatten Multilevel Linked List
40. Copy List With Random Pointer

### Priority within this set

Master these first:

```text
Reverse Linked List
        ↓
Middle Node
        ↓
Cycle Detection
        ↓
Merge Sorted Lists
        ↓
Remove Nth Node
```

The PDF specifically calls linked-list cycle detection one of its critical/high-frequency areas and reports several of these as actual interview questions.

Recent candidate evidence also includes linked-list questions in HackerRank screening.

---

# SET 4 — Greedy + Heap + Priority Queue

## Priority: 🔥🔥🔥🔥½

This set gets elevated because **recent IBM OA evidence specifically contains it**.

41. Greedy Resource Allocation
42. Max Heap — Insert
43. Max Heap — Delete
44. Max Heap — Heapify
45. Kth Largest Element
46. Top K Frequent Elements
47. Merge K Sorted Lists
48. Median From Data Stream
49. Task Scheduler
50. Stock Span

### Why this is unusually important

This isn't just generic DSA theory.

A 2025 IBM campus experience explicitly reports:

> Coding Assessment 1: **Greedy + Max Heap**

and another IBM experience reports:

> **Anagram + Priority Queue**

as its two OA questions.

The uploaded PDF independently lists Max Heap Operations as a 2025 OA question.

Therefore this set gets a higher priority than its usual position in a generic placement roadmap.

---

# SET 5 — Bit Manipulation + Mathematics

## Priority: 🔥🔥🔥🔥

51. Power of Two
52. Single Number
53. Number of 1 Bits
54. Reverse Bits
55. XOR Problems
56. Bitwise AND of Numbers Range
57. Swap MSB and LSB
58. Detect Endianness
59. HCF Without Recursion
60. GCD of Array
61. Kth Factor of N
62. Prime Number Check
63. Fibonacci
64. Factorial
65. Power Function
66. Circle Relationships

The PDF explicitly reports MSB/LSB swap, endianness, power-of-two, HCF, GCD, kth factor and circle relationships.

### Recognition targets

```text
"only one number appears differently"
        ↓
XOR

"power of 2"
        ↓
n & (n-1)

"GCD/HCF"
        ↓
Euclidean algorithm

"kth factor"
        ↓
factor enumeration / sqrt(n)

"binary representation"
        ↓
bit manipulation
```

---

# SET 6 — Trees + Graphs

## Priority: 🔥🔥🔥

67. Binary Tree Inorder Traversal
68. Maximum Depth of Binary Tree
69. Validate BST
70. Lowest Common Ancestor
71. Level Order Traversal
72. Binary Tree From Preorder + Inorder
73. Number of Islands
74. Course Schedule
75. Clone Graph
76. Word Ladder
77. Graph Valid Tree
78. Alien Dictionary

### Why this is below Sets 1–5

These problems are explicitly present in the PDF's broader DSA bank, but they have **less direct OA evidence in the supplied source** than the array/string, heap, greedy, linked-list, bit and mathematical categories.

We still cover them because your objective is robust pattern recognition, not merely surviving one expected OA.

---

# SET 7 — Dynamic Programming

## Priority: 🔥🔥🔥

79. Climbing Stairs
80. House Robber
81. Coin Change
82. 0/1 Knapsack
83. Longest Increasing Subsequence
84. Longest Common Subsequence
85. Edit Distance
86. Decode Ways
87. Word Break

### Important

DP is in the PDF, but it is **not among the strongest direct OA signals in this particular resource**.

Therefore we don't spend the first part of IBM preparation here.

You already studied DP substantially during your FoodHub preparation, so this set should primarily be **pattern revision**, not starting from zero.

---

# SET 8 — IBM Practical / Non-DSA Coding

## Priority: 🔥🔥🔥🔥

This set deserves special attention because recent IBM assessments show that the OA is not necessarily a pure LeetCode test.

88. Simple If-Else Logic
89. Pattern Printing
90. Employee–Department SQL JOIN
91. SQL GROUP BY / HAVING / Aggregation
92. Second Highest Salary
93. Anagram-Based Problem
94. IPv4 → IPv6
95. Grammar Checker
96. Circle Relationship

The first 96 here is **not a claim that the PDF numbers these as 1–96**. It is our preparation sequence.

The PDF explicitly reports SQL JOIN, if/else, pattern printing and IPv4/last-word questions in OA experiences.

Recent IBM evidence strongly supports keeping SQL and simple coding in the preparation: one 2025 drive had **if/else + SQL JOIN + pattern printing**, while another reported a SQL question in its assessment.

---

# 3. Where your existing work fits

You are **not starting from zero**.

### Already covered

| Problem/topic         | Status |
| --------------------- | ------ |
| Max Uniform Team Size | 🟢     |
| Trie fundamentals     | 🟢     |
| TrieNode              | 🟢     |
| Trie insertion        | 🟢     |
| Trie search           | 🟢     |
| Trie startsWith       | 🟢     |
| Trie prefix counting  | 🟢     |

### In progress

| Problem           | Status |
| ----------------- | ------ |
| Complete Prefixes | 🟡     |

### Not yet completed in this IBM sequence

Everything else above remains 🔴 until we actually practice it.

---

# 4. Your actual priority ladder

If you suddenly had very little time, this is the order I would use:

```text
                    IBM OA
                      │
          ┌───────────┴───────────┐
          │                       │
     ARRAY / STRING            PRACTICAL
          │                       │
       SET 1                  SET 8
          │
       SET 2
          │
   ┌──────┴──────┐
   │             │
LINKED LIST    HEAP/GREEDY
 SET 3          SET 4
   │             │
   └──────┬──────┘
          │
       SET 5
   BIT + MATH
          │
     ┌────┴────┐
     │         │
   TREES      DP
   SET 6      SET 7
```

---

# 5. How your readiness should increase

We should **not** say:

> "After Set 1 your probability is exactly 40%."

There is no dataset in the sources that supports such a numerical probability.

Instead, use this readiness model:

| Completion | Readiness meaning                                             |
| ---------- | ------------------------------------------------------------- |
| Set 1      | Basic IBM OA stories become recognizable                      |
| Set 1 + 2  | Strong coverage of the PDF's dominant array/string category   |
| + Set 3    | Strong linked-list coverage                                   |
| + Set 4    | Coverage of recent Greedy/Heap OA evidence                    |
| + Set 5    | Strong basic/medium algorithm coverage                        |
| + Set 8    | Better protection against IBM's practical/simple/SQL-style OA |
| + Set 6    | Broader DSA safety                                            |
| + Set 7    | DP safety                                                     |

So **Sets 1–5 + 8 are the core IBM OA package**.

Sets 6–7 are the **insurance layer**.

---

# 6. Your 100% solving training system

Simply solving these problems once is **not enough**, especially given your previous OA experience.

For every problem, we will use five passes.

### PASS 1 — Story decoding

I give you the IBM-style statement.

You identify:

* input
* output
* constraints
* what is actually being asked
* irrelevant story information

### PASS 2 — Pattern recognition

Before coding, you answer:

> "What known problem does this remind me of?"

Examples:

```text
"consecutive"
→ running count

"frequency"
→ hashmap

"window"
→ sliding window

"sum divisible by K"
→ prefix remainder

"maximum contiguous"
→ Kadane

"top K"
→ heap

"shortest path"
→ BFS

"prefix"
→ Trie
```

### PASS 3 — Derivation

I **will not immediately give you the solution**.

I'll ask questions until you derive it.

This is exactly what we were doing with Max Team Size and Trie.

### PASS 4 — Independent coding

You write the solution.

I review:

* correctness
* edge cases
* complexity
* implementation errors

### PASS 5 — Blind recall

Later I give you a **different story representing the same pattern**.

You solve it without seeing the original solution.

That is how we'll train against IBM changing the wording.

---

# 7. The first set we should actually resume with

We should **not restart Trie from the beginning**.

We paused at:

> **Complete Prefixes**

Finish that first.

Then begin:

### SET 1

**Problem 1 — Length of Last Word**

Then:

**Problem 2 — Pangram**

**Problem 3 — Reverse String**

**Problem 4 — String Compression**

**Problem 5 — Valid Parentheses**

…and continue through Set 1.

This gives you a clean progression from the material you've already learned.

---

# Final priority verdict

If I were preparing **you specifically** for the IBM OA based on the evidence available:

### Tier S — Must master

* Two Sum / Pair Sum
* String manipulation
* Frequency / HashMap
* Pangram
* Last Word
* Stock Buy/Sell
* Kadane
* Dutch National Flag
* Linked-list reverse
* Linked-list cycle
* Heap / Priority Queue
* Greedy
* SQL JOIN
* Pattern printing
* Simple logic
* IPv4/IPv6
* HCF/GCD

### Tier A — Strongly recommended

* Sliding Window
* Prefix Sum
* Three Sum
* Longest Substring
* Group Anagrams
* Remove Nth Node
* Merge Sorted Lists
* Bit manipulation
* Kth Largest
* Top K
* Circle relationships
* Kth Factor

### Tier B — Insurance

* Trees
* Graphs
* DP
* Advanced linked lists
* Advanced heap problems

**Your highest-ROI route is therefore:**

**Complete Prefixes → Set 1 → Set 2 → Set 3 → Set 4 → Set 5 → Set 8 → Set 6 → Set 7.**

That order is based on the combination of the uploaded IBM question bank's explicit OA data and recent candidate reports—not on generic LeetCode popularity.
