# IBM OA — MASTER PATTERN NOTEBOOK
# SET 2 — HASHING + PREFIX SUM + SLIDING WINDOW

Source basis:
The IBM PYQ resource explicitly lists:
- Two Sum and variations
- Subarray Sum Equals K (2024–2025)
- Count Triplets Divisible by K (2024–2025)
- Longest Substring Without Repeating Characters
- Group Anagrams
- Count Vowels
- Common Elements in Three Sorted Arrays
- Container With Most Water
- Three Sum

The resource also explicitly reports **Count Sub-arrays whose sum is divisible by K** as an OA question. :contentReference[oaicite:0]{index=0}

This set is deliberately built around the common patterns connecting those problems.

---

# SET 2 — BIG PICTURE

SET 2
│
├── HASHING
│      │
│      ├── Frequency
│      ├── Presence
│      ├── Complement
│      └── Grouping by Signature
│
├── PREFIX SUM
│      │
│      ├── Subarray Sum
│      ├── Range Sum
│      ├── Divisibility
│      └── Prefix Remainder
│
├── SLIDING WINDOW
│      │
│      ├── Longest Valid Window
│      ├── Character Frequency
│      ├── Distinct Characters
│      └── Variable Window
│
└── TWO / MULTIPLE POINTERS
       │
       ├── Pair
       ├── Triplet
       ├── Sorted Arrays
       └── Container Problems

---

# SET 2 — MASTER MENTAL MAP

HASHING
│
├── "Have I seen this?"
│       ↓
│    HashSet
│
├── "How many times?"
│       ↓
│    HashMap / Frequency
│
├── "Where did I see this?"
│       ↓
│    HashMap → index
│
├── "What complements current?"
│       ↓
│    target - current
│
└── "What objects are equivalent?"
        ↓
     Signature
        ↓
      HashMap


PREFIX SUM
│
├── "Sum of subarray"
│       ↓
│    Prefix Sum
│
├── "Sum equals K"
│       ↓
│    Prefix Sum + HashMap
│
├── "Sum divisible by K"
│       ↓
│    Prefix Remainder + HashMap
│
└── "Repeated prefix state"
        ↓
     Difference between
     two prefixes gives
     desired subarray


SLIDING WINDOW
│
├── "Substring"
├── "Subarray"
├── "Contiguous"
├── "Longest"
├── "Shortest"
├── "At most K"
└── "Without repetition"
        ↓
    Consider WINDOW


TWO POINTERS
│
├── Sorted + Pair
├── Sorted + Triplet
├── Opposite ends
├── Remove duplicates
└── Container
        ↓
    Pointer movement


---

# 19. SUBARRAY SUM EQUALS K

## STORY

Given an array, find/count subarrays whose sum equals K.

---

SUBARRAY SUM = K
│
├── KEY WORD
│      │
│      ├── SUBARRAY
│      └── SUM
│
├── SUBARRAY
│      │
│      └── CONTIGUOUS
│
├── FIRST THOUGHT
│      │
│      └── Prefix Sum
│
├── PREFIX SUM
│
│      prefix[i]
│
│      =
│
│      sum of elements
│      from beginning → i
│
├── CORE EQUATION
│
│      currentPrefix - oldPrefix = K
│
│
│      Therefore:
│
│      oldPrefix =
│      currentPrefix - K
│
├── PATTERN
│      │
│      └── PREFIX SUM
│             +
│          HASHMAP
│
├── MENTAL MODEL
│
│      [.......i]
│
│      currentPrefix
│
│           -
│
│      previousPrefix
│
│           =
│
│      desired subarray sum
│
├── HASHMAP STORES
│      │
│      └── prefixSum → frequency
│
├── WHY FREQUENCY?
│      │
│      └── The same prefix sum
│          may occur multiple times
│
├── CONNECTION
│      │
│      ├── Subarray Sum Divisible by K
│      ├── Count Triplets Divisible by K
│      ├── Prefix Sum
│      └── HashMap
│
├── STORY CLUES
│      │
│      ├── subarray
│      ├── contiguous
│      ├── sum = K
│      └── number of subarrays
│
├── IMPORTANT
│      │
│      └── Do NOT automatically
│          use sliding window
│
│          because negative numbers
│          may exist.
│
└── COMPLEXITY
       O(n) time
       O(n) space


