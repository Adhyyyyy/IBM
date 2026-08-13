# IBM OA — MASTER PATTERN NOTEBOOK
# SET 4 — GREEDY + HEAP / PRIORITY QUEUE

## SOURCE BASIS

The IBM PYQ resource explicitly lists the following under **Heaps & Priority Queues**:

- Max heap operations (2025)
- Kth largest element
- Merge K sorted lists
- Top K frequent elements
- Find median from data stream
- Task scheduler problem

It also reports the exact 2025 OA question:

> "Perform operations on a Max Heap (insert, delete, heapify)"

and a 2025 OA question:

> "Design a greedy algorithm to optimize a resource allocation problem." :contentReference[oaicite:0]{index=0} :contentReference[oaicite:1]{index=1}

The resource therefore gives us **direct OA evidence for Max Heap and Greedy**, while the other Heap/Priority Queue problems are part of the broader question bank. :contentReference[oaicite:2]{index=2}


---

# SET 4 — BIG PICTURE

SET 4
│
├── GREEDY
│      │
│      ├── Local best choice
│      ├── Resource allocation
│      ├── Scheduling
│      └── Optimization
│
├── HEAP
│      │
│      ├── Min Heap
│      ├── Max Heap
│      ├── Insert
│      ├── Delete
│      └── Heapify
│
├── PRIORITY QUEUE
│      │
│      ├── Always access highest/lowest priority
│      ├── Kth largest
│      ├── Top K
│      ├── Median
│      └── Scheduling
│
└── HEAP + GREEDY
       │
       ├── Task scheduling
       ├── Resource allocation
       └── Repeated best-choice problems


---

# SET 4 — MASTER MENTAL MAP

GREEDY
│
├── "Choose the best now"
│       ↓
│    GREEDY
│
├── "Maximum benefit"
│       ↓
│    choose best available
│
├── "Minimum cost"
│       ↓
│    choose cheapest available
│
├── "Schedule"
│       ↓
│    often sort by a useful criterion
│
└── "Resource allocation"
        ↓
     repeatedly make
     the best feasible choice


HEAP
│
├── "Need maximum quickly"
│       ↓
│    MAX HEAP
│
├── "Need minimum quickly"
│       ↓
│    MIN HEAP
│
├── "Need best element repeatedly"
│       ↓
│    PRIORITY QUEUE
│
├── "Top K"
│       ↓
│    HEAP
│
├── "Kth largest"
│       ↓
│    MIN HEAP of size K
│
├── "Kth smallest"
│       ↓
│    MAX HEAP of size K
│
├── "Many sorted lists"
│       ↓
│    MIN HEAP
│
├── "Repeated scheduling"
│       ↓
│    PRIORITY QUEUE
│
└── "Running median"
        ↓
     TWO HEAPS


---

# FIRST: WHAT IS A HEAP?

Before solving the problems, understand the data structure.

A HEAP is a tree-based structure that maintains a special ordering.

For a:

MAX HEAP

every parent is:

>= its children

Example:

              50
             /  \
           30    40
          / \    / \
        10 20  35 25


The largest value is always at:

ROOT


For a:

MIN HEAP

every parent is:

<= its children

Example:

              10
             /  \
           20    15
          / \    / \
        30 25  40 35


The smallest value is always at:

ROOT


---

# HEAP — IMPORTANT DISTINCTION

A heap is NOT fully sorted.

MAX HEAP:

          50
         /  \
       30    40

30 and 40 have no required ordering relative to each other.

The only guarantee is:

parent >= children


Therefore:

HEAP
   ↓
Only partial ordering

NOT:

FULL SORTING


This distinction is very important.


---

# HEAP AS AN ARRAY

A binary heap is commonly stored in an array.

Example:

Tree:

              50
             /  \
           30    40
          / \    / \
        10 20  35 25


Array:

[50, 30, 40, 10, 20, 35, 25]


For a node at index i:

LEFT CHILD:

2*i + 1


RIGHT CHILD:

2*i + 2


PARENT:

(i - 1) / 2


This is the basic structure behind `priority_queue`.


---

# C++ PRIORITY QUEUE

MAX HEAP:

priority_queue<int> pq;


By default:

largest element
      ↓
    top()


Example:

pq.push(10)
pq.push(50)
pq.push(30)


          50
         /  \
       10    30


pq.top()
   ↓
  50


MIN HEAP:

priority_queue<int,
               vector<int>,
               greater<int>> pq;


Now:

smallest element
      ↓
    top()


