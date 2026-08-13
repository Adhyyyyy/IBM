# IBM OA — MASTER PATTERN NOTEBOOK

ADHY, this is the IBM OA coding roadmap converted into a **pattern-recognition notebook**, rather than just a checklist of LeetCode problems.

The structure is:

**Problem → story clues → mental model → pattern → connection → algorithm → what to remember → traps → complexity → related problems.**

One important source-accuracy point: the uploaded PDF explicitly reports certain questions as OA questions and then gives a broader DSA bank. It does **not** itself number a master list as “96 questions.” Our 96-question sequence is the **deduplicated preparation roadmap we constructed from that resource**, not a literal numbering from the PDF.

---

# IBM OA — MASTER PATTERN NOTEBOOK

IBM OA CODING
│
├── SET 1 — CORE ARRAY + STRING
│      │
│      ├── Highest ROI
│      ├── Direct OA evidence
│      └── Basic patterns hidden inside stories
│
├── SET 2 — HASHING + PREFIX SUM + SLIDING WINDOW
│      │
│      ├── Frequency
│      ├── Subarrays
│      ├── Remainders
│      └── Window patterns
│
├── SET 3 — LINKED LIST
│      │
│      ├── Pointer movement
│      ├── Fast/slow pointer
│      └── In-place manipulation
│
├── SET 4 — GREEDY + HEAP
│      │
│      ├── Recent IBM OA evidence
│      ├── Priority Queue
│      └── Optimization
│
├── SET 5 — BIT + MATHEMATICS
│      │
│      ├── XOR
│      ├── Binary properties
│      ├── GCD
│      └── Number theory
│
├── SET 6 — TREES + GRAPHS
│      │
│      ├── DFS
│      ├── BFS
│      ├── Topological Sort
│      └── Graph connectivity
│
├── SET 7 — DYNAMIC PROGRAMMING
│      │
│      ├── State
│      ├── Transition
│      ├── Memoization
│      └── Tabulation
│
└── SET 8 — IBM PRACTICAL CODING
       │
       ├── SQL
       ├── Pattern Printing
       ├── Simple Logic
       ├── Parsing
       └── IBM-specific practical stories

The PDF specifically states that arrays and strings account for **60% of coding questions**, so Set 1 and Set 2 deliberately come first.

---

# SET 1 — CORE ARRAY + STRING

SET 1
│
├── A. STRING BASICS
│      ├── 1. Length of Last Word
│      ├── 2. Pangram
│      ├── 3. Reverse String
│      ├── 4. String Compression
│      ├── 5. Valid Parentheses
│      ├── 6. Longest Substring Without Repeating Characters
│      ├── 7. Group Anagrams
│      └── 8. Concatenated-Word String
│
├── B. ARRAY + HASHING
│      ├── 9. Two Sum / Pair With Given Sum
│      ├── 10. Print All Duplicates
│      ├── 11. Find Missing Number
│      ├── 12. Remove Duplicates From Sorted Array
│      └── 13. Common Elements in Three Sorted Arrays
│
└── C. CORE ALGORITHMS
       ├── 14. Best Time to Buy and Sell Stock
       ├── 15. Maximum Subarray — Kadane
       ├── 16. Dutch National Flag
       ├── 17. Binary Search
       └── 18. Prime Number Check

The PDF explicitly reports Length of Last Word, Pangram, Pair Sum, Stock Buy/Sell, Dutch National Flag and concatenated-word checking among its OA questions, while the broader DSA bank contains the remaining related patterns.

---

# 1. LENGTH OF LAST WORD

**Source connection:** explicitly reported in the PDF's 2024 OA questions.

LENGTH OF LAST WORD
│
├── STORY
│      │
│      └── Sentence
│             │
│             ├── spaces
│             ├── words
│             └── trailing characters/spaces
│
├── REAL QUESTION
│      │
│      └── Find length of final word
│
├── FIRST THOUGHT
│      │
│      └── I only care about the END
│
├── PATTERN
│      │
│      └── Reverse traversal
│
├── MENTAL MODEL
│      │
│      ├── Start from n-1
│      │
│      ├── Ignore trailing spaces
│      │
│      └── Count characters
│             until space
│
├── CONNECTION
│      │
│      ├── "Last / end"
│      │       ↓
│      │    Traverse backward
│      │
│      └── Similar idea
│              │
│              ├── Last occurrence
│              ├── Rightmost element
│              └── Suffix processing
│
├── WHEN TO USE
│      │
│      └── Problem asks about
│             final/rightmost/suffix
│
├── REMEMBER
│      │
│      ├── Skip trailing spaces first
│      ├── Then count
│      └── Stop at next space
│
├── TRAPS
│      │
│      ├── Empty string
│      ├── All spaces
│      └── Multiple spaces
│
└── COMPLEXITY
       O(n) time
       O(1) extra space