## MEMORY CONNECTION

SUBARRAY
   +
SUM
   ↓
PREFIX SUM

PREFIX SUM
   +
"How many previous states?"
   ↓
HASHMAP


## RECOGNITION

"Count contiguous portions whose sum equals K"

              ↓

        PREFIX SUM + MAP

---

# 20. SUBARRAYS WHOSE SUM IS DIVISIBLE BY K

## SOURCE CONNECTION

This is explicitly reported as a 2024–2025 IBM OA question:

> Count sub-arrays whose sum is divisible by K. :contentReference[oaicite:1]{index=1}

---

SUBARRAY SUM DIVISIBLE BY K
│
├── STORY
│      └── Find/count subarrays
│          whose sum % K == 0
│
├── KEY DIFFERENCE
│      │
│      └── We don't need
│          exact sum
│
│          We need:
│
│          sum % K == 0
│
├── PREFIX SUM
│
│      Let:
│
│      P[i] = prefix sum
│
├── IMPORTANT EQUATION
│
│      (P[j] - P[i]) % K = 0
│
│      Therefore:
│
│      P[j] % K == P[i] % K
│
├── PATTERN
│      │
│      └── PREFIX REMAINDER
│             +
│          HASHMAP
│
├── HASHMAP
│      │
│      └── remainder → frequency
│
├── MENTAL MODEL
│
│      Same remainder
│          ↓
│      Difference divisible by K
│          ↓
│      Valid subarray
│
├── CONNECTION
│      │
│      ├── Subarray Sum = K
│      ├── Prefix Sum
│      ├── Modulo
│      └── Count frequencies
│
├── STORY CLUES
│      │
│      ├── subarray
│      ├── divisible by K
│      ├── modulo
│      └── count
│
├── IMPORTANT EDGE CASE
│      │
│      └── Negative remainder
│
│          In C++:
│          ((sum % K) + K) % K
│
└── COMPLEXITY
       O(n) time
       O(K) or O(n) space
       depending on implementation


## CRITICAL MEMORY CONNECTION

SUM = K
   ↓
prefix difference = K

DIVISIBLE BY K
   ↓
prefix remainders equal


So:

SUBARRAY SUM
      │
      ├── Exact target
      │      ↓
      │   prefixSum - K
      │
      └── Divisible
             ↓
         same remainder


---

# 21. COUNT TRIPLETS WHOSE SUM IS DIVISIBLE BY K

## SOURCE CONNECTION

Explicitly reported as a 2024–2025 IBM OA question. :contentReference[oaicite:2]{index=2}

---

COUNT TRIPLETS DIVISIBLE BY K
│
├── STORY
│      └── Choose 3 numbers
│          whose sum is divisible by K
│
├── KEY CONDITION
│
│      (a + b + c) % K == 0
│
├── FIRST THOUGHT
│      │
│      └── Don't immediately
│          enumerate every triplet
│
├── IMPORTANT OBSERVATION
│
│      Only remainders matter.
│
│      a % K
│      b % K
│      c % K
│
├── TRANSFORM
│
│      r1 + r2 + r3
│
│      must be divisible by K
│
├── PATTERN
│      │
│      └── FREQUENCY OF REMAINDERS
│
├── MENTAL MODEL
│
│      Store:
│
│      remainder → count
│
│      Then count valid
│      remainder combinations.
│
├── CONNECTION
│      │
│      ├── Subarrays divisible by K
│      ├── Modulo arithmetic
│      ├── Frequency counting
│      └── Combinatorics
│
├── STORY CLUES
│      │
│      ├── triplets
│      ├── divisible by K
│      └── sum condition
│
├── BIG RECOGNITION
│
│      Values themselves
│           ↓
│      often don't matter
│
│      Remainders
│           ↓
│      matter
│
└── COMPLEXITY
       Depends on implementation.
       The key optimization is
       reducing values to K remainder classes.