---

# 43. MAX HEAP OPERATIONS

## SOURCE CONNECTION

This is an exact 2025 IBM OA question:

> "Perform operations on a Max Heap (insert, delete, heapify)." :contentReference[oaicite:3]{index=3}

---

MAX HEAP OPERATIONS
│
├── INSERT
│      ↓
│   Add at end
│      ↓
│   Bubble Up
│
├── DELETE
│      ↓
│   Usually remove root
│      ↓
│   Move last element to root
│      ↓
│   Bubble Down
│
└── HEAPIFY
       ↓
    Restore heap property


---

# MAX HEAP INSERT

Suppose:

              50
             /  \
           30    40
          /
        10


Insert:

45


FIRST:

Put it at the next available position.

              50
             /  \
           30    40
          / \
        10  45


Now:

45 > 30

So:

swap.


              50
             /  \
           45    40
          / \
        10  30


Now:

45 < 50

STOP.


---

# INSERT MENTAL MODEL

INSERT
│
├── Put new element
│      │
│      └── LAST position
│
├── Compare with parent
│
├── If child > parent
│      ↓
│    swap
│
├── Move upward
│
└── Stop when heap property restored


PATTERN:

INSERT
   ↓
BUBBLE UP
   ↓
COMPARE WITH PARENT


---

# MAX HEAP DELETE

Usually when a problem says delete from a max heap, the important operation is deleting the root.

Example:

              50
             /  \
           40    30
          / \
        10  20


Delete 50.

Do NOT simply leave the root empty.

Instead:

Move last element to root.

              20
             /  \
           40    30
          /
        10


Now heap property is broken:

20 < 40

Therefore:

BUBBLE DOWN.


Swap 20 and 40:

              40
             /  \
           20    30
          /
        10


Now valid.


---

# DELETE MENTAL MODEL

DELETE ROOT
│
├── Replace root with last element
│
├── Remove last element
│
└── Bubble Down
       │
       └── swap with appropriate child


For MAX HEAP:

swap with larger child.


For MIN HEAP:

swap with smaller child.


---

# HEAPIFY

HEAPIFY means:

> Restore heap property.

There are two directions:

BUBBLE UP
│
└── Usually after INSERT


BUBBLE DOWN
│
└── Usually after DELETE / building heap


---

# BUILDING A HEAP

Suppose:

[10, 40, 20, 5, 30]


We want a MAX HEAP.

Instead of repeatedly inserting every element, we can heapify from the last non-leaf node toward the root.

Important idea:

LEAF
│
└── already satisfies heap property
       because it has no children.


Therefore:

Start from:

last non-leaf node

and move toward index 0.


---

# HEAP COMPLEXITY

Operation:

INSERT
    ↓
O(log n)


DELETE ROOT
    ↓
O(log n)


TOP
    ↓
O(1)


BUILD HEAP
    ↓
O(n)


This is important.

A common mistake is assuming:

Build heap = O(n log n)

The standard bottom-up heap construction is:

O(n).


---

# CONNECTION

MAX HEAP
│
├── Need largest repeatedly
│       ↓
│    root
│
└── Need dynamic largest
        ↓
     priority_queue


MIN HEAP
│
├── Need smallest repeatedly
│       ↓
│    root
│
└── Need dynamic smallest
        ↓
     priority_queue


---

# 44. KTH LARGEST ELEMENT

## SOURCE CONNECTION

Listed under Heaps & Priority Queues in the IBM question bank. :contentReference[oaicite:4]{index=4}

---

KTH LARGEST
│
├── STORY
│      └── Find kth largest
│
├── FIRST THOUGHT
│      │
│      └── Sort
│
├── SORTING
│      │
│      └── O(n log n)
│
├── HEAP APPROACH
│      │
│      └── Keep only K useful elements
│
├── QUESTION
│      │
│      └── What kind of heap?
│
├── ANSWER
│      └── MIN HEAP
│             of size K
│
├── WHY?
│      │
│      └── The smallest among
│          our current top K
│          tells us what can be removed.
│
├── PROCESS
│
│      Traverse elements
│           ↓
│      push into min heap
│           ↓
│      if size > K
│           ↓
│      pop smallest
│
└── FINAL
       heap.top()
       =
       Kth largest


---

# VISUAL EXAMPLE

Array:

[3, 2, 1, 5, 6, 4]

Find:

2nd largest


K = 2


Maintain:

MIN HEAP size 2


Process:

3

heap:
[3]


2

heap:
[2,3]