### Pattern connection

"LAST"
   ↓
Don't scan blindly from left.
Ask:
"Can I start from the right?"

This is a very useful IBM story-decoding habit.

---

# 2. PANGRAM

**Source connection:** explicitly reported in the OA section and repeated in the DSA bank.

PANGRAM
│
├── STORY
│      └── Sentence contains letters
│
├── REAL QUESTION
│      └── Does every alphabet character occur?
│
├── PATTERN
│      └── Presence / Frequency Tracking
│
├── MENTAL MODEL
│      │
│      ├── Alphabet = 26 possibilities
│      │
│      ├── Create visited[26]
│      │
│      ├── For every character
│      │      │
│      │      └── mark it
│      │
│      └── At end
│             │
│             └── Are all 26 marked?
│
├── CONNECTION
│      │
│      ├── "Have I seen X?"
│      │       ↓
│      │    Boolean array
│      │
│      ├── "How many X?"
│      │       ↓
│      │    Frequency array
│      │
│      └── "Does X exist?"
│              ↓
│           HashSet / boolean array
│
├── DECISION
│      │
│      └── Fixed small alphabet?
│             ↓
│           array[26]
│
├── REMEMBER
│      │
│      └── Presence ≠ frequency
│
├── TRAP
│      │
│      └── Case sensitivity
│
└── COMPLEXITY
       O(n) time
       O(1) space
       because alphabet size = 26

### Mental connection

PANGRAM
   ↓
Every possible character must appear
   ↓
Track SEEN
   ↓
Boolean / frequency array

This same mental structure later connects to:

- duplicates
- anagrams
- character frequency
- longest substring
- group anagrams

---

# 3. REVERSE STRING

**Source connection:** listed in the Technical Interview coding section and broader DSA bank.

REVERSE STRING
│
├── STORY
│      └── Reverse characters
│
├── PATTERN
│      └── TWO POINTERS
│
├── MENTAL MODEL
│
│      L                         R
│      ↓                         ↓
│     [a][b][c][d][e]
│
│      swap(L,R)
│
│      L++                       R--
│
├── CONNECTION
│      │
│      ├── Reverse Array
│      ├── Palindrome
│      ├── Reverse Linked List
│      └── In-place swapping
│
├── WHEN TO RECOGNIZE
│      │
│      ├── Reverse
│      ├── Mirror
│      ├── From both ends
│      └── Compare left/right
│
├── CORE TEMPLATE
│
│      left = 0
│      right = n-1
│
│      while(left < right)
│      {
│          swap(...)
│          left++
│          right--
│      }
│
├── REMEMBER
│      └── Two pointers move toward center
│
└── COMPLEXITY
       O(n)
       O(1)

### Important connection

REVERSE STRING
      │
      ├───────────────┐
      ↓               ↓
   TWO POINTER      SWAP
      │               │
      ↓               ↓
PALINDROME       REVERSE ARRAY

When you see **reverse**, immediately ask:

> Can I solve this with two pointers?

---

# 4. STRING COMPRESSION

STRING COMPRESSION
│
├── STORY
│      └── Consecutive repeated characters
│
├── REAL QUESTION
│      └── Convert runs into character + count
│
├── PATTERN
│      └── RUN-LENGTH ENCODING
│
├── MENTAL MODEL
│
│      aaabbcccc
│
│      aaa → a3
│      bb  → b2
│      cccc → c4
│
├── CORE IDEA
│      │
│      ├── Start at i
│      ├── Count identical characters
│      └── Move i to next different character
│
├── CONNECTION
│      │
│      ├── Consecutive elements
│      ├── Grouping
│      ├── Frequency of RUN
│      └── Two-pointer style traversal
│
├── STORY CLUES
│      │
│      ├── consecutive
│      ├── repeated
│      ├── compress
│      └── groups
│
├── TRAP
│      └── Frequency of entire string
│             ≠
│          frequency of consecutive run
│
└── COMPLEXITY
       O(n)