## CONNECTION

TRIPLET SUM DIVISIBLE BY K
          ↓
       MODULO
          ↓
      remainder
          ↓
      frequency


This is the same mathematical idea as:

SUBARRAY SUM DIVISIBLE BY K

but the **objects being counted are different**.

---

# 22. LONGEST SUBSTRING WITHOUT REPEATING CHARACTERS

## CONNECTION FROM SET 1

We introduced this in Set 1.

Now we deepen the pattern.

---

LONGEST SUBSTRING WITHOUT REPEATING
│
├── KEY WORD
│      └── SUBSTRING
│
├── SUBSTRING
│      ↓
│   CONTIGUOUS
│
├── QUESTION
│      │
│      └── Longest VALID window
│
├── VALID CONDITION
│      │
│      └── No character appears twice
│
├── PATTERN
│      └── SLIDING WINDOW
│
├── POINTERS
│
│      left
│       ↓
│      [ valid window ]
│                    ↑
│                   right
│
├── RIGHT POINTER
│      │
│      └── Expand window
│
├── DUPLICATE
│      │
│      └── Window becomes invalid
│
├── LEFT POINTER
│      │
│      └── Shrink window
│          until valid again
│
├── DATA STRUCTURE
│      │
│      ├── frequency array
│      ├── HashMap
│      └── HashSet
│
├── CORE PATTERN
│
│      expand
│         ↓
│      violation?
│         ↓
│      shrink
│         ↓
│      valid
│         ↓
│      update answer
│
├── CONNECTION
│      │
│      ├── String compression
│      ├── Character frequency
│      ├── Longest window
│      ├── At most K distinct
│      └── Minimum window
│
└── COMPLEXITY
       O(n)
       O(charset)


## MASTER SLIDING WINDOW TEMPLATE

WINDOW
│
├── right++
│
├── Add new element
│
├── Check condition
│
├── If invalid
│      │
│      └── left++
│          remove elements
│
├── When valid
│      │
│      └── update answer
│
└── Continue


## RECOGNITION

"Longest contiguous section satisfying a condition"

                 ↓

          SLIDING WINDOW

---

# 23. GROUP ANAGRAMS

## CONNECTION FROM SET 1

GROUP ANAGRAMS
│
├── CORE QUESTION
│      │
│      └── When are two strings
│          equivalent?
│
├── ANAGRAM
│      │
│      └── Same character
│          frequencies
│
├── PATTERN
│      └── HASHING BY SIGNATURE
│
├── SIGNATURE OPTION
│      │
│      ├── Sorted string
│      └── Frequency vector
│
├── MENTAL MODEL
│
│      word
│       ↓
│      signature
│       ↓
│      HashMap
│       ↓
│      group
│
├── CONNECTION
│      │
│      ├── Pangram
│      ├── Character frequency
│      ├── Duplicate detection
│      └── HashMap
│
├── BIGGER IDEA
│      │
│      └── Canonical representation
│
│          Different objects
│                 ↓
│          same canonical form
│                 ↓
│             same group
│
└── COMPLEXITY
       Sorting signature:
       O(N × K log K)

       Frequency signature:
       O(N × K)


## MEMORY TRIGGER

ANAGRAM
   ↓
Same letters
   ↓
Same frequency
   ↓
Same signature
   ↓
HASHMAP

---

# 24. TWO SUM / TWO SUM VARIATIONS

## SOURCE CONNECTION

