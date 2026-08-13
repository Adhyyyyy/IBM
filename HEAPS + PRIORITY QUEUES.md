# IBM OA — MASTER PATTERN NOTEBOOK
# SET 8 — HEAPS + PRIORITY QUEUES

# SOURCE BASIS

The IBM PYQ Question Bank lists:

- Max heap operations (2025)
- Kth largest element
- Merge k sorted lists
- Top K frequent elements
- Find median from data stream
- Task scheduler problem :contentReference[oaicite:3]{index=3}


The DSA Geetha says:

HEAP / PRIORITY QUEUE
│
├── Kth largest / smallest
├── Top-K elements
├── Merge K sorted lists
└── Median stream

Keywords:

"kth"
"top k"
"median"
"k largest"
"k frequent"

Core thinking:

Min-heap of size K
        ↓
Kth largest

Max-heap of size K
        ↓
Kth smallest

Maintain:

heap size = K :contentReference[oaicite:4]{index=4}


# SET 8 — BIG PICTURE

HEAP
│
├── WHAT?
│      └── Special tree-based
│          data structure
│
├── MAIN PURPOSE
│      └── Quickly access
│          minimum / maximum
│
├── MIN HEAP
│      └── smallest at top
│
├── MAX HEAP
│      └── largest at top
│
└── PRIORITY QUEUE
       └── repeatedly process
           highest-priority item


# 97. WHAT IS A HEAP?

A heap is a:

COMPLETE BINARY TREE

with a special ordering property.


Two major types:

MIN HEAP

Parent
    ≤
Children


MAX HEAP

Parent
    ≥
Children


# MIN HEAP

Example:

             1
           /   \
          3     2
         / \   /
        7   5 4


The smallest element:

1

is at the root.


Important:

The entire tree is NOT sorted.


Only the parent-child relationship
is guaranteed.


# MAX HEAP

Example:

             9
           /   \
          7     8
         / \   /
        3   4 5


Largest:

9

is at the root.


# IMPORTANT DIFFERENCE

SORTED ARRAY

[1,2,3,4,5,6]


Every element has global ordering.


HEAP

       1
      / \
     3   2
    / \
   7   5


Only heap property is guaranteed.


Therefore:

HEAP
≠
SORTED TREE.


# 98. WHY DO WE NEED A HEAP?

Suppose:

[8, 3, 10, 2, 5, 7]


Question:

"Give me the largest element repeatedly."


A normal approach:

Sort:

[2,3,5,7,8,10]

Cost:

O(n log n)


But if we only need the current largest:

MAX HEAP


gives:

largest
 ↓
top


and after removing it:

next largest
 ↓
top


Therefore:

HEAP
 ↓
repeated best element access


# CORE HEAP IDEA

Need:

MINIMUM repeatedly
        ↓
MIN HEAP


Need:

MAXIMUM repeatedly
        ↓
MAX HEAP


This is the most important first recognition rule.


# 99. PRIORITY QUEUE

In C++:

priority_queue


Default:

MAX HEAP


Example:

priority_queue<int> pq;


Insert:

pq.push(5);
pq.push(2);
pq.push(10);


Top:

10


Because:

largest
 ↓
top


# MIN HEAP IN C++

priority_queue<
    int,
    vector<int>,
    greater<int>
> pq;


Now:

smallest
 ↓
top


Example:

push:

5
2
10


top:

2


# MEMORY

C++ DEFAULT:

priority_queue<int>
        ↓
      MAX HEAP


C++ MIN HEAP:

priority_queue<
    int,
    vector<int>,
    greater<int>
>


# 100. HEAP OPERATIONS

MAIN OPERATIONS:

push()
│
└── insert element


pop()
│
└── remove top


top()
│
└── access top


empty()
│
└── check empty


size()
│
└── number of elements


# COMPLEXITIES

push:

O(log n)


pop:

O(log n)


top:

O(1)


size:

O(1)