### Critical distinction

"aaabb"

Frequency:

a = 3
b = 2

Run structure:

aaa
bb

They happen to be the same here.

But:

"abab"

Frequency:

a = 2
b = 2

Runs:

a
b
a
b

So **do not automatically use HashMap** when the word "count" appears.

Ask:

> **Are the occurrences consecutive?**

---

# 5. VALID PARENTHESES

VALID PARENTHESES
│
├── STORY
│      └── Brackets must close correctly
│
├── PATTERN
│      └── STACK
│
├── MENTAL MODEL
│
│      Opening
│         ↓
│      PUSH
│
│      Closing
│         ↓
│      MATCH TOP
│         ↓
│      POP
│
├── WHY STACK?
│      │
│      └── Last opened bracket
│         must close first
│
│         ↓
│      LIFO
│
├── CONNECTION
│      │
│      ├── Undo
│      ├── Nested structures
│      ├── Function calls
│      ├── Expression parsing
│      └── DFS-style stack
│
├── STORY CLUES
│      │
│      ├── nested
│      ├── matching
│      ├── balanced
│      └── opening/closing
│
├── CORE RULE
│      │
│      ├── opening → push
│      └── closing → must match top
│
├── FINAL CONDITION
│      │
│      └── Stack must be empty
│
└── COMPLEXITY
       O(n) time
       O(n) space

### Mental trigger

NESTED + MATCHING
        ↓
      STACK

Don't think about the actual brackets first.

Think about the **behavior**:

> Last opened → first closed.

That's the pattern.

---

# 6. LONGEST SUBSTRING WITHOUT REPEATING CHARACTERS

**Source connection:** appears in the broader DSA bank.

LONGEST SUBSTRING WITHOUT REPEATING
│
├── STORY
│      └── Longest continuous portion
│             with unique characters
│
├── KEY WORD
│      └── SUBSTRING
│
├── SUBSTRING
│      │
│      └── CONTIGUOUS
│
├── PATTERN
│      └── SLIDING WINDOW
│
├── MENTAL MODEL
│
│      [ l o n g ]
│        ↑     ↑
│       left right
│
│      Maintain a VALID window
│
├── RULE
│      │
│      ├── Add right character
│      │
│      ├── If duplicate
│      │
│      └── Move left until valid
│
├── DATA STRUCTURE
│      │
│      ├── frequency array
│      ├── HashMap
│      └── HashSet
│
├── CONNECTION
│      │
│      ├── Longest substring
│      ├── Minimum window
│      ├── At most K distinct
│      ├── Frequency in window
│      └── Sliding window
│
├── STORY CLUES
│      │
│      ├── substring
│      ├── contiguous
│      ├── longest
│      ├── window
│      └── at most/exactly
│
├── IMPORTANT
│      │
│      └── SUBSTRING
│             ↓
│          contiguous
│             ↓
│          consider window
│
└── COMPLEXITY
       O(n)

### Connection to Set 2

SET 1
Longest Substring
       │
       ▼
Recognize WINDOW
       │
       ▼
SET 2
Sliding Window
       │
       ├── frequency
       ├── distinct count
       ├── constraints
       └── variable window

---

# 7. GROUP ANAGRAMS

GROUP ANAGRAMS
│
├── STORY
│      └── Words containing the same characters
│
├── CORE OBSERVATION
│      │
│      └── Anagrams have
│         identical character frequencies
│
├── PATTERN
│      └── HASHING
│
├── KEY QUESTION
│      │
│      └── "What can I use as
│          the identity/signature
│          of a word?"
│
├── OPTION 1
│      │
│      └── Sort characters
│
│          eat → aet
│          tea → aet
│          ate → aet
│
├── OPTION 2
│      │
│      └── Frequency signature
│
│          a:1
│          e:1
│          t:1
│
├── HASHMAP
│      │
│      └── signature → group
│
├── CONNECTION
│      │
│      ├── Anagram
│      ├── Frequency counting
│      ├── HashMap
│      └── Canonical representation
│
├── STORY CLUES
│      │
│      ├── same letters
│      ├── rearrangement
│      ├── anagram
│      └── group equivalent strings
│
└── COMPLEXITY
       Sorting approach:
       O(n × k log k)

       Frequency signature:
       O(n × k)