1

push:

[1,2,3]

size > 2

pop 1

[2,3]


5

[2,3,5]

pop 2

[3,5]


6

[3,5,6]

pop 3

[5,6]


4

[4,5,6]

pop 4

[5,6]


Top:

5


Answer:

5


---

# WHY MIN HEAP?

This is the key intuition.

We want:

TOP K LARGEST


Imagine keeping:

[largest, second largest, ...]

We need to throw away anything that cannot belong to the final top K.

The weakest member of our top-K group is:

SMALLEST


Therefore:

MIN HEAP


---

# MASTER RULE

KTH LARGEST
      ↓
MIN HEAP
      ↓
SIZE K


KTH SMALLEST
      ↓
MAX HEAP
      ↓
SIZE K


This is one of the most important Heap patterns.


---

# 45. TOP K FREQUENT ELEMENTS

## SOURCE CONNECTION

Listed in the Heap/Priority Queue question bank. :contentReference[oaicite:5]{index=5}

---

TOP K FREQUENT
│
├── STORY
│      └── Find K most frequent values
│
├── FIRST PROBLEM
│      │
│      └── Need frequency
│
├── STEP 1
│      │
│      └── HashMap
│
│          value → frequency
│
├── STEP 2
│      │
│      └── Need top K frequencies
│
├── PATTERN
│      └── HASHMAP + HEAP
│
├── HEAP
│      └── MIN HEAP size K
│
├── WHY?
│      │
│      └── Keep only K highest frequencies
│
└── CONNECTION

FREQUENCY
    ↓
HASHMAP

TOP K
    ↓
HEAP

Therefore:

TOP K FREQUENT
    ↓
HASHMAP + MIN HEAP


---

# MENTAL STRUCTURE

"How many times?"

        ↓

FREQUENCY MAP


"Which K are largest?"

        ↓

TOP K


"Top K dynamically?"

        ↓

MIN HEAP size K


---

# IMPORTANT CONNECTION TO SET 2

SET 2:

COUNT / FREQUENCY
      ↓
HASHMAP


SET 4:

TOP K FREQUENT
      ↓
HASHMAP
      +
HEAP


So we are not learning a completely new problem.

We are combining old patterns.


---

# 46. MERGE K SORTED LISTS

## SOURCE CONNECTION

Listed in the Heap/Priority Queue bank. :contentReference[oaicite:6]{index=6}

---

MERGE K SORTED LISTS
│
├── STORY
│      └── Multiple sorted lists
│
├── PREVIOUS KNOWLEDGE
│      │
│      └── Merge TWO sorted lists
│
├── PROBLEM
│      │
│      └── What changes when
│          there are K lists?
│
├── KEY OBSERVATION
│      │
│      └── At any moment,
│          we only care about
│          the smallest current node
│          from each list.
│
├── DATA STRUCTURE
│      └── MIN HEAP
│
├── HEAP CONTENT
│      │
│      └── Current smallest node
│          from every non-empty list
│
├── PROCESS
│
│      Put first node of each list
│           ↓
│      pop smallest
│           ↓
│      add to answer
│           ↓
│      insert its next node
│           ↓
│      repeat
│
└── PATTERN
       K-WAY MERGE
          +
       MIN HEAP


---

# VISUAL

List 1:

1 → 4 → 7


List 2:

2 → 5 → 8


List 3:

3 → 6 → 9


Heap initially:

[1,2,3]


Pop:

1

Insert:

4

Heap:

[2,3,4]


Pop:

2

Insert:

5

Heap:

[3,4,5]


Continue...


Result:

1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → 9


---

# CONNECTION

MERGE TWO SORTED LISTS
        ↓
Compare two fronts


MERGE K SORTED LISTS
        ↓
Need smallest among K fronts
        ↓
MIN HEAP


This is a very important generalization.


---

# 47. FIND MEDIAN FROM DATA STREAM

## SOURCE CONNECTION

Listed in the Heap/Priority Queue bank. :contentReference[oaicite:7]{index=7}

---

MEDIAN FROM DATA STREAM
│
├── STORY
│      └── Numbers arrive one by one
│
├── PROBLEM
│      │
│      └── Need median after
│          every insertion
│
├── NAIVE
│      │
│      └── Keep sorting
│
├── BETTER
│      └── TWO HEAPS
│
├── LEFT HALF
│      │
│      └── MAX HEAP
│
├── RIGHT HALF
│      │
│      └── MIN HEAP
│
├── WHY?
│      │
│      ├── max of left half
│      └── min of right half
│
│      sit around the median.
│
└── PATTERN
       TWO HEAPS


