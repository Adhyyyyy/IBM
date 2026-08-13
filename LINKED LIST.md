# IBM OA — MASTER PATTERN NOTEBOOK
# SET 3 — LINKED LIST

Source basis:

The IBM PYQ resource lists the following Linked List problems:

- Create linked list node (2024)
- Detect cycle using Floyd's algorithm (Multiple years)
- Reverse linked list — iterative/recursive (2024)
- Find middle element (2024)
- Merge two sorted lists
- Remove nth node from end (Unspecified)
- Flatten multilevel linked list
- Copy list with random pointer
- Add two numbers represented as lists
- Intersection of two linked lists

The resource also reports Linked List cycle detection using Floyd's algorithm as a **90% frequency** technical-interview topic and states that Linked List problems appear in **85% of technical interviews** in its compiled analysis. :contentReference[oaicite:0]{index=0} :contentReference[oaicite:1]{index=1}

The resource explicitly records these as live-coding questions:

- Create a linked list node
- Detect a cycle using Floyd's algorithm
- Reverse a linked list iteratively and recursively
- Find the middle element
- Merge two sorted linked lists :contentReference[oaicite:2]{index=2}

---

# SET 3 — BIG PICTURE

SET 3 — LINKED LIST
│
├── FUNDAMENTALS
│      │
│      ├── Node
│      ├── Head
│      ├── next
│      └── Traversal
│
├── TWO POINTERS
│      │
│      ├── Fast / Slow
│      ├── Middle
│      ├── Cycle
│      └── Nth From End
│
├── POINTER MANIPULATION
│      │
│      ├── Reverse
│      ├── Merge
│      └── Reconnect
│
├── LIST RELATIONSHIPS
│      │
│      ├── Intersection
│      └── Cycle
│
└── ADVANCED LINKED LIST
       │
       ├── Random Pointer
       ├── Multilevel List
       └── Arithmetic using Lists


---

# SET 3 — MASTER MENTAL MAP

LINKED LIST
│
├── "MOVE THROUGH NODES"
│       ↓
│    curr = curr->next
│
├── "REVERSE"
│       ↓
│    prev / curr / next
│
├── "MIDDLE"
│       ↓
│    slow / fast
│
├── "CYCLE"
│       ↓
│    slow / fast
│
├── "NTH FROM END"
│       ↓
│    maintain GAP
│       ↓
│    two pointers
│
├── "MERGE SORTED LISTS"
│       ↓
│    compare current nodes
│       ↓
│    connect smaller
│
├── "INTERSECTION"
│       ↓
│    align paths
│       ↓
│    two-pointer switching
│
├── "RANDOM POINTER"
│       ↓
│    node mapping
│       ↓
│    HashMap / interleaving
│
├── "ADD NUMBERS"
│       ↓
│    digit-by-digit
│       ↓
│    carry
│
└── "MULTILEVEL"
        ↓
     pointer restructuring


---

# THE MOST IMPORTANT LINKED LIST IDEA

Before individual problems, understand this:

ARRAY
│
├── Data stored continuously
├── index available
└── arr[i]

LINKED LIST
│
├── Nodes can be anywhere in memory
├── No direct index
└── follow pointers

        NODE

   ┌───────────────┐
   │ data │ next ──┼──────► next node
   └───────────────┘


Therefore:

ARRAY
   ↓
INDEX MOVEMENT

LINKED LIST
   ↓
POINTER MOVEMENT


---

# LINKED LIST CORE STRUCTURE

struct Node
{
    int data;
    Node* next;

    Node(int x)
    {
        data = x;
        next = nullptr;
    }
};


MENTAL MODEL:

Node
│
├── data
│
└── next
       │
       ├── nullptr
       │
       └── another Node


Example:

head

  ↓

[10 | •] ───► [20 | •] ───► [30 | nullptr]


The `next` pointer stores the address of the next node.

---

# 30. CREATE LINKED LIST NODE

## SOURCE CONNECTION

This is explicitly listed as a 2024 live-coding question. :contentReference[oaicite:3]{index=3}

---

CREATE NODE
│
├── STORY
│      └── Create a linked-list node
│
├── STRUCTURE
│      │
│      ├── data
│      └── next
│
├── INITIAL STATE
│      │
│      ├── data = given value
│      └── next = nullptr
│
├── MENTAL MODEL
│
│      Node
│       │
│       ├── data
│       │
│       └── next → nullptr
│
└── CORE CODE

struct Node
{
    int data;
    Node* next;

    Node(int x)
    {
        data = x;
        next = nullptr;
    }
};