Two Sum and variations are explicitly included in the IBM DSA bank, and the OA question asks to check whether a pair with a given sum exists. 

---

TWO SUM
│
├── QUESTION
│      └── Find pair satisfying target
│
├── EQUATION
│
│      x + y = target
│
├── REARRANGE
│
│      y = target - x
│
├── PATTERN
│      └── COMPLEMENT
│
├── UNSORTED
│      │
│      └── HashSet / HashMap
│
├── SORTED
│      │
│      └── Two pointers
│
├── CONNECTION
│      │
│      ├── Three Sum
│      ├── Four Sum
│      ├── Pair divisible by K
│      └── Frequency problems
│
├── STORY CLUES
│      │
│      ├── pair
│      ├── target
│      ├── sum
│      └── two values
│
└── COMPLEXITY
       Hashing:
       O(n)

       Sorted two-pointer:
       O(n)
       after sorting: O(n log n)


## MASTER CONNECTION

PAIR
 ↓
TARGET
 ↓
COMPLEMENT
 ↓
target - current
 ↓
LOOK UP


If unsorted:

LOOK UP
 ↓
HASHMAP / SET

If sorted:

LOOK UP
 ↓
TWO POINTERS

---

# 25. COUNT VOWELS IN STRING

## SOURCE CONNECTION

The IBM DSA bank explicitly includes "Count vowels in string." :contentReference[oaicite:4]{index=4}

---

COUNT VOWELS
│
├── STORY
│      └── Count characters satisfying
│          a particular category
│
├── QUESTION
│      └── Is current character
│          a vowel?
│
├── PATTERN
│      └── SIMPLE TRAVERSAL
│             +
│          CATEGORY CHECK
│
├── MENTAL MODEL
│
│      for each character
│             ↓
│      classify character
│             ↓
│      vowel?
│             ↓
│      count++
│
├── OPTIONS
│      │
│      ├── if conditions
│      ├── switch
│      └── set/string lookup
│
├── CONNECTION
│      │
│      ├── Pangram
│      ├── Character frequency
│      ├── String parsing
│      └── Classification problems
│
├── STORY CLUES
│      │
│      ├── count characters
│      ├── vowels
│      ├── consonants
│      └── categories
│
└── COMPLEXITY
       O(n)
       O(1)


## MENTAL TRIGGER

"Count characters satisfying X"

              ↓

          TRAVERSE
              ↓
           CHECK
              ↓
           COUNT

Don't overcomplicate simple IBM questions.

---

# 26. ARRAY FREQUENCY / DUPLICATE DETECTION

## SOURCE CONNECTION

The OA explicitly reports "Print all duplicates in an array." :contentReference[oaicite:5]{index=5}

---

DUPLICATE / FREQUENCY
│
├── CORE QUESTION
│      │
│      └── Have I seen this value?
│
├── PATTERN
│      └── HASHING
│
├── IF ASKED
│
│      "Does it exist?"
│           ↓
│        HashSet
│
│      "How many?"
│           ↓
│        HashMap
│
│      "Which repeats?"
│           ↓
│        Frequency
│
├── IF VALUES ARE SMALL
│      │
│      └── Frequency array
│
├── IF VALUES ARE ARBITRARY
│      │
│      └── HashMap / HashSet
│
├── CONNECTION
│      │
│      ├── Pangram
│      ├── Anagram
│      ├── Two Sum
│      ├── Group Anagrams
│      └── Prefix remainder counting
│
└── CORE QUESTION

"Have I seen this before?"
             ↓
        SET / MAP


---

# 27. COMMON ELEMENTS IN THREE SORTED ARRAYS

## SOURCE CONNECTION

The Technical Interview section explicitly includes:

> Find common elements in three sorted arrays. :contentReference[oaicite:6]{index=6}

---