---

# VISUAL

Numbers:

1 2 3 4 5


LEFT HALF:

[1,2]

MAX HEAP
top = 2


RIGHT HALF:

[3,4,5]

MIN HEAP
top = 3


Median:

3


For an even count:

LEFT:
[1,2]

RIGHT:
[3,4]

Median:

(2 + 3) / 2


---

# TWO HEAP RULE

MAX HEAP
│
└── smaller half


MIN HEAP
│
└── larger half


Maintain:

size difference <= 1


Then:

if equal sizes:

median =
(maxLeft + minRight) / 2


if left larger:

median =
maxLeft


if right larger:

median =
minRight


---

# MEMORY TRIGGER

STREAM
+
MEDIAN
    ↓
TWO HEAPS


Do NOT think:

"How do I sort every time?"

Think:

> "How can I keep the middle accessible?"


---

# 48. TASK SCHEDULER

## SOURCE CONNECTION

Listed in the Heap/Priority Queue bank. :contentReference[oaicite:8]{index=8}

---

TASK SCHEDULER
│
├── STORY
│      └── Tasks must be scheduled
│          with constraints
│
├── COMMON FORM
│      │
│      └── Same task may require
│          a cooldown period
│
├── KEY QUESTION
│      │
│      └── Which task should
│          we execute next?
│
├── IMPORTANT IDEA
│      │
│      └── Highest remaining frequency
│          is often the most urgent
│
├── DATA STRUCTURE
│      └── MAX HEAP
│
├── FREQUENCY
│      │
│      └── HashMap / frequency array
│
├── COMBINATION
│
│      frequency
│          ↓
│      MAX HEAP
│          ↓
│      choose most frequent task
│
└── PATTERN
       FREQUENCY + MAX HEAP


---

# CONNECTION

TOP K FREQUENT:

frequency
    +
min heap


TASK SCHEDULER:

frequency
    +
max heap


The difference is:

What are we trying to select?


TOP K:
keep strongest K


SCHEDULER:
execute most urgent/high-frequency task


---

# 49. GREEDY RESOURCE ALLOCATION

## SOURCE CONNECTION

The resource explicitly reports this as a 2025 OA question:

> "Design a greedy algorithm to optimize a resource allocation problem." :contentReference[oaicite:9]{index=9}

Important limitation:

The source gives the **question category**, but does not provide enough detail to identify the exact underlying resource-allocation variant.

Therefore, we should NOT pretend the PDF specifies one exact algorithm.

What we can safely learn is the GREEDY pattern.

---

# WHAT IS GREEDY?

GREEDY
│
├── Make a choice
│      ↓
│   that looks best NOW
│
├── Commit to the choice
│
└── Continue


The key question:

> Can I make the locally best choice without destroying the possibility of an optimal final answer?


---

# GREEDY MENTAL MODEL

PROBLEM
   ↓
Many possible choices
   ↓
Find the best feasible choice NOW
   ↓
Take it
   ↓
Reduce problem
   ↓
Repeat


---

# EXAMPLE MENTAL MODEL

Suppose resources must be allocated to requests.

Each request has:

benefit

and maybe:

cost


Possible greedy rule:

choose the feasible request
with the highest benefit


But:

IMPORTANT

Greedy is NOT:

> "Always choose the largest number."

It is:

> "Choose according to a proven useful local criterion."


---

# GREEDY STORY CLUES

Look for:

├── maximize
├── minimize
├── schedule
├── allocate
├── choose
├── repeatedly select
├── best available
├── minimum cost
├── maximum benefit
└── limited resources


These words should make you ASK:

> Is there a greedy ordering or local choice?


---

# GREEDY vs DP

This distinction is extremely important.

GREEDY
│
└── Make one local decision
       ↓
    never reconsider


DP
│
├── Explore possible states
├── Store results
└── compare alternatives


Example mental question:

"Can I safely commit to this choice?"

YES
 ↓
Maybe GREEDY

NO
 ↓
May need DP / search / other method


---

# GREEDY vs HEAP

These are NOT the same thing.

GREEDY
    ↓
Algorithmic strategy

HEAP
    ↓
Data structure


But they can work together.

Example:

GREEDY
│
└── Always choose highest-priority
       available task
              ↓
           MAX HEAP


Therefore:

GREEDY
+
HEAP
=
Efficient repeated best-choice selection


---