## CONNECTION

CREATE NODE
     ↓
NODE STRUCTURE
     ↓
TRAVERSAL
     ↓
INSERTION
     ↓
DELETION
     ↓
ALL LINKED LIST PROBLEMS


## REMEMBER

A linked list is not the nodes alone.

It is:

NODE
 +
POINTER CONNECTIONS


---

# 31. TRAVERSE A LINKED LIST

This is not separately listed as a PYQ, but it is the foundation required by every Linked List problem in the resource.

---

TRAVERSAL
│
├── START
│      ↓
│    head
│
├── CURRENT NODE
│      ↓
│    curr
│
├── MOVE
│      ↓
│    curr = curr->next
│
└── STOP
       ↓
    curr == nullptr


MENTAL MODEL:

head
 ↓
10 → 20 → 30 → nullptr

curr = head

curr
 ↓
10

curr = curr->next

curr
 ↓
20

curr = curr->next

curr
 ↓
30

curr = curr->next

curr
 ↓
nullptr


## CORE TEMPLATE

Node* curr = head;

while(curr != nullptr)
{
    // process curr

    curr = curr->next;
}


## MOST IMPORTANT LINKED LIST RULE

When you want to move:

ARRAY:
    i++

LINKED LIST:
    curr = curr->next


---

# 32. REVERSE LINKED LIST — ITERATIVE

## SOURCE CONNECTION

Explicitly listed as a 2024 live-coding question. :contentReference[oaicite:4]{index=4}

---

REVERSE LINKED LIST
│
├── ORIGINAL
│
│      10 → 20 → 30 → nullptr
│
├── REQUIRED
│
│      10 ← 20 ← 30
│                        ↑
│                       head
│
├── PROBLEM
│      │
│      └── Every arrow must
│          point backward
│
├── PATTERN
│      └── POINTER REVERSAL
│
├── REQUIRED POINTERS
│      │
│      ├── prev
│      ├── curr
│      └── next
│
├── MENTAL MODEL
│
│      prev   curr   next
│       ↓      ↓      ↓
│      null   10     20
│
├── STEP 1
│      │
│      └── Save next
│
│          next = curr->next
│
├── STEP 2
│      │
│      └── Reverse arrow
│
│          curr->next = prev
│
├── STEP 3
│      │
│      └── Move prev
│
│          prev = curr
│
├── STEP 4
│      │
│      └── Move curr
│
│          curr = next
│
└── FINAL
       head = prev


## CRITICAL RULE

Before changing:

curr->next

SAVE IT FIRST.

Otherwise:

curr->next
       ↓
    original next
       ↓
     LOST


So:

SAVE
 ↓
REVERSE
 ↓
MOVE


## CONNECTION

REVERSE ARRAY
     ↓
two pointers

REVERSE LINKED LIST
     ↓
pointer reversal

Both are:

CHANGE DIRECTION


## ITERATIVE TEMPLATE

Node* prev = nullptr;
Node* curr = head;

while(curr != nullptr)
{
    Node* next = curr->next;

    curr->next = prev;

    prev = curr;
    curr = next;
}

head = prev;


## COMPLEXITY

Time:
O(n)

Extra space:
O(1)


---

# 33. REVERSE LINKED LIST — RECURSIVE

## SOURCE CONNECTION

The resource explicitly includes iterative/recursive reverse linked list. :contentReference[oaicite:5]{index=5}

---

RECURSIVE REVERSE
│
├── KEY IDEA
│      │
│      └── Let recursion reverse
│          everything after current
│
├── EXAMPLE
│
│      10 → 20 → 30 → nullptr
│
├── RECURSION
│
│      reverse(10)
│          ↓
│      reverse(20)
│          ↓
│      reverse(30)
│
├── BASE CASE
│      │
│      ├── head == nullptr
│      └── head->next == nullptr
│
├── AFTER RECURSION
│      │
│      └── reverse the pointer
│
│          head->next->next = head
│
├── THEN
│      │
│      └── head->next = nullptr
│
└── RETURN
       new head


## MENTAL MODEL

Don't try to reverse the entire list at once.

Think:

reverse(
    current
    +
    everything after current
)


The recursive call handles the suffix.

Current node only needs to connect itself backward.

---

# ITERATIVE vs RECURSIVE

ITERATIVE
│
├── prev
├── curr
├── next
└── O(1) extra space

RECURSIVE
│
├── recursion stack
├── base case
└── O(n) stack space


MEMORY TRIGGER:

ITERATIVE
    ↓
prev / curr / next

RECURSIVE
    ↓