### Important mental structure

Different-looking objects
        ↓
Find what makes them equivalent
        ↓
Build a SIGNATURE
        ↓
HashMap
        ↓
Group

This idea is much bigger than anagrams.

---

# 8. CONCATENATED-WORD STRING

**Source connection:** explicitly reported in the 2024 OA section.

CONCATENATED-WORD STRING
│
├── STORY
│      │
│      ├── Given target string
│      └── Given dictionary of words
│
├── QUESTION
│      │
│      └── Can target be formed
│          by concatenating
│          dictionary words?
│
├── CORE RECOGNITION
│      │
│      └── STRING BREAKING
│
├── THINK
│      │
│      ├── Start from index 0
│      ├── Try possible dictionary words
│      ├── If one matches
│      └── Solve remaining suffix
│
├── CONNECTION
│      │
│      ├── Word Break
│      ├── Prefix matching
│      ├── Trie
│      └── Dynamic Programming
│
├── IMPORTANT
│      │
│      └── This is NOT simply
│          substring searching
│
│          because:
│
│          target may require
│          multiple words
│
├── MENTAL MODEL
│
│      target
│      │
│      ├── choose word
│      │
│      ▼
│      remaining suffix
│      │
│      ├── choose word
│      │
│      ▼
│      ...
│
└── RECOGNITION
       "Can this string be
        constructed from pieces?"
                ↓
             Word Break

### Connection

CONCATENATED WORD
       │
       ▼
    WORD BREAK
       │
       ▼
     PREFIX
       │
       ▼
      TRIE
       │
       ▼
  DP / SEARCH

So when we later reach **Word Break in Set 7**, you should immediately remember this OA question.

---

# 9. TWO SUM / PAIR WITH GIVEN SUM

**Source connection:** explicitly reported as an OA question and repeated in the DSA bank.

TWO SUM
│
├── STORY
│      └── Find two values whose sum = target
│
├── FIRST THOUGHT
│      │
│      └── For x
│         need target - x
│
├── PATTERN
│      └── HASHMAP
│
├── MENTAL EQUATION
│
│      x + y = target
│
│      y = target - x
│
├── ALGORITHM
│      │
│      ├── Traverse x
│      ├── calculate need
│      ├── check whether need exists
│      └── store x
│
├── CONNECTION
│      │
│      ├── Complement
│      ├── Frequency
│      ├── HashMap
│      └── Two Pointer if sorted
│
├── DECISION
│
│      Unsorted
│         ↓
│      HashMap
│
│      Sorted
│         ↓
│      Two pointers
│
├── STORY CLUES
│      │
│      ├── pair
│      ├── target sum
│      ├── complement
│      └── two values
│
└── COMPLEXITY
       HashMap:
       O(n) time
       O(n) space

### Critical connection

PAIR + TARGET
      ↓
COMPLEMENT
      ↓
target - current
      ↓
HASHMAP

This is one of the patterns you should be able to recognize **within seconds**.

---

# 10. PRINT ALL DUPLICATES

DUPLICATES
│
├── STORY
│      └── Find repeated values
│
├── QUESTION
│      └── Has this value appeared before?
│
├── PATTERN
│      └── FREQUENCY / SEEN
│
├── OPTIONS
│      │
│      ├── HashSet
│      ├── HashMap
│      ├── Frequency array
│      └── Sorting
│
├── DECISION
│      │
│      ├── Values bounded/small
│      │      ↓
│      │    frequency array
│      │
│      ├── Arbitrary integers
│      │      ↓
│      │    HashMap/Set
│      │
│      └── Need O(1) extra?
│             ↓
│          maybe sorting / marking
│
├── CONNECTION
│      │
│      ├── Pangram
│      ├── Anagram
│      ├── Frequency
│      ├── Two Sum
│      └── Character counting
│
└── CORE QUESTION
       "Have I seen this before?"
              ↓
          SET / MAP

---

# 11. FIND MISSING NUMBER