COMMON ELEMENTS
│
├── KEY WORD
│      └── SORTED
│
├── ARRAYS
│      A
│      B
│      C
│
├── POINTERS
│      i → A
│      j → B
│      k → C
│
├── QUESTION
│      │
│      └── Which pointer moves?
│
├── RULE
│      │
│      └── Move smallest value
│
├── WHY?
│      │
│      └── The smallest value
│          cannot match a larger
│          value until it moves forward
│
├── PATTERN
│      └── MULTIPLE POINTER
│
├── CONNECTION
│      │
│      ├── Two Sum sorted
│      ├── Three Sum
│      ├── Array intersection
│      └── Merge sorted arrays
│
└── COMPLEXITY
       O(n + m + p)


## MEMORY TRIGGER

SORTED
   +
COMMON
   ↓
MULTIPLE POINTERS

---

# 28. CONTAINER WITH MOST WATER

## SOURCE CONNECTION

The IBM DSA bank explicitly includes Container With Most Water. :contentReference[oaicite:7]{index=7}

---

CONTAINER WITH MOST WATER
│
├── STORY
│      └── Vertical lines
│          form containers
│
├── AREA
│
│      width × minimum height
│
│      area =
│      (right-left)
│      ×
│      min(height[left], height[right])
│
├── NAIVE
│      │
│      └── Try every pair
│          O(n²)
│
├── PATTERN
│      └── TWO POINTERS
│
├── START
│      │
│      ├── left = 0
│      └── right = n-1
│
├── CORE QUESTION
│      │
│      └── Which pointer should move?
│
├── RULE
│      │
│      └── Move the SHORTER side
│
├── WHY?
│      │
│      └── Area is limited by
│          the shorter height.
│
│          Moving the taller side
│          cannot increase the limiting
│          height while width decreases.
│
├── CONNECTION
│      │
│      ├── Two pointers
│      ├── Opposite-end traversal
│      ├── Greedy reasoning
│      └── Three Sum
│
├── STORY CLUES
│      │
│      ├── maximize area
│      ├── two boundaries
│      └── height/width
│
└── COMPLEXITY
       O(n)
       O(1)


## CRITICAL MEMORY RULE

TWO POINTERS
      ↓
Which pointer can be proven useless?
      ↓
Move that pointer

For Container:

SHORTER SIDE
      ↓
MOVE IT

---

# 29. THREE SUM

## SOURCE CONNECTION

The IBM DSA bank explicitly includes Three Sum. :contentReference[oaicite:8]{index=8}

---

THREE SUM
│
├── STORY
│      └── Find triplets satisfying
│          a + b + c = target
│
├── FIRST THOUGHT
│      │
│      └── Three nested loops?
│
├── OPTIMIZATION
│      │
│      └── Sort first
│
├── AFTER SORTING
│
│      Fix i
│       ↓
│      solve remaining
│      TWO SUM
│
├── PATTERN
│      └── SORT + TWO POINTERS
│
├── MENTAL MODEL
│
│      i
│      ↓
│      [ fixed ]
│
│            L →       ← R
│
├── EQUATION
│
│      nums[i]
│      + nums[L]
│      + nums[R]
│
├── DECISION
│      │
│      ├── sum < target
│      │      ↓
│      │    L++
│      │
│      ├── sum > target
│      │      ↓
│      │    R--
│      │
│      └── sum == target
│             ↓
│          record
│
├── CONNECTION
│      │
│      ├── Two Sum
│      ├── Container
│      ├── Sorted arrays
│      ├── Two pointers
│      └── Four Sum
│
├── STORY CLUES
│      │
│      ├── triplet
│      ├── target sum
│      └── combinations
│
└── COMPLEXITY
       O(n²) after sorting


## BIG CONNECTION

TWO SUM
   ↓
PAIR

THREE SUM
   ↓
Fix one
   ↓
Two Sum on remainder

FOUR SUM
   ↓
Fix two
   ↓
Two Sum on remainder


---