reverse suffix
    ↓
connect current backward


---

# 34. FIND MIDDLE ELEMENT

## SOURCE CONNECTION

Explicitly listed as a 2024 live-coding question. :contentReference[oaicite:6]{index=6}

---

FIND MIDDLE
│
├── STORY
│      └── Find middle node
│
├── NAIVE
│      │
│      ├── count nodes
│      ├── calculate middle
│      └── traverse again
│
├── OPTIMIZATION
│      └── FAST / SLOW POINTER
│
├── POINTERS
│      │
│      ├── slow → one step
│      └── fast → two steps
│
├── MENTAL MODEL
│
│      1 → 2 → 3 → 4 → 5
│
│      slow
│       ↓
│       1 → 2 → 3
│
│      fast
│       ↓
│       1 → 3 → 5
│
├── WHEN FAST REACHES END
│      │
│      └── slow is at middle
│
├── PATTERN
│      └── FAST / SLOW
│
├── CONNECTION
│      │
│      ├── Cycle detection
│      ├── Find nth from end
│      ├── Palindrome linked list
│      └── Split linked list
│
└── COMPLEXITY
       O(n)
       O(1)


## MASTER RULE

FAST
moves 2

SLOW
moves 1

Therefore:

FAST covers distance twice as quickly.

When FAST reaches the end:

SLOW
   ↓
MIDDLE


---

# EVEN-LENGTH LIST

Example:

1 → 2 → 3 → 4 → nullptr

Depending on the exact problem convention, the returned middle may be:

3

or:

2

The common LeetCode convention returns the **second middle**, so the pointer condition matters.

For:

while(fast != nullptr && fast->next != nullptr)

    slow = slow->next
    fast = fast->next->next

the result is:

1 → 2 → 3 → 4
          ↑
         slow

Answer = 3.


## IMPORTANT

Don't memorize the middle answer blindly.

Understand the loop condition.

---

# 35. DETECT CYCLE — FLOYD'S ALGORITHM

## SOURCE CONNECTION

This is one of the strongest IBM-linked-list patterns in the resource.

The resource explicitly lists:

> Detect cycle using Floyd's algorithm (Multiple years)

and gives it a **90% interview-frequency** rating. :contentReference[oaicite:7]{index=7} :contentReference[oaicite:8]{index=8}

---

CYCLE DETECTION
│
├── STORY
│      └── Determine whether
│          linked list contains a cycle
│
├── NORMAL LIST
│
│      10 → 20 → 30 → nullptr
│
├── CYCLIC LIST
│
│      10 → 20 → 30
│           ↑       │
│           └───────┘
│
├── PROBLEM
│      │
│      └── Traversal never reaches nullptr
│
├── PATTERN
│      └── FAST / SLOW POINTER
│
├── SLOW
│      └── moves 1 step
│
├── FAST
│      └── moves 2 steps
│
├── KEY OBSERVATION
│      │
│      └── If cycle exists,
│          fast eventually catches slow
│
└── IF NO CYCLE
       ↓
    fast reaches nullptr


## MENTAL MODEL

Imagine runners on a circular track.

SLOW:
    →

FAST:
    →

FAST is faster.

If the track is circular:

FAST eventually catches SLOW.


If the track is not circular:

FAST falls off the end.


Therefore:

FAST == SLOW
       ↓
    CYCLE

FAST == nullptr
       ↓
  NO CYCLE


## CORE TEMPLATE

Node* slow = head;
Node* fast = head;

while(fast != nullptr &&
      fast->next != nullptr)
{
    slow = slow->next;
    fast = fast->next->next;

    if(slow == fast)
        return true;
}

return false;


## CONNECTION

FIND MIDDLE
     ↓
FAST / SLOW

CYCLE DETECTION
     ↓
FAST / SLOW

So:

FAST / SLOW
     ↓
One of the most important
Linked List patterns.


---

# 36. REMOVE NTH NODE FROM END

## SOURCE CONNECTION

The resource explicitly lists:

> Remove nth node from the back of the linked list

as an unspecified-year IBM OA problem. :contentReference[oaicite:9]{index=9}

---

REMOVE NTH FROM END
│
├── STORY
│      └── Delete node
│          n positions from end
│
├── NAIVE
│      │
│      ├── Count length
│      ├── Find position
│      └── Traverse again
│
├── BETTER
│      └── TWO POINTERS
│
├── CORE IDEA
│      │
│      └── Maintain a GAP of n
│          between pointers
│
├── POINTERS
│      │
│      ├── fast
│      └── slow
│
├── STEP 1
│      │
│      └── Move fast n steps
│
├── STEP 2
│      │
│      └── Move both together
│
├── STEP 3
│      │
│      └── When fast reaches end,
│          slow is before target
│
├── DELETE
│      │
│      └── slow->next =
│          slow->next->next
│
└── PATTERN
       TWO POINTER + GAP