MISSING NUMBER
│
├── STORY
│      └── Numbers from expected range
│          but one is missing
│
├── PATTERN OPTIONS
│      │
│      ├── Sum formula
│      ├── XOR
│      └── Sorting
│
├── BEST RECOGNITION
│      │
│      └── Expected values form
│          a complete range
│
├── XOR IDEA
│      │
│      ├── x ^ x = 0
│      ├── x ^ 0 = x
│      └── Everything appearing twice cancels
│
├── CONNECTION
│      │
│      ├── Single Number
│      ├── XOR problems
│      └── Bit manipulation
│
└── REMEMBER
       Range + exactly one missing
              ↓
          SUM or XOR

This is an important bridge from Set 1 → Set 5.

---

# 12. REMOVE DUPLICATES FROM SORTED ARRAY

REMOVE DUPLICATES
│
├── KEY WORD
│      └── SORTED
│
├── BIG CLUE
│      │
│      └── Duplicates are adjacent
│
├── PATTERN
│      └── TWO POINTER
│
├── MENTAL MODEL
│
│      read pointer
│           ↓
│      scans every element
│
│      write pointer
│           ↓
│      stores next unique element
│
├── CONNECTION
│      │
│      ├── Sorted array
│      ├── In-place modification
│      ├── Remove duplicates
│      └── Compress array
│
├── STORY CLUE
│      │
│      └── "sorted"
│           ↓
│      exploit ordering
│
└── COMPLEXITY
       O(n)
       O(1)

### Critical recognition rule

SORTED + REMOVE DUPLICATES
             ↓
        TWO POINTERS

Do **not** immediately reach for HashSet.

---

# 13. COMMON ELEMENTS IN THREE SORTED ARRAYS

COMMON ELEMENTS
│
├── KEY WORD
│      └── SORTED
│
├── PATTERN
│      └── MULTIPLE POINTERS
│
├── MENTAL MODEL
│
│      i → array A
│      j → array B
│      k → array C
│
├── QUESTION
│      │
│      └── Which pointer can safely move?
│
├── RULE
│      │
│      └── Move the pointer
│          holding the smallest value
│
├── WHY?
│      │
│      └── It cannot match a larger
│          value unless it increases
│
├── CONNECTION
│      │
│      ├── Merge sorted arrays
│      ├── Intersection
│      ├── Two pointer
│      └── K-way merge
│
└── RECOGNITION
       SORTED + COMMON
              ↓
       MULTIPLE POINTERS

---

# 14. BEST TIME TO BUY AND SELL STOCK

**Source connection:** explicitly reported in the OA section.

STOCK BUY / SELL
│
├── STORY
│      └── Buy once
│          sell later
│
├── CORE QUESTION
│      │
│      └── Best future selling price
│          - minimum previous price
│
├── PATTERN
│      └── ONE-PASS MINIMUM
│
├── MENTAL MODEL
│
│      current price
│            │
│            ▼
│      best profit if sold today
│            │
│            ▼
│      current - minimumSeen
│
├── STATE
│      │
│      ├── minPrice
│      └── maxProfit
│
├── CONNECTION
│      │
│      ├── Prefix minimum
│      ├── One-pass optimization
│      └── Kadane-like running state
│
├── STORY CLUE
│      │
│      ├── maximum profit
│      ├── buy before sell
│      └── one transaction
│
├── TRAP
│      │
│      └── Don't choose global min
│          and global max blindly
│
│          because:
│
│          buy MUST happen before sell
│
└── COMPLEXITY
       O(n)
       O(1)

### Connection to Kadane

STOCK
minimum seen
     ↓
best profit

KADANE
best previous sum
     ↓
best current sum

Both:
ONE-PASS + MAINTAIN STATE

This connection is worth remembering.

---

# 15. MAXIMUM SUBARRAY — KADANE

KADANE
│
├── STORY
│      └── Maximum sum contiguous subarray
│
├── KEY WORD
│      └── CONTIGUOUS
│
├── PATTERN
│      └── KADANE
│
├── CORE QUESTION
│      │
│      └── Should I:
│
│          continue current subarray?
│
│          OR
│
│          start fresh here?
│
├── STATE
│      │
│      ├── currentBest
│      └── globalBest
│
├── DECISION
│
│      current + nums[i]
│            OR
│      nums[i]
│
├── MENTAL EQUATION
│
│      currentBest =
│      max(nums[i],
│          currentBest + nums[i])
│
├── CONNECTION
│      │
│      ├── Stock profit
│      ├── DP
│      ├── Running state
│      └── Contiguous optimization
│
├── STORY CLUES
│      │
│      ├── maximum sum
│      ├── contiguous
│      └── subarray
│
└── COMPLEXITY
       O(n)
       O(1)