# SET 2 — THE MOST IMPORTANT CONNECTIONS

HASHING
│
├── Pangram
│
├── Duplicates
│
├── Anagrams
│
├── Group Anagrams
│
├── Two Sum
│
└── Prefix Sum counting


PREFIX SUM
│
├── Subarray Sum = K
│
└── Subarray Sum divisible by K


MODULO
│
├── Triplets divisible by K
│
└── Subarrays divisible by K


SLIDING WINDOW
│
└── Longest Substring
       │
       └── More window problems later


TWO POINTERS
│
├── Two Sum when sorted
├── Remove duplicates
├── Common elements
├── Container
└── Three Sum


---

# SET 2 — STORY DECODING CHEAT SHEET

STORY
│
├── "How many times?"
│       ↓
│    FREQUENCY
│
├── "Have I seen this?"
│       ↓
│    SET
│
├── "Pair + target"
│       ↓
│    COMPLEMENT
│       ↓
│    HASHMAP / TWO POINTER
│
├── "Triplet + target"
│       ↓
│    SORT + TWO POINTER
│
├── "Subarray + exact sum"
│       ↓
│    PREFIX SUM + MAP
│
├── "Subarray + divisible by K"
│       ↓
│    PREFIX REMAINDER + MAP
│
├── "Triplet + divisible by K"
│       ↓
│    REMAINDER FREQUENCY
│
├── "Longest substring"
│       ↓
│    SLIDING WINDOW
│
├── "No repeated characters"
│       ↓
│    WINDOW + FREQUENCY
│
├── "Anagrams"
│       ↓
│    FREQUENCY SIGNATURE
│
├── "Sorted + common"
│       ↓
│    MULTIPLE POINTERS
│
├── "Maximize container"
│       ↓
│    TWO POINTERS
│
└── "Count characters of category"
        ↓
     TRAVERSAL + CONDITION


---

# SET 2 — MOST IMPORTANT DIFFERENCES

## HASHMAP vs SLIDING WINDOW

HASHMAP
│
└── Usually asks about
       relationships between
       elements / previous states

Examples:
├── Two Sum
├── Frequency
├── Anagrams
└── Prefix Sum

SLIDING WINDOW
│
└── Usually maintains
       a CONTIGUOUS range

Examples:
├── Longest Substring
├── Minimum Window
└── At Most K Distinct


---

# PREFIX SUM vs SLIDING WINDOW

PREFIX SUM
│
├── Subarray
├── Sum
├── Exact target
├── Divisibility
└── Negative numbers may exist

SLIDING WINDOW
│
├── Contiguous
├── Maintain valid window
├── Expand / shrink
└── Usually relies on a condition
    that allows safe shrinking


---

# TWO POINTERS vs HASHING

PAIR + TARGET

UNSORTED
   ↓
HASHMAP

SORTED
   ↓
TWO POINTERS

So before coding ask:

> Is the array sorted?

---

# TWO SUM → THREE SUM CONNECTION

TWO SUM
│
└── Find two values
       ↓
    target

THREE SUM
│
├── Fix one value
│
└── Remaining problem
       ↓
     TWO SUM


---

# SUBARRAY SUM CONNECTION

SUBARRAY SUM = K
│
└── Prefix Sum
       │
       └── currentPrefix - K
               ↓
            lookup

SUBARRAY SUM DIVISIBLE BY K
│
└── Prefix Sum
       │
       └── remainder
              ↓
        same remainder


---

# SET 2 — CHECKLIST

SET 2 — HASHING + PREFIX SUM + SLIDING WINDOW
│
├── [ ] 19. Subarray Sum Equals K
├── [ ] 20. Count Subarrays Whose Sum Is Divisible by K
├── [ ] 21. Count Triplets Whose Sum Is Divisible by K
├── [ ] 22. Longest Substring Without Repeating Characters
├── [ ] 23. Group Anagrams
├── [ ] 24. Two Sum / Two Sum Variations
├── [ ] 25. Count Vowels in String
├── [ ] 26. Array Frequency / Duplicate Detection
├── [ ] 27. Common Elements in Three Sorted Arrays
├── [ ] 28. Container With Most Water
└── [ ] 29. Three Sum