## MENTAL MODEL

List:

1 → 2 → 3 → 4 → 5

n = 2

Target:

4

Maintain:

slow
 ↓
1

fast
 ↓
3

Distance = 2


Move both:

slow
 ↓
2

fast
 ↓
4


Again:

slow
 ↓
3

fast
 ↓
5


Now:

slow is immediately before target.

Delete:

3 → 5


## CONNECTION

MIDDLE
   ↓
FAST / SLOW

CYCLE
   ↓
FAST / SLOW

NTH FROM END
   ↓
FAST / SLOW
   +
GAP


## MASTER RULE

FAST / SLOW has multiple meanings.

Ask:

> What relationship am I trying to maintain?

MIDDLE:
fast = 2 × slow

NTH FROM END:
fast = slow + n

CYCLE:
fast catches slow


---

# 37. MERGE TWO SORTED LINKED LISTS

## SOURCE CONNECTION

Explicitly listed in the Linked List DSA bank and as live coding. :contentReference[oaicite:10]{index=10} :contentReference[oaicite:11]{index=11}

---

MERGE TWO SORTED LISTS
│
├── STORY
│      └── Two sorted linked lists
│
├── GOAL
│      └── Produce one sorted list
│
├── INPUT
│
│      A:
│      1 → 4 → 7
│
│      B:
│      2 → 3 → 8
│
├── FIRST THOUGHT
│      │
│      └── Compare current nodes
│
├── POINTERS
│      │
│      ├── p1 → list A
│      └── p2 → list B
│
├── RULE
│      │
│      └── Pick smaller current node
│
├── CONNECT
│      │
│      └── Add it to result
│
├── MOVE
│      │
│      └── Move pointer from
│          whichever list was selected
│
├── REMAINING
│      │
│      └── Attach remaining list
│
└── PATTERN
       TWO POINTER MERGE


## MENTAL MODEL

A:

1 → 4 → 7

B:

2 → 3 → 8


Compare:

1 vs 2
 ↓
take 1

2 vs 4
 ↓
take 2

3 vs 4
 ↓
take 3

4 vs 8
 ↓
take 4

7 vs 8
 ↓
take 7

remaining:
8


Result:

1 → 2 → 3 → 4 → 7 → 8


## CONNECTION

MERGE SORT
   ↓
merge two sorted arrays

LINKED LIST MERGE
   ↓
merge two sorted lists

The underlying idea is identical:

> Compare the front of each sorted structure and consume the smaller one.


## COMPLEXITY

O(n + m) time

O(1) auxiliary space
if nodes are reused.


---

# 38. INTERSECTION OF TWO LINKED LISTS

## SOURCE CONNECTION

The resource includes Intersection of two linked lists. :contentReference[oaicite:12]{index=12}

---

INTERSECTION
│
├── IMPORTANT
│      │
│      └── Intersection means
│          SAME NODE
│
├── NOT
│      │
│      └── Same VALUE
│
├── EXAMPLE
│
│      A:
│      1 → 2
│           \
│            8 → 9
│           /
│      B:  4 → 5
│
│
│      Node 8 is physically
│      the same node.
│
├── NAIVE
│      │
│      └── Store addresses in Set
│
├── OPTIMIZED
│      └── TWO POINTER SWITCHING
│
├── POINTERS
│      │
│      ├── pA
│      └── pB
│
├── RULE
│
│      If pA reaches null:
│          move to headB
│
│      If pB reaches null:
│          move to headA
│
├── WHY?
│      │
│      └── Both pointers travel:
│
│          lengthA + lengthB
│
│      Therefore path lengths
│      become aligned.
│
└── PATTERN
       PATH ALIGNMENT


## MENTAL MODEL

A path:

A-only + common

B path:

B-only + common


Pointer A:

A-only → common
then
B-only → common


Pointer B:

B-only → common
then
A-only → common


Both have traversed:

A + B

Therefore:

They meet at the intersection.


## CONNECTION

NTH FROM END
   ↓
Maintain GAP

INTERSECTION
   ↓
Equalize PATH LENGTH


---

# 39. ADD TWO NUMBERS REPRESENTED BY LINKED LISTS

## SOURCE CONNECTION

The resource includes "Add two numbers represented as lists." :contentReference[oaicite:13]{index=13}