# SET 4 — MASTER CONNECTIONS

## CONNECTION 1

KTH LARGEST

"Keep top K"
    ↓
MIN HEAP
    ↓
size K


TOP K FREQUENT

"Keep top K frequencies"
    ↓
MIN HEAP
    ↓
size K


Same pattern.


---

# CONNECTION 2

MERGE TWO SORTED LISTS

2 lists
    ↓
compare two fronts


MERGE K SORTED LISTS

K lists
    ↓
need smallest among K fronts
    ↓
MIN HEAP


Same idea generalized.


---

# CONNECTION 3

TASK SCHEDULER

Need most frequent/urgent task
    ↓
MAX HEAP


TOP K

Need top K
    ↓
MIN HEAP size K


The heap direction depends on what must remain accessible.


---

# CONNECTION 4

MEDIAN

Need middle
    ↓
Split into two halves
    ↓
MAX HEAP + MIN HEAP


This is an important extension of the heap idea.


---

# CONNECTION 5

SET 2 → SET 4

SET 2
│
├── HashMap
├── Frequency
└── Two Pointer


SET 4
│
├── HashMap
│      +
│    Heap
│
├── Frequency
│      +
│    Heap
│
└── Sorted structures
       +
       Heap


So:

SET 4 is not isolated.

It combines previous patterns with a new data structure.


---

# SET 4 — STORY DECODING CHEAT SHEET

STORY
│
├── "Largest repeatedly"
│      ↓
│    MAX HEAP
│
├── "Smallest repeatedly"
│      ↓
│    MIN HEAP
│
├── "Top K largest"
│      ↓
│    MIN HEAP size K
│
├── "Top K smallest"
│      ↓
│    MAX HEAP size K
│
├── "Top K frequent"
│      ↓
│    FREQUENCY + MIN HEAP
│
├── "Merge K sorted"
│      ↓
│    MIN HEAP
│
├── "Median from stream"
│      ↓
│    TWO HEAPS
│
├── "Most frequent task"
│      ↓
│    FREQUENCY + MAX HEAP
│
├── "Repeated best choice"
│      ↓
│    GREEDY
│
└── "Repeated best choice efficiently"
       ↓
    GREEDY + HEAP


---

# SET 4 — HEAP DIRECTION CHEAT SHEET

QUESTION
│
├── Need MAX immediately
│      ↓
│    MAX HEAP
│
├── Need MIN immediately
│      ↓
│    MIN HEAP
│
├── KTH LARGEST
│      ↓
│    MIN HEAP size K
│
├── KTH SMALLEST
│      ↓
│    MAX HEAP size K
│
├── TOP K LARGEST
│      ↓
│    MIN HEAP size K
│
├── TOP K SMALLEST
│      ↓
│    MAX HEAP size K
│
├── K SORTED LISTS
│      ↓
│    MIN HEAP
│
└── MEDIAN
       ↓
    MAX HEAP + MIN HEAP


---

# WHY KTH LARGEST USES MIN HEAP

This deserves permanent memory.

We want:

K largest elements.

Suppose:

K = 3

Current candidates:

[100, 90, 80]

Which candidate is least useful?

80.

So we want the smallest candidate at the top.

Therefore:

MIN HEAP.


Whenever a new number arrives:

if it is larger than the smallest candidate,

remove the smallest and keep the new number.


Hence:

MIN HEAP
+
SIZE K


---

# SET 4 — PRIORITY QUEUE MENTAL MODEL

A normal queue:

FIRST IN
   ↓
FIRST OUT


A priority queue:

HIGHEST PRIORITY
      ↓
    FIRST


Therefore:

priority_queue
      ↓
"Give me the most important element."


MAX HEAP:

most important =
largest


MIN HEAP:

most important =
smallest


The priority is defined by the problem.


---

# SET 4 — COMPLEXITY CHEAT SHEET

HEAP OPERATION
│
├── top
│      ↓
│    O(1)
│
├── push
│      ↓
│    O(log n)
│
├── pop
│      ↓
│    O(log n)
│
└── build heap
       ↓
     O(n)


KTH LARGEST:

O(n log K)


TOP K:

O(n log K)


K-WAY MERGE:

O(N log K)

where:

N = total number of elements


MEDIAN STREAM:

O(log n) per insertion


---

# SET 4 — CHECKLIST