This is why heaps are useful when we repeatedly need the best element.


# HEAP INTERNAL STORY

INSERT

new element
    ↓
place at end
    ↓
compare with parent
    ↓
swap upward if necessary
    ↓
HEAPIFY UP


REMOVE TOP

remove root
    ↓
move last element to root
    ↓
compare with children
    ↓
swap downward
    ↓
HEAPIFY DOWN


You don't normally implement this manually in an OA if C++ priority_queue is allowed.

But you should understand what happens.


# 101. HEAP AS AN ARRAY

A complete binary tree can be stored efficiently in an array.


Example:

             10
            /  \
           7    8
          / \
         3   5


Array:

[10, 7, 8, 3, 5]


For zero-based indexing:

parent(i):

(i - 1) / 2


left child:

2*i + 1


right child:

2*i + 2


# WHY ARRAY?

Because the tree is:

COMPLETE


There are no unnecessary gaps.


Therefore:

HEAP
 ↓
COMPLETE TREE
 ↓
ARRAY


# 102. MAX HEAP OPERATIONS

## SOURCE CONNECTION

"Max heap operations" is explicitly listed as a 2025 IBM PYQ. :contentReference[oaicite:5]{index=5}


MAX HEAP
│
├── ROOT
│      ↓
│    MAXIMUM
│
├── INSERT
│      ↓
│    heapify up
│
├── DELETE MAX
│      ↓
│    heapify down
│
└── TOP
       ↓
     maximum


# EXAMPLE

Insert:

10

Heap:

[10]


Insert:

5:

[10,5]


Insert:

20:

Before fixing:

[10,5,20]


20 > parent 10

Swap:

[20,5,10]


Now:

20
 ↓
root


# MENTAL MODEL

MAX HEAP:

"largest item wants to move upward."


MIN HEAP:

"smallest item wants to move upward."


# 103. KTH LARGEST ELEMENT

## SOURCE CONNECTION

Kth Largest Element is explicitly listed in the IBM heap question bank. :contentReference[oaicite:6]{index=6}

You have already worked through the core idea in your previous heap practice: maintain a **min-heap of size K**, remove the smallest whenever the heap grows beyond K, and the final top is the kth largest. :contentReference[oaicite:7]{index=7}


# KTH LARGEST

STORY:

Find:

kth largest


Example:

[3,2,1,5,6,4]

k = 2


Sorted descending:

6,5,4,3,2,1


Answer:

5


# FIRST THOUGHT

Could sort.

O(n log n)


But:

we only need kth largest.


Therefore:

TOP-K PATTERN.


# KEY IDEA

Maintain:

MIN HEAP
of size K.


Why MIN HEAP?


Suppose:

k = 2


Heap contains:

[5,6]


The smallest among these:

5

is the:

2nd largest.


Therefore:

MIN HEAP
+
SIZE K


# PROCESS

nums:

3 2 1 5 6 4


k = 2


Insert 3:

[3]


Insert 2:

[2,3]


Size > 2?

No.


Insert 1:

[1,2,3]


Size > 2:

YES


Remove smallest:

1


Heap:

[2,3]


Insert 5:

[2,3,5]


Remove:

2


Heap:

[3,5]


Insert 6:

[3,5,6]


Remove:

3


Heap:

[5,6]


Insert 4:

[4,5,6]


Remove:

4


Final:

[5,6]


TOP:

5


Answer:

5


# MENTAL MODEL

Need:

K LARGEST


Keep:

K BEST


But among those K:

which one is the weakest?

SMALLEST.


Therefore:

MIN HEAP.


This is the core insight.


# GOLDEN RULE

KTH LARGEST
        ↓
MIN HEAP
        ↓
SIZE K
        ↓
TOP = ANSWER


KTH SMALLEST
        ↓
MAX HEAP
        ↓
SIZE K
        ↓
TOP = ANSWER


This exact mapping is given in the DSA Geetha. :contentReference[oaicite:8]{index=8}