---

ADD TWO NUMBERS
│
├── STORY
│      └── Each node represents
│          a digit
│
├── CORE IDEA
│      │
│      └── Normal addition
│          from right to left
│
├── LINKED LIST ISSUE
│      │
│      └── If digits are stored
│          least-significant first,
│          traversal already goes
│          right → left
│
├── STATE
│      │
│      ├── p1
│      ├── p2
│      └── carry
│
├── EQUATION
│
│      sum = digit1 + digit2 + carry
│
│      digit = sum % 10
│
│      carry = sum / 10
│
├── PATTERN
│      └── DIGIT SIMULATION
│             +
│          CARRY
│
├── CONNECTION
│      │
│      ├── Addition
│      ├── Carry
│      ├── Multiple pointers
│      └── Dummy node
│
└── COMPLEXITY
       O(max(n,m))


## MENTAL MODEL

Example:

2 → 4 → 3

represents:

342

5 → 6 → 4

represents:

465


Add:

342
+
465
=
807


Linked-list result:

7 → 0 → 8


Process:

2 + 5 = 7

4 + 6 = 10
     ↓
digit = 0
carry = 1

3 + 4 + 1 = 8


---

# 40. PALINDROME LINKED LIST

This is not explicitly listed as a separate Linked List item in the resource, so treat it as a **pattern extension**, not a source-reported IBM question.

---

PALINDROME LINKED LIST
│
├── STORY
│      └── Same forward/backward
│
├── FIRST THOUGHT
│      └── Two sides must match
│
├── PROBLEM
│      │
│      └── Linked list has
│          no backward pointer
│
├── APPROACH
│      │
│      ├── Find middle
│      ├── Reverse second half
│      └── Compare both halves
│
├── PATTERNS COMBINED
│      │
│      ├── Fast / Slow
│      ├── Reverse
│      └── Two pointers
│
└── CONNECTION

MIDDLE
  +
REVERSE
  +
COMPARE


This is a good example of why pattern connections matter more than memorizing isolated questions.

---

# 41. FLATTEN MULTILEVEL LINKED LIST

## SOURCE CONNECTION

The resource includes Flatten multilevel linked list. :contentReference[oaicite:14]{index=14}

---

FLATTEN MULTILEVEL LIST
│
├── STORY
│      └── Nodes may contain
│          additional child/down pointers
│
├── STRUCTURE
│
│      node
│      │
│      ├── next
│      └── child
│
├── GOAL
│      └── Convert into one level
│
├── CORE CHALLENGE
│      │
│      └── Pointer restructuring
│
├── PATTERN
│      │
│      ├── Traversal
│      ├── Recursion / Stack
│      └── Pointer manipulation
│
├── CONNECTION
│      │
│      ├── DFS
│      ├── Stack
│      └── Tree-like traversal
│
└── PRIORITY

LOWER than:

Cycle
Reverse
Middle
Merge
Nth from end

for IBM preparation because the resource does not mark it as an exact OA/live-coding question.


---

# 42. COPY LIST WITH RANDOM POINTER

## SOURCE CONNECTION

The resource includes Copy list with random pointer. :contentReference[oaicite:15]{index=15}

---

COPY RANDOM POINTER
│
├── NODE
│      │
│      ├── data
│      ├── next
│      └── random
│
├── PROBLEM
│      │
│      └── Create completely
│          independent copy
│
├── KEY ISSUE
│      │
│      └── random may point
│          anywhere
│
├── PATTERN
│      └── NODE MAPPING
│
├── SIMPLE APPROACH
│      │
│      ├── Create copy of each node
│      ├── Map original → copy
│      └── Connect pointers
│
├── HASHMAP
│
│      original node
│             ↓
│          copied node
│
├── CONNECTION
│      │
│      ├── Graph cloning
│      ├── Object mapping
│      └── HashMap
│
└── PRIORITY

Advanced Linked List pattern.

Not among the five exact live-coding Linked List questions reported in the resource.


---

# SET 3 — MASTER FAST/SLOW MAP

FAST / SLOW
│
├── FIND MIDDLE
│      │
│      └── fast moves 2
│          slow moves 1
│
├── DETECT CYCLE
│      │
│      └── fast catches slow
│
├── NTH FROM END
│      │
│      └── maintain gap n
│
└── PALINDROME
       │
       └── find middle
           + reverse second half


This is one of the most important Linked List mental structures.

When you see:

> "middle"

> "cycle"

> "nth from end"

don't immediately start coding.

First ask:

```text
Can FAST + SLOW maintain the relationship?