---

# SET 2 — PATTERN CHECKLIST

Before considering Set 2 complete, you should be able to answer these immediately:

├── [ ] "Have I seen this before?"
│        → Set / HashMap
│
├── [ ] "How many times?"
│        → Frequency
│
├── [ ] "Pair + target?"
│        → Complement
│
├── [ ] "Sorted pair?"
│        → Two pointers
│
├── [ ] "Triplet + target?"
│        → Sort + Two pointers
│
├── [ ] "Subarray + exact sum?"
│        → Prefix Sum + HashMap
│
├── [ ] "Subarray + divisible by K?"
│        → Prefix remainder + HashMap
│
├── [ ] "Longest contiguous valid substring?"
│        → Sliding Window
│
├── [ ] "Anagram?"
│        → Frequency signature
│
├── [ ] "Sorted arrays + common?"
│        → Multiple pointers
│
└── [ ] "Container maximum?"
         → Two pointers


---

# SET 2 — CONNECTION TO SET 1

SET 1
│
├── Pangram
│      ↓
│   Character presence
│      ↓
│   HASHING / FREQUENCY
│
├── Group Anagrams
│      ↓
│   Character frequency
│      ↓
│   HASHMAP
│
├── Two Sum
│      ↓
│   Complement
│      ↓
│   HASHMAP
│
├── Longest Substring
│      ↓
│   Sliding Window
│      ↓
│   SET 2
│
├── Remove Duplicates
│      ↓
│   Two Pointers
│      ↓
│   SET 2
│
└── Common Elements
       ↓
    Multiple Pointers
       ↓
    SET 2


---

# SET 2 — CONNECTION TO FUTURE SETS

SET 2
│
├── Prefix Sum
│      │
│      └──────────────→ Advanced Array Problems
│
├── Sliding Window
│      │
│      └──────────────→ More String / Array Problems
│
├── HashMap
│      │
│      ├──────────────→ Graph / Frequency Problems
│      └──────────────→ DP State Optimization
│
├── Two Pointer
│      │
│      ├──────────────→ Linked List
│      └──────────────→ Greedy / Array Problems
│
└── Modulo
       │
       └──────────────→ Mathematics / Number Theory


---

# SET 2 — FINAL MEMORY TREE

IBM STORY
│
├── COUNT / SEEN
│      ↓
│    HASHING
│
├── PAIR + TARGET
│      ↓
│    COMPLEMENT
│      ↓
│    HASHMAP
│
├── SORTED + PAIR
│      ↓
│    TWO POINTERS
│
├── TRIPLET + TARGET
│      ↓
│    SORT
│      ↓
│    TWO POINTERS
│
├── SUBARRAY + SUM
│      ↓
│    PREFIX SUM
│
├── PREFIX SUM + COUNT
│      ↓
│    HASHMAP
│
├── DIVISIBLE BY K
│      ↓
│    REMAINDER
│
├── LONGEST + SUBSTRING
│      ↓
│    SLIDING WINDOW
│
├── ANAGRAM
│      ↓
│    FREQUENCY SIGNATURE
│
├── SORTED + COMMON
│      ↓
│    MULTIPLE POINTERS
│
└── MAXIMUM CONTAINER
       ↓
    TWO POINTERS


---

# SET 2 — READINESS CHECK

After Set 2, the goal is NOT merely:

> "I solved 11 more problems."

The goal is:

```text
IBM STORY
    ↓
Identify keywords
    ↓
Ask what mathematical/data relationship exists
    ↓
Recognize pattern
    ↓
Recall connected problems
    ↓
Derive algorithm