### Most important recognition rule

MAXIMUM + CONTIGUOUS SUBARRAY
              ↓
            KADANE

---

# 16. DUTCH NATIONAL FLAG

**Source connection:** explicitly reported in the 2024 OA section.

DUTCH NATIONAL FLAG
│
├── STORY
│      └── Array contains only
│          0, 1, 2
│
├── QUESTION
│      └── Sort in-place
│
├── PATTERN
│      └── THREE POINTER
│
├── POINTERS
│      │
│      ├── low
│      ├── mid
│      └── high
│
├── MENTAL MODEL
│
│      [0s] [unknown] [2s]
│        ↑       ↑       ↑
│       low     mid     high
│
├── RULE
│      │
│      ├── 0 → swap low/mid
│      ├── 1 → mid++
│      └── 2 → swap mid/high
│
├── IMPORTANT
│      │
│      └── When swapping with high,
│          DON'T automatically move mid
│
│          because the incoming value
│          is still unknown
│
├── CONNECTION
│      │
│      ├── Partitioning
│      ├── QuickSort
│      ├── Three-way partition
│      └── In-place array manipulation
│
└── COMPLEXITY
       O(n)
       O(1)

### Recognition

ONLY 3 CATEGORIES
       +
IN-PLACE
       ↓
THREE POINTER PARTITION

---

# 17. BINARY SEARCH

BINARY SEARCH
│
├── KEY REQUIREMENT
│      └── SEARCH SPACE IS ORDERED
│
├── PATTERN
│      └── ELIMINATE HALF
│
├── MENTAL MODEL
│
│      [ L -------- M -------- R ]
│
│      Compare target with M
│
│      target < M
│          ↓
│      discard right half
│
│      target > M
│          ↓
│      discard left half
│
├── CONNECTION
│      │
│      ├── Sorted array
│      ├── Lower bound
│      ├── Upper bound
│      ├── Rotated array
│      └── Binary Search on Answer
│
├── STORY CLUES
│      │
│      ├── sorted
│      ├── find
│      ├── minimum/maximum feasible
│      └── monotonic condition
│
├── BIGGER PATTERN
│
│      Can I ask:
│
│      "Is answer X feasible?"
│
│             ↓
│      Binary Search on Answer
│
└── COMPLEXITY
       O(log n)

### Connection you must remember

SORTED SEARCH
      ↓
Binary Search

MONOTONIC ANSWER
      ↓
Binary Search on Answer

So binary search is not only an array-search algorithm.

---

# 18. PRIME NUMBER CHECK

PRIME CHECK
│
├── STORY
│      └── Is n divisible by
│          anything except 1 and n?
│
├── PATTERN
│      └── DIVISOR CHECK
│
├── NAIVE
│      │
│      └── check 2 → n-1
│
├── OPTIMIZATION
│      │
│      └── check only up to sqrt(n)
│
├── WHY?
│      │
│      └── If n = a × b
│
│          at least one factor
│          must be ≤ sqrt(n)
│
├── CONNECTION
│      │
│      ├── Factor problems
│      ├── Kth factor
│      └── Number theory
│
└── COMPLEXITY
       O(sqrt(n))

### Connection to Set 5

PRIME CHECK
     │
     ├── divisors
     │
     ▼
KTH FACTOR
     │
     ▼
GCD / HCF
     │
     ▼
NUMBER THEORY SET

---

# SET 1 — MEMORY MAP

This is the part to memorize **conceptually**, not as code.