# COMPLEXITY

For n elements:

Each heap operation:

O(log K)


We maintain heap size:

K


Total:

O(n log K)


Space:

O(K)


# IMPORTANT CORRECTION FROM YOUR EARLIER ANSWER

You previously gave:

O(mk)


for space.

That is NOT correct.


The heap contains at most:

K


elements.


Therefore:

SPACE = O(K)


not:

O(nK).


# CODE

```cpp
int findKthLargest(vector<int>& nums, int k)
{
    priority_queue<
        int,
        vector<int>,
        greater<int>
    > pq;

    for(int x : nums)
    {
        pq.push(x);

        if(pq.size() > k)
            pq.pop();
    }

    return pq.top();
}



104. TOP K LARGEST

KTH LARGEST
vs
TOP K LARGEST

KTH LARGEST:

Need:

ONE ANSWER

TOP K:

Need:

K ELEMENTS

SAME HEAP

MIN HEAP
+
SIZE K

At the end:

heap contains
K largest elements.

Difference:

KTH:

return top.

TOP K:

return all heap elements.

CONNECTION

KTH LARGEST
↓
TOP-K PATTERN

TOP K FREQUENT
↓
TOP-K PATTERN

K LARGEST
↓
TOP-K PATTERN

The story changes.

The heap pattern remains.

105. TOP K FREQUENT ELEMENTS
SOURCE CONNECTION

Explicitly listed in the IBM heap/PQ question bank.

TOP K FREQUENT
│
├── FIRST
│ ↓
│ COUNT FREQUENCY
│
├── THEN
│ ↓
│ TOP K
│
├── DATA STRUCTURES
│ │
│ ├── HashMap
│ └── Min Heap
│
└── PATTERN

FREQUENCY
+
TOP K

EXAMPLE

nums:

[1,1,1,2,2,3]

Frequency:

1 → 3
2 → 2
3 → 1

k = 2

Need:

1
2

STEP 1

Build frequency map.

unordered_map<int,int> freq;

STEP 2

Maintain min heap of:

{frequency, number}

Example:

(3,1)
(2,2)
(1,3)

WHY MIN HEAP?

Need:

TOP K frequencies.

Keep:

K largest frequencies.

The smallest frequency among the current K:

should be removed first.

Therefore:

MIN HEAP.

MENTAL MODEL

TOP K FREQUENT
│
├── "How often?"
│ ↓
│ HASHMAP
│
└── "Which K are highest?"
↓
MIN HEAP

CONNECTION

KTH LARGEST
↓
MIN HEAP SIZE K

TOP K FREQUENT
↓
FREQUENCY MAP
+
MIN HEAP SIZE K

Same second half:

TOP K.

IMPORTANT

Do NOT jump directly to heap.

First ask:

What is being ranked?

Here:

FREQUENCY.

Therefore:

MAP FIRST.

106. MERGE K SORTED LISTS
SOURCE CONNECTION

Explicitly listed in the IBM heap/PQ question bank.

MERGE K SORTED LISTS
│
├── INPUT
│ └── K sorted lists
│
├── QUESTION
│ └── merge into
│ one sorted list
│
├── KEY OBSERVATION
│ │
│ └── Each list's
│ current smallest
│ element matters
│
├── DATA STRUCTURE
│ └── MIN HEAP
│
└── HEAP CONTENT
└── one current candidate
from each list

EXAMPLE

List 1:

1 → 4 → 7

List 2:

2 → 5 → 8

List 3:

3 → 6 → 9

Current heads:

1
2
3

Need smallest:

1

After taking 1:

next candidate from list 1:

4

Heap now:

2
3
4

Take:

2

Then:

3

Then:

4...

MENTAL MODEL

K SORTED STREAMS

Each stream gives:

CURRENT SMALLEST

Need globally smallest.

Therefore:

MIN HEAP.

CORE PROCESS

Put first node of every list
into min heap.

Take smallest node.

Add it to result.

If that node has a next node:

push next node.

Repeat.

WHY HEAP SIZE K?

At most:

one candidate per list.

Therefore:

heap size ≤ K.

COMPLEXITY

If total number of elements:

N

Each heap operation:

O(log K)

Total:

O(N log K)

Space:

O(K)

for heap, excluding output.

CONNECTION

KTH LARGEST:

Heap stores:
K candidates.

MERGE K LISTS:

Heap stores:
K current candidates.

Common idea:

Keep only the candidates that can currently become the next answer.

107. MEDIAN FROM DATA STREAM
SOURCE CONNECTION

Explicitly listed in the IBM heap/PQ question bank.

MEDIAN STREAM
│
├── INPUT
│ └── numbers arrive
│ continuously
│
├── QUESTION
│ └── median after
│ each insertion
│
├── PROBLEM
│ └── Need middle values
│ dynamically
│
└── PATTERN
TWO HEAPS

TWO HEAPS

LOWER HALF
↓
MAX HEAP

UPPER HALF
↓
MIN HEAP

Why?

MAX HEAP
gives largest of lower half.

MIN HEAP
gives smallest of upper half.

Together:

the middle boundary
gives the median.

VISUAL

Numbers:

1 2 3 4 5

Lower half:

1 2

MAX HEAP:

top = 2

Upper half:

3 4 5

MIN HEAP:

top = 3

Median:

(2 + 3) / 2

TWO-HEAP INVARIANT

Usually maintain:

size difference ≤ 1

And:

every element in lower half
≤
every element in upper half.

INSERT

Suppose:

x

If x <= lower.top:

put into max heap.

Otherwise:

put into min heap.

Then rebalance.

REBALANCING

If one heap becomes too large:

move its top to the other heap.

Goal:

sizes differ by at most 1.

FIND MEDIAN

If sizes equal:

median:

(lower.top + upper.top) / 2

If one is larger:

median:

top of larger heap.

MENTAL MODEL

STREAM
↓
SPLIT INTO TWO HALVES

LOW HALF
↓
MAX HEAP

HIGH HALF
↓
MIN HEAP

MIDDLE
↓
HEAP TOPS

CONNECTION

KTH LARGEST
↓
ONE HEAP

MEDIAN
↓
TWO HEAPS

Why two?

Because median depends on:

both sides
of the middle.

108. TASK SCHEDULER
SOURCE CONNECTION

Task Scheduler is listed in the IBM heap/PQ question bank. The source names the problem but the retrieved PYQ material does not specify its exact statement/variant.

Therefore:

The exact IBM variant should NOT be assumed from the source.

For preparation, the standard task-scheduling pattern is:

TASKS
+
FREQUENCIES
+
PRIORITY QUEUE

CORE IDEA

Suppose:

A A A
B B
C

If a task has high frequency:

it creates more scheduling pressure.

Therefore:

Track frequency.

A max heap can repeatedly give:

MOST FREQUENT AVAILABLE TASK.

STANDARD PATTERN

TASKS
↓
FREQUENCY MAP
↓
MAX HEAP
↓
PROCESS HIGHEST FREQUENCY
↓
COOLDOWN / SCHEDULING RULE

The exact cooldown behavior depends on the problem statement.

IMPORTANT SOURCE LIMIT

The IBM source only confirms:

"Task scheduler problem"

It does NOT, in the retrieved text, specify:

cooldown value
exact scheduling rules
whether idle slots are allowed
exact required output

So those details should be taken from the actual question if encountered.

SET 8 — MASTER HEAP MAP

HEAP
│
├── MIN HEAP
│ ↓
│ smallest at top
│
├── MAX HEAP
│ ↓
│ largest at top
│
├── TOP K
│ │
│ ├── Kth largest
│ │ ↓
│ │ MIN HEAP
│ │
│ ├── Kth smallest
│ │ ↓
│ │ MAX HEAP
│ │
│ └── Top K frequent
│ ↓
│ frequency
│ +
│ MIN HEAP
│
├── MERGE K
│ ↓
│ MIN HEAP
│
├── MEDIAN
│ ↓
│ TWO HEAPS
│
└── TASK SCHEDULER
↓
FREQUENCY
+
PRIORITY QUEUE
depending on variant

SET 8 — THE MOST IMPORTANT PATTERN

QUESTION:

"Do I repeatedly need the smallest/largest/current best item?"

    ↓

YES

    ↓

HEAP

Then ask:

"What exactly am I keeping?"

    ↓

ONE BEST
→ normal heap

TOP K
→ heap size K

KTH LARGEST
→ min heap size K

KTH SMALLEST
→ max heap size K

MERGE K SORTED
→ min heap of current heads

MEDIAN STREAM
→ two heaps

FREQUENCY + TOP K
→ hashmap + heap

SET 8 — MIN HEAP vs MAX HEAP

NEED KTH LARGEST
↓
Keep K largest
↓
Need weakest among them
↓
SMALLEST
↓
MIN HEAP

NEED KTH SMALLEST
↓
Keep K smallest
↓
Need weakest among them
↓
LARGEST
↓
MAX HEAP

This is the most important heap inversion to remember.

SET 8 — STORY DECODING CHEAT SHEET

STORY
│
├── "Maximum/minimum repeatedly"
│ ↓
│ HEAP
│
├── "Kth largest"
│ ↓
│ MIN HEAP SIZE K
│
├── "Kth smallest"
│ ↓
│ MAX HEAP SIZE K
│
├── "Top K"
│ ↓
│ HEAP SIZE K
│
├── "Top K frequent"
│ ↓
│ HASHMAP + MIN HEAP
│
├── "Merge K sorted"
│ ↓
│ MIN HEAP
│ current head from each list
│
├── "Median of stream"
│ ↓
│ TWO HEAPS
│
└── "Task scheduling"
↓
FREQUENCY + PRIORITY QUEUE
depending on exact variant

SET 8 — TOP K FAMILY

TOP K
│
├── Kth Largest
│ ↓
│ min heap size K
│
├── K Largest
│ ↓
│ min heap size K
│
├── Top K Frequent
│ ↓
│ frequency map
│ +
│ min heap size K
│
└── K Smallest
↓
max heap size K

KEY CONNECTION

KTH LARGEST
↓
KEEP K BEST
↓
REMOVE WORST AMONG THEM

That is why:

MIN HEAP.

SET 8 — MERGE K CONNECTION

MERGE TWO SORTED ARRAYS
↓
Two pointers

MERGE K SORTED LISTS
↓
Many current pointers
↓
Need smallest among K
↓
MIN HEAP

So:

2 sources
↓
pointer comparison

K sources
↓
heap of candidates

SET 8 — MEDIAN CONNECTION

SORT ALL NUMBERS
↓
Find middle

But stream means:

numbers keep arriving.

Full sorting repeatedly:

expensive.

Therefore:

maintain structure dynamically.

LOW HALF
↓
MAX HEAP

HIGH HALF
↓
MIN HEAP

The two heap tops
stay around the middle.

SET 8 — HEAP + HASHMAP CONNECTION

TOP K FREQUENT

First question:

"What is the frequency?"

HASHMAP.

Second question:

"Which K frequencies are highest?"

HEAP.

Therefore:

HASHMAP
+
HEAP

Do not confuse their jobs.

HASHMAP

COUNT

HEAP

RANK / SELECT

SET 8 — HEAP vs SORTING

SORTING
│
└── Gives complete order

HEAP
│
└── Gives efficient access
to current best element

If question asks:

"Sort everything"

    ↓

SORT

If question asks:

"Kth"
"Top K"
"Repeated minimum"
"Repeated maximum"
"Merge K sorted"
"Median stream"

    ↓

THINK HEAP.

SET 8 — COMPLEXITY CHEAT SHEET

HEAP PUSH
↓
O(log n)

HEAP POP
↓
O(log n)

HEAP TOP
↓
O(1)

KTH LARGEST
↓
O(n log K)

KTH LARGEST SPACE
↓
O(K)

TOP K FREQUENT
↓
typically O(n log K)
after frequency counting,
depending on implementation

MERGE K SORTED LISTS
↓
O(N log K)

MERGE K SPACE
↓
O(K)

MEDIAN STREAM
↓
O(log n) per insertion
with two heaps

MEDIAN SPACE
↓
O(n)

SET 8 — HEAP COMPLEXITY MENTAL MODEL

Heap size:

N

push/pop:

log N

But if we deliberately maintain:

heap size K

then:

push/pop:

log K

Therefore:

TOP K

often becomes:

O(N log K)

This is why keeping the heap small is the optimization.

SET 8 — COMMON TRAPS

├── [ ] Using max heap for Kth largest
├── [ ] Forgetting heap-size K
├── [ ] Returning wrong heap top
├── [ ] Confusing Kth with Top K
├── [ ] Forgetting frequency map in Top K Frequent
├── [ ] Putting all elements into heap unnecessarily
├── [ ] Using one heap for median
├── [ ] Forgetting to rebalance two heaps
├── [ ] Confusing min heap with sorted array
└── [ ] Assuming exact Task Scheduler rules without reading the statement

SET 8 — KTH LARGEST TRAP

WRONG THOUGHT:

"Kth largest
→ max heap"

Why?

A max heap gives:

largest

But we need:

kth largest.

If we maintain:

MAX HEAP

we may have to retain many elements or remove repeatedly.

Better:

MIN HEAP
size K.

The smallest element inside the K largest:

is the kth largest.

SET 8 — KTH SMALLEST TRAP

Symmetric:

KTH SMALLEST
↓
MAX HEAP SIZE K

Because:

K smallest elements
are maintained.

The largest among them:

is the kth smallest.

SET 8 — MERGE K TRAP

Do NOT:

Put every element into heap immediately
if the point is to exploit the fact
that each list is already sorted.

Instead:

one current element
per list.

When one is removed:

push that list's next element.

This keeps:

heap size ≤ K.

SET 8 — MEDIAN TRAP

Do NOT think:

"Median = sort."

For a stream:

the numbers keep arriving.

Need:

dynamic middle.

Therefore:

two heaps.

SET 8 — CORE C++ TEMPLATES
MAX HEAP
priority_queue<int> pq;
MIN HEAP
priority_queue<
    int,
    vector<int>,
    greater<int>
> pq;
PUSH
pq.push(x);
TOP
int x = pq.top();
POP
pq.pop();
SIZE
pq.size();
EMPTY
pq.empty();
SET 8 — TOP K TEMPLATE
priority_queue<
    int,
    vector<int>,
    greater<int>
> pq;

for(int x : nums)
{
    pq.push(x);

    if(pq.size() > k)
        pq.pop();
}

At the end:

pq
 ↓
K largest elements

and:

pq.top()
 ↓
Kth largest
SET 8 — TOP K FREQUENT TEMPLATE
unordered_map<int, int> freq;

for(int x : nums)
{
    freq[x]++;
}

priority_queue<
    pair<int,int>,
    vector<pair<int,int>>,
    greater<pair<int,int>>
> pq;

for(auto [value, count] : freq)
{
    pq.push({count, value});

    if(pq.size() > k)
        pq.pop();
}

Mental structure:

nums
 ↓
frequency
 ↓
(freq, value)
 ↓
min heap
 ↓
size K
SET 8 — MERGE K TEMPLATE

Conceptual node:

struct Node
{
    int val;
    Node* next;
};

Heap stores:

(current value, list/node)

Process:

push first node of every list
        ↓
take minimum
        ↓
append to answer
        ↓
push its next node
        ↓
repeat
SET 8 — MEDIAN TEMPLATE
lower = MAX HEAP
upper = MIN HEAP

Invariant:

size(lower) ≈ size(upper)

and:

max(lower) <= min(upper)

Then:

equal sizes:
    median = average of two tops

one larger:
    median = top of larger heap
SET 8 — MASTER CONNECTION MAP

HEAP
│
├── NEED BEST ELEMENT
│ ↓
│ MIN / MAX HEAP
│
├── TOP K
│ ↓
│ SIZE K
│
├── KTH LARGEST
│ ↓
│ MIN HEAP K
│
├── KTH SMALLEST
│ ↓
│ MAX HEAP K
│
├── TOP K FREQUENT
│ ↓
│ HASHMAP
│ +
│ MIN HEAP
│
├── MERGE K SORTED
│ ↓
│ MIN HEAP
│ +
│ K CURRENT HEADS
│
├── MEDIAN STREAM
│ ↓
│ MAX HEAP
│ +
│ MIN HEAP
│
└── TASK SCHEDULER
↓
FREQUENCY
+
PRIORITY QUEUE
depending on exact variant

SET 8 — PRIORITY
TIER 1 — MUST MASTER

These form the core heap pattern and are directly represented in the IBM list:

├── [ ] 97. Heap fundamentals
├── [ ] 98. Priority Queue
├── [ ] 99. Heap operations
├── [ ] 100. Kth Largest
└── [ ] 101. Top K pattern

TIER 2 — HIGH VALUE

├── [ ] 102. Top K Frequent Elements
├── [ ] 103. Merge K Sorted Lists
└── [ ] 104. Median from Data Stream

TIER 3 — VARIANT / EXACT-STATEMENT DEPENDENT

└── [ ] 105. Task Scheduler

IMPORTANT SOURCE DISTINCTION

The IBM source explicitly lists:

Max heap operations (2025)
Kth largest
Merge K sorted lists
Top K frequent
Median from data stream
Task scheduler

but the retrieved source does not give individual frequency percentages for each one.

Therefore:

The Tier ordering above is a preparation/prerequisite ordering,
NOT a claim that IBM asks Tier 1 more frequently.

SET 8 — CHECKLIST

SET 8 — HEAPS + PRIORITY QUEUES
│
├── FUNDAMENTALS
│ ├── [ ] Complete binary tree
│ ├── [ ] Min heap
│ ├── [ ] Max heap
│ ├── [ ] Heapify up
│ ├── [ ] Heapify down
│ └── [ ] Array representation
│
├── C++ PRIORITY QUEUE
│ ├── [ ] Max heap syntax
│ ├── [ ] Min heap syntax
│ ├── [ ] push
│ ├── [ ] pop
│ ├── [ ] top
│ └── [ ] size
│
├── CORE PROBLEMS
│ ├── [ ] Max heap operations
│ ├── [ ] Kth largest
│ ├── [ ] Top K frequent
│ ├── [ ] Merge K sorted lists
│ ├── [ ] Median stream
│ └── [ ] Task scheduler
│
└── PATTERNS
├── [ ] Top K
├── [ ] Heap + HashMap
├── [ ] K-way merge
└── [ ] Two heaps

SET 8 — EDGE CASES

KTH LARGEST

├── [ ] k = 1
├── [ ] k = n
├── [ ] duplicates
└── [ ] negative numbers

TOP K FREQUENT

├── [ ] k = 1
├── [ ] all elements same frequency
├── [ ] duplicate input values
└── [ ] k = number of unique values

MERGE K LISTS

├── [ ] k = 0
├── [ ] empty lists
├── [ ] one list
└── [ ] duplicate values

MEDIAN

├── [ ] one element
├── [ ] even count
├── [ ] odd count
├── [ ] duplicate values
└── [ ] negative values

HEAP

├── [ ] empty heap
└── [ ] single element

SET 8 — FINAL RECOGNITION RULES
Repeated minimum/maximum → think heap.
Kth largest → min heap of size K.
Kth smallest → max heap of size K.
Top K → maintain heap size K.
Top K frequent → frequency map first, heap second.
Merge K sorted lists → min heap of current heads.
Median stream → two heaps.
Lower half → max heap.
Upper half → min heap.
Heap top is O(1).
Heap push/pop is O(log heap-size).
If heap size is K, push/pop is O(log K).
Don't sort the entire array if only Top K is required.
Don't put all K sorted-list elements into a heap when one candidate per list is enough.
HashMap counts; Heap selects.
Kth and Top K are related but not identical.
The heap is not globally sorted.
Task Scheduler must be solved according to its exact statement because the IBM source only names the problem.
SET 8 — COMPLETE STORY

QUESTION
↓
Repeatedly need
minimum / maximum?
↓
HEAP

QUESTION
↓
Kth largest?
↓
MIN HEAP
↓
SIZE K

QUESTION
↓
Kth smallest?
↓
MAX HEAP
↓
SIZE K

QUESTION
↓
Top K frequent?
↓
HASHMAP
↓
FREQUENCY
↓
MIN HEAP
↓
SIZE K

QUESTION
↓
Merge K sorted lists?
↓
MIN HEAP
↓
ONE CURRENT HEAD
FROM EACH LIST

QUESTION
↓
Median of stream?
↓
TWO HEAPS
↓
LOW HALF + HIGH HALF

QUESTION
↓
Task scheduler?
↓
READ EXACT VARIANT
↓
FREQUENCY + PRIORITY QUEUE
if applicable

SET 8 — CONNECTION TO PREVIOUS SETS

SET 4 — HASHING
│
└── Frequency Map
↓
SET 8
│
└── Top K Frequent
↓
HashMap + Heap

SET 3 — LINKED LIST
│
└── Merge Sorted Lists
↓
SET 8
│
└── Merge K Sorted Lists
↓
K-way merge + Heap

SET 7 — DP
│
└── optimization / choices

SET 8 — HEAP
│
└── repeatedly choose
current best candidate

SET 6 — BFS
│
└── Queue

SET 8 — PRIORITY QUEUE
│
└── Queue where
highest-priority item
comes first

SET 8 — THE BIGGEST MENTAL CONNECTION

NORMAL QUEUE:

First In
↓
First Out

PRIORITY QUEUE:

Highest priority
↓
First Out

Therefore:

QUEUE

order of arrival

PRIORITY QUEUE

order of priority

This is why priority queues are useful in:

Kth/top-K problems
Scheduling
K-way merge
Dynamic median
SET 8 — FINAL MEMORY MAP

HEAP
│
├── MIN
│ └── smallest top
│
├── MAX
│ └── largest top
│
├── TOP K
│ └── maintain K
│
├── KTH LARGEST
│ └── MIN K
│
├── KTH SMALLEST
│ └── MAX K
│
├── FREQUENCY
│ └── MAP + HEAP
│
├── K-WAY MERGE
│ └── MIN HEAP
│
├── MEDIAN
│ └── TWO HEAPS
│
└── SCHEDULING
└── FREQUENCY + PQ
depending on variant

SET 8 — COMPLETION TARGET

Before moving to Set 9, you should be able to immediately recognize:

"Kth largest"
↓
MIN HEAP SIZE K

"Kth smallest"
↓
MAX HEAP SIZE K

"Top K frequent"
↓
HASHMAP + MIN HEAP

"Merge K sorted lists"
↓
MIN HEAP
+
one candidate per list

"Median from stream"
↓
MAX HEAP + MIN HEAP

"Repeatedly get minimum"
↓
MIN HEAP

"Repeatedly get maximum"
↓
MAX HEAP

"Priority matters more than arrival order"
↓
PRIORITY QUEUE