SET 4 — GREEDY + HEAP
│
├── MUST MASTER — DIRECT OA
│      │
│      ├── [ ] 42. Max Heap Insert
│      ├── [ ] 43. Max Heap Delete
│      ├── [ ] 44. Max Heapify
│      └── [ ] 45. Greedy Resource Allocation
│
├── HIGH VALUE HEAP PATTERNS
│      │
│      ├── [ ] 46. Kth Largest Element
│      ├── [ ] 47. Top K Frequent Elements
│      ├── [ ] 48. Merge K Sorted Lists
│      ├── [ ] 49. Median From Data Stream
│      └── [ ] 50. Task Scheduler
│
└── FOUNDATION
       │
       ├── [ ] Max Heap
       ├── [ ] Min Heap
       ├── [ ] Priority Queue
       └── [ ] Heapify


---

# PRIORITY ORDER FOR IBM

## TIER 1 — DO FIRST

├── [ ] Max Heap operations
│      │
│      ├── Insert
│      ├── Delete
│      └── Heapify
│
└── [ ] Greedy resource allocation


Why?

Because both are explicitly reported as **2025 OA questions**. :contentReference[oaicite:10]{index=10}


---

# TIER 2 — HIGH ROI

├── [ ] Kth Largest
├── [ ] Top K Frequent
└── [ ] Merge K Sorted Lists


These teach the central Priority Queue patterns.


---

# TIER 3 — ADVANCED

├── [ ] Median From Data Stream
└── [ ] Task Scheduler


These are valuable because they combine multiple concepts.


---

# SET 4 — IMPORTANT CONNECTION TO IBM OA

The source's exact 2025 questions include:

GREEDY RESOURCE ALLOCATION
        +
MAX HEAP OPERATIONS

This is significant for preparation because the current set directly covers both of those source-reported OA categories. :contentReference[oaicite:11]{index=11}


---

# SET 4 — MASTER MEMORY TREE

HEAP
│
├── MAX HEAP
│      │
│      ├── largest at top
│      ├── insert → bubble up
│      └── delete → bubble down
│
├── MIN HEAP
│      │
│      ├── smallest at top
│      └── useful for top-K largest
│
├── TOP K
│      │
│      ├── K largest
│      │      ↓
│      │   MIN HEAP size K
│      │
│      └── K smallest
│             ↓
│          MAX HEAP size K
│
├── FREQUENCY
│      ↓
│   HASHMAP
│      +
│   HEAP
│
├── K SORTED LISTS
│      ↓
│   MIN HEAP
│
├── MEDIAN
│      ↓
│   TWO HEAPS
│
└── SCHEDULING
       ↓
    PRIORITY QUEUE


GREEDY
│
├── Local best
├── Commit
├── Reduce problem
└── Repeat


---

# SET 4 — FINAL RECOGNITION RULES

1. **Need largest quickly → MAX HEAP.**

2. **Need smallest quickly → MIN HEAP.**

3. **Kth largest → MIN HEAP of size K.**

4. **Kth smallest → MAX HEAP of size K.**

5. **Top K largest → MIN HEAP of size K.**

6. **Top K frequent → FREQUENCY MAP + HEAP.**

7. **Merge K sorted lists → MIN HEAP of current heads.**

8. **Median from stream → TWO HEAPS.**

9. **Repeated highest-priority task → PRIORITY QUEUE / MAX HEAP.**

10. **Insert into heap → add at end + bubble up.**

11. **Delete root → replace with last + bubble down.**

12. **Heapify → restore heap property.**

13. **Build heap bottom-up → O(n).**

14. **Heap is NOT a sorted array.**

15. **Greedy is a strategy, not a data structure.**

16. **Heap is a data structure, not automatically a greedy algorithm.**

17. **Greedy + Heap is useful when we repeatedly need the best currently available choice.**

18. **The source confirms the 2025 OA had Max Heap operations and a greedy resource-allocation question; it does not specify the exact resource-allocation variant, so we should not invent one.** :contentReference[oaicite:12]{index=12}


---

# SET 4 — FINAL VISUAL CONNECTION

SET 2
│
├── HASHMAP
│      ↓
│   frequency
│
└── TWO POINTERS


SET 3
│
└── LINKED LIST POINTERS


SET 4
│
├── HEAP
│      ↓
│   priority
│
├── HASHMAP
│      +
│    HEAP
│
└── GREEDY
       ↓
    best current choice


The pattern progression is:

```text
SET 1
Basic Array / String
        ↓
SET 2
Hashing / Prefix Sum / Sliding Window
        ↓
SET 3
Pointer Manipulation / Linked List
        ↓
SET 4
Priority / Heap / Greedy