ARRAY / STRING STORY
│
├── "LAST"
│      ↓
│   Reverse traversal
│
├── "EVERY CHARACTER"
│      ↓
│   Seen / Frequency
│
├── "REVERSE"
│      ↓
│   Two pointers
│
├── "CONSECUTIVE REPEATED"
│      ↓
│   Run counting
│
├── "NESTED / MATCHING"
│      ↓
│   Stack
│
├── "LONGEST SUBSTRING"
│      ↓
│   Sliding Window
│
├── "ANAGRAM"
│      ↓
│   Character signature
│      ↓
│   HashMap
│
├── "CAN FORM STRING FROM WORDS"
│      ↓
│   Word Break
│      ↓
│   Trie / DP
│
├── "PAIR + TARGET"
│      ↓
│   Complement
│      ↓
│   HashMap
│
├── "DUPLICATES"
│      ↓
│   Seen / Frequency
│
├── "MISSING FROM RANGE"
│      ↓
│   Sum / XOR
│
├── "SORTED + REMOVE DUPLICATES"
│      ↓
│   Two pointers
│
├── "SORTED + COMMON"
│      ↓
│   Multiple pointers
│
├── "MAX PROFIT"
│      ↓
│   Running minimum
│
├── "MAX CONTIGUOUS SUM"
│      ↓
│   Kadane
│
├── "0,1,2"
│      ↓
│   Three-way partition
│
├── "SORTED SEARCH"
│      ↓
│   Binary Search
│
└── "PRIME / DIVISOR"
       ↓
    sqrt optimization

---

# SET 1 — CHECKLIST

SET 1 — CORE ARRAY + STRING
│
├── [ ] 1. Length of Last Word
├── [ ] 2. Pangram
├── [ ] 3. Reverse String
├── [ ] 4. String Compression
├── [ ] 5. Valid Parentheses
├── [ ] 6. Longest Substring Without Repeating Characters
├── [ ] 7. Group Anagrams
├── [ ] 8. Concatenated-Word String
├── [ ] 9. Two Sum / Pair With Given Sum
├── [ ] 10. Print All Duplicates
├── [ ] 11. Find Missing Number
├── [ ] 12. Remove Duplicates From Sorted Array
├── [ ] 13. Common Elements in Three Sorted Arrays
├── [ ] 14. Best Time to Buy and Sell Stock
├── [ ] 15. Maximum Subarray — Kadane
├── [ ] 16. Dutch National Flag
├── [ ] 17. Binary Search
└── [ ] 18. Prime Number Check

### Your current IBM-specific status

SET 1
│
├── 1  Length of Last Word          🔴
├── 2  Pangram                      🔴
├── 3  Reverse String               🔴
├── 4  String Compression           🔴
├── 5  Valid Parentheses            🔴
├── 6  Longest Substring            🔴
├── 7  Group Anagrams               🔴
├── 8  Concatenated Word            🔴
├── 9  Two Sum                      🔴
├── 10 Print Duplicates             🔴
├── 11 Missing Number               🔴
├── 12 Remove Duplicates            🔴
├── 13 Common Elements              🔴
├── 14 Stock Buy/Sell               🔴
├── 15 Kadane                       🔴
├── 16 Dutch National Flag          🔴
├── 17 Binary Search                🔴
└── 18 Prime Check                  🔴

---

# EXISTING IBM-SPECIFIC STATUS

SET 1
│
├── Max Uniform Team Size           🟢 Covered + independently coded
│
└── Complete Prefixes / Trie        🟡 Started but unfinished

Trie fundamentals already covered:
│
├── TrieNode
├── child[26]
├── nullptr meaning
├── character → index
├── shared prefixes
├── endHere
├── insert()
├── search()
├── startsWith()
├── prefixCount
└── endCount

---

# HOW WE WILL USE THIS NOTEBOOK

For every `[ ]` problem:

QUESTION
   ↓
STORY DECODING
   ↓
WHAT IS ACTUALLY ASKED?
   ↓
PATTERN RECOGNITION
   ↓
CONNECT TO KNOWN PROBLEM
   ↓
YOU DERIVE THE IDEA
   ↓
YOU CODE
   ↓
EDGE CASES
   ↓
TIME + SPACE
   ↓
IBM STORY VARIATION
   ↓
YOU SOLVE AGAIN
   ↓
[✓]

That last **story variation** is important.

Your goal isn't:

> "Two Sum = this exact code."

Your goal is to see:

> "Find two servers whose combined load is X"

or:

> "Find two students whose marks total X"

or:

> "Find two transactions whose values equal X"

and immediately think:

PAIR + TARGET
     ↓
COMPLEMENT
     ↓
target - current
     ↓
HASHMAP

That is the **100%-solving mindset** we're building.

---

# NEXT

The next section is:

# SET 2 — HASHING + PREFIX SUM + SLIDING WINDOW

This is where the connections become much more important because several apparently different IBM stories collapse into the same 4–5 patterns.
