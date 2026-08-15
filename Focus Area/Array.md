ADHY, yes. I studied the attached String master notebook and I'm following the same structure: **big picture → mental map → pattern recognition → each problem → intuition → algorithm → C++ solution → dry run → complexity → when to use → when not to use → OA traps → interview explanation → memory trigger → master cheat sheet**. 

Below is the **complete Arrays / Hashing Set 1 notebook** for Problems **9–13**, written so you can directly paste it into your `.md` file.

````md
# ARRAY + HASHING — MASTER PATTERN NOTEBOOK
## 5 HIGH-VALUE ARRAY PROBLEMS
### OA + INTERVIEW + PATTERN RECOGNITION

---

# TABLE OF CONTENTS

9. Pair With Given Sum / Two Sum
10. Print All Duplicates
11. Find Missing Number
12. Remove Duplicates From Sorted Array
13. Common Elements in Three Sorted Arrays

---

# ============================================================
# 0. ARRAYS / HASHING — BIG PICTURE
# ============================================================

ARRAY PROBLEMS
│
├── HASHING
│   │
│   ├── Two Sum
│   │      └── Hash Map
│   │
│   └── Print All Duplicates
│          └── Hash Set
│
├── BIT MANIPULATION
│   │
│   └── Find Missing Number
│          └── XOR
│
├── TWO POINTERS
│   │
│   ├── Two Sum in Sorted Array
│   │
│   └── Remove Duplicates
│
└── MULTIPLE POINTERS
    │
    └── Common Elements in Three Sorted Arrays
           └── Three Pointers


# ============================================================
# 1. MASTER MENTAL MAP
# ============================================================

ARRAY
│
├── "Find two numbers whose sum is target"
│       ↓
│   NEED = TARGET - CURRENT
│       ↓
│   HASH MAP
│
├── "Find duplicates / repeated values"
│       ↓
│   HAVE I SEEN THIS?
│       ↓
│   HASH SET
│
├── "One number missing from 0...n"
│       ↓
│   XOR CANCELLATION
│       ↓
│   XOR
│
├── "Remove duplicates from SORTED array"
│       ↓
│   DUPLICATES ARE ADJACENT
│       ↓
│   TWO POINTERS
│
└── "Common elements in THREE SORTED arrays"
        ↓
    THREE POINTERS
        ↓
    MOVE THE SMALLEST


# ============================================================
# 2. MASTER PATTERN RECOGNITION
# ============================================================

When reading an Array problem, ask:

1. Do I need to find a pair satisfying a condition?
   → HASH MAP / TWO POINTERS

2. Do I only need to know whether something was seen?
   → HASH SET

3. Is one number missing from a known range?
   → XOR / SUM

4. Is the array SORTED?
   → Think TWO POINTERS.

5. Are MULTIPLE arrays sorted?
   → Think MULTIPLE POINTERS.

6. Does the problem require in-place modification?
   → Think READ + WRITE POINTERS.

7. Is the problem asking for fast lookup?
   → Think HASHING.

8. Can sorted order eliminate impossible candidates?
   → Think POINTERS.


# ============================================================
# 3. MASTER PATTERN TABLE
# ============================================================

| Problem | Main Pattern | Data Structure | Time | Extra Space |
|---|---|---|---|---|
| Two Sum | Hash Lookup | Hash Map | O(n) avg | O(n) |
| Print All Duplicates | Seen Tracking | Hash Set | O(n) avg | O(n) |
| Missing Number | XOR Cancellation | XOR | O(n) | O(1) |
| Remove Duplicates | Two Pointers | None | O(n) | O(1) |
| Common 3 Arrays | Three Pointers | None | O(n+m+p) | O(1)* |

*excluding output.


# ============================================================
# 4. PROBLEM 9 — PAIR WITH GIVEN SUM / TWO SUM
# ============================================================

## PROBLEM

Given an array of integers `nums` and an integer `target`,
find two distinct elements whose sum equals `target`.

Return their indices.

If no such pair exists, return `{-1, -1}`.

Example:

Input:

nums = [2, 7, 11, 15]
target = 9

Output:

[0, 1]

Because:

2 + 7 = 9


# ------------------------------------------------------------
# PATTERN
# ------------------------------------------------------------

TWO SUM
   ↓
a + b = target
   ↓
b = target - a
   ↓
NEED = TARGET - CURRENT
   ↓
HASH MAP
   ↓
CHECK WHETHER NEED WAS SEEN


# ------------------------------------------------------------
# KEY OBSERVATION
# ------------------------------------------------------------

For every current element:

nums[i]

we need:

target - nums[i]

Example:

target = 9
current = 2

need:

9 - 2 = 7

So the question becomes:

"Have I already seen 7?"

If yes → answer found.

If no → store current element.


# ------------------------------------------------------------
# WHY HASH MAP?
# ------------------------------------------------------------

Brute force:

For every element:

    search every other element

This gives:

O(n²)

Instead, store previously seen values:

value → index

Then lookup becomes O(1) average.

Therefore:

O(n) average time.


# ------------------------------------------------------------
# DATA STRUCTURE
# ------------------------------------------------------------

unordered_map<int, int>

Meaning:

KEY   → number
VALUE → index

Example:

2 → 0
7 → 1
11 → 2


# ------------------------------------------------------------
# ALGORITHM
# ------------------------------------------------------------

1. Create an empty hash map.

2. Traverse the array.

3. Calculate:

   need = target - nums[i]

4. Check whether `need` exists in the map.

5. If yes:
   return current index + stored index.

6. If no:
   store:

   nums[i] → i

7. If traversal ends:
   return {-1, -1}.


# ------------------------------------------------------------
# C++ SOLUTION
# ------------------------------------------------------------

```cpp
vector<int> twoSum(vector<int>& nums, int target) {

    unordered_map<int, int> mp;

    for (int i = 0; i < nums.size(); i++) {

        int need = target - nums[i];

        if (mp.find(need) != mp.end()) {
            return {i, mp[need]};
        }

        mp[nums[i]] = i;
    }

    return {-1, -1};
}
````

# ------------------------------------------------------------

# DRY RUN

# ------------------------------------------------------------

nums = [2, 7, 11, 15]
target = 9

i = 0

current = 2

need:

9 - 2 = 7

7 is NOT in map.

Store:

2 → 0

i = 1

current = 7

need:

9 - 7 = 2

2 IS in map.

map:

2 → 0

Therefore:

return {1, 0}

# ------------------------------------------------------------

# WHY CHECK BEFORE STORE?

# ------------------------------------------------------------

This is important.

Suppose:

nums = [3]

target = 6

current = 3

need = 3

If we store `3` first and then search,
we could accidentally use the same element twice.

Therefore:

CHECK NEED
↓
THEN STORE CURRENT

# ------------------------------------------------------------

# DUPLICATE CASE

# ------------------------------------------------------------

nums = [3, 3]
target = 6

i = 0:

need = 3

not found.

Store:

3 → 0

i = 1:

need = 3

found.

Return:

{1, 0}

Correct.

# ------------------------------------------------------------

# COMPLEXITY

# ------------------------------------------------------------

Time:

O(n) average

Space:

O(n)

# ------------------------------------------------------------

# SORTED ARRAY VARIANT

# ------------------------------------------------------------

If the array is SORTED, we can use two pointers.

Example:

nums = [1, 2, 4, 6, 8, 9]
target = 10

left = 0
right = n - 1

Calculate:

sum = nums[left] + nums[right]

If:

sum < target
↓
left++

If:

sum > target
↓
right--

If:

sum == target
↓
FOUND

# ------------------------------------------------------------

# TWO SUM PATTERN

# ------------------------------------------------------------

UNSORTED
↓
HASH MAP

SORTED
↓
TWO POINTERS

# ------------------------------------------------------------

# WHEN TO USE HASH MAP

# ------------------------------------------------------------

Use Hash Map when:

* Array is unsorted.
* Need value → index.
* Need fast complement lookup.
* Need O(n) average time.
* Need to remember previously seen values.

# ------------------------------------------------------------

# WHEN NOT TO USE HASH MAP

# ------------------------------------------------------------

If the array is already sorted and the problem only asks
whether a pair exists, two pointers may be better.

Two pointers:

Time  = O(n)
Space = O(1)

# ------------------------------------------------------------

# COMMON OA TRAPS

# ------------------------------------------------------------

TRAP 1:

Using the same element twice.

Avoid by checking before storing.

TRAP 2:

Forgetting duplicate values can form the answer.

Example:

[3,3], target = 6

TRAP 3:

Using nested loops unnecessarily.

Brute force:

O(n²)

Optimal hash map:

O(n) average.

# ------------------------------------------------------------

# INTERVIEW EXPLANATION

# ------------------------------------------------------------

"I calculate the complement of each element as
target minus the current value. I store previously seen
values and their indices in a hash map. If the complement
already exists, I return its index and the current index.
This reduces the brute-force O(n²) solution to O(n)
average time."

# ------------------------------------------------------------

# MEMORY TRIGGER

# ------------------------------------------------------------

TWO SUM
↓
CURRENT
↓
NEED = TARGET - CURRENT
↓
HASH MAP
↓
FOUND?
├── YES → ANSWER
└── NO  → STORE

# ============================================================

# 5. PROBLEM 10 — PRINT ALL DUPLICATES

# ============================================================

## PROBLEM

Given an array of integers, find the values that occur more
than once.

Example:

Input:

[1, 2, 3, 2, 4, 1, 5]

Output:

[2, 1]

# ------------------------------------------------------------

# PATTERN

# ------------------------------------------------------------

DUPLICATES
↓
"Have I seen this before?"
↓
HASH SET

# ------------------------------------------------------------

# KEY OBSERVATION

# ------------------------------------------------------------

We don't need:

* index
* frequency initially
* ordering

We only need to know:

"Have I already encountered this value?"

A Hash Set is designed for exactly this.

# ------------------------------------------------------------

# DATA STRUCTURE

# ------------------------------------------------------------

unordered_set<int>

It stores unique values.

Example:

nums:

[1, 2, 3, 2]

After processing first three:

set = {1,2,3}

Next:

2

2 already exists.

Therefore:

2 = duplicate.

# ------------------------------------------------------------

# ALGORITHM

# ------------------------------------------------------------

1. Create empty set `seen`.

2. Traverse the array.

3. If current value is already in `seen`:
   add it to answer.

4. Otherwise:
   insert it into `seen`.

5. Return answer.

# ------------------------------------------------------------

# C++ SOLUTION

# ------------------------------------------------------------

```cpp
vector<int> duplicates(vector<int>& nums) {

    unordered_set<int> st;
    vector<int> ans;

    for (int x : nums) {

        if (st.find(x) != st.end()) {
            ans.push_back(x);
        }
        else {
            st.insert(x);
        }
    }

    return ans;
}
```

# ------------------------------------------------------------

# DRY RUN

# ------------------------------------------------------------

nums:

[1, 2, 3, 2, 4, 1, 5]

1:

not seen

store 1

2:

not seen

store 2

3:

not seen

store 3

2:

already seen

answer:

[2]

4:

not seen

store 4

1:

already seen

answer:

[2,1]

5:

not seen

store 5

Final:

[2,1]

# ------------------------------------------------------------

# IMPORTANT DISTINCTION

# ------------------------------------------------------------

The above implementation adds a value EVERY TIME it appears
after its first occurrence.

Example:

[1,1,1,2]

Output:

[1,1]

Why?

First 1:
store

Second 1:
duplicate → add

Third 1:
duplicate → add

# ------------------------------------------------------------

# IF UNIQUE DUPLICATES ARE REQUIRED

# ------------------------------------------------------------

If the question asks:

"Return each duplicate value only once."

Then use another set.

Example:

[1,1,1,2,2]

Expected:

[1,2]

Possible solution:

```cpp
vector<int> duplicates(vector<int>& nums) {

    unordered_set<int> seen;
    unordered_set<int> added;

    vector<int> ans;

    for (int x : nums) {

        if (seen.count(x)) {

            if (!added.count(x)) {
                ans.push_back(x);
                added.insert(x);
            }

        } else {
            seen.insert(x);
        }
    }

    return ans;
}
```

# ------------------------------------------------------------

# COMPLEXITY

# ------------------------------------------------------------

Time:

O(n) average

Space:

O(n)

# ------------------------------------------------------------

# HASH SET VS HASH MAP

# ------------------------------------------------------------

HASH SET:

Question:

"Does this value exist?"

↓

unordered_set

HASH MAP:

Question:

"What information is associated with this value?"

↓

unordered_map

Examples:

Duplicates:

value → existence

Use:

Hash Set

Two Sum:

value → index

Use:

Hash Map

# ------------------------------------------------------------

# WHEN TO USE HASH SET

# ------------------------------------------------------------

Think Hash Set when you see:

* duplicate
* repeated
* already seen
* exists
* membership
* distinct elements
* detect repetition

# ------------------------------------------------------------

# WHEN NOT TO USE HASH SET

# ------------------------------------------------------------

If the problem asks:

* How many times?
* Frequency
* Index
* Value → another value

then Hash Map / frequency array may be more suitable.

# ------------------------------------------------------------

# COMMON OA TRAPS

# ------------------------------------------------------------

TRAP 1:

Confusing duplicate occurrence with unique duplicate value.

TRAP 2:

Using a map when only existence is required.

TRAP 3:

Forgetting that unordered_set gives O(1) average lookup,
not guaranteed O(1) worst case.

# ------------------------------------------------------------

# INTERVIEW EXPLANATION

# ------------------------------------------------------------

"I only need to know whether a value has appeared before,
so I use a hash set. While traversing the array, if the
current value is already present in the set, it is a
duplicate; otherwise I insert it."

# ------------------------------------------------------------

# MEMORY TRIGGER

# ------------------------------------------------------------

DUPLICATE
↓
SEEN BEFORE?
↓
HASH SET

# ============================================================

# 6. PROBLEM 11 — FIND MISSING NUMBER

# ============================================================

## PROBLEM

Given an array containing `n` distinct numbers taken from
the range:

0 to n

return the one missing number.

Example:

Input:

[3, 0, 1]

Output:

2

# ------------------------------------------------------------

# PATTERN

# ------------------------------------------------------------

MISSING NUMBER
↓
KNOWN RANGE 0...n
↓
ONE VALUE MISSING
↓
XOR CANCELLATION
↓
XOR

# ------------------------------------------------------------

# KEY OBSERVATION

# ------------------------------------------------------------

XOR has two extremely important properties:

x ^ x = 0

x ^ 0 = x

Therefore:

0 ^ 1 ^ 2 ^ 3
^
3 ^ 0 ^ 1

Common values cancel.

Remaining:

2

# ------------------------------------------------------------

# WHY XOR?

# ------------------------------------------------------------

Expected:

0, 1, 2, ..., n

Actual:

all except one.

If we XOR all expected values and all actual values:

Every present number occurs exactly twice.

Therefore:

x ^ x = 0

Only the missing number occurs once.

So it survives.

# ------------------------------------------------------------

# ALGORITHM

# ------------------------------------------------------------

1. Let:

   n = nums.size()

2. Initialize:

   ans = n

3. Traverse i from 0 to n-1.

4. XOR:

   ans ^= i
   ans ^= nums[i]

5. Return ans.

# ------------------------------------------------------------

# C++ SOLUTION

# ------------------------------------------------------------

```cpp
int missingNumber(vector<int>& nums) {

    int n = nums.size();

    int ans = n;

    for (int i = 0; i < n; i++) {

        ans ^= i;
        ans ^= nums[i];
    }

    return ans;
}
```

# ------------------------------------------------------------

# DRY RUN

# ------------------------------------------------------------

nums:

[3,0,1]

n = 3

Expected:

0 1 2 3

Actual:

3 0 1

Start:

ans = 3

i = 0:

ans ^= 0
ans ^= 3

i = 1:

ans ^= 1
ans ^= 0

i = 2:

ans ^= 2
ans ^= 1

Combined XOR:

3 ^ 0 ^ 3 ^ 1 ^ 0 ^ 2 ^ 1

Cancel:

3 ^ 3 = 0
0 ^ 0 = 0
1 ^ 1 = 0

Remaining:

2

Answer:

2

# ------------------------------------------------------------

# ALTERNATIVE — SUM FORMULA

# ------------------------------------------------------------

Expected sum:

n * (n + 1) / 2

Then:

missing = expectedSum - actualSum

Example:

n = 3

Expected:

3 * 4 / 2 = 6

Actual:

3 + 0 + 1 = 4

Missing:

6 - 4 = 2

But XOR has an advantage:

No sum overflow issue.

# ------------------------------------------------------------

# COMPLEXITY

# ------------------------------------------------------------

Time:

O(n)

Space:

O(1)

# ------------------------------------------------------------

# WHEN TO USE XOR

# ------------------------------------------------------------

Think XOR when:

* One number is missing.
* Values should occur in pairs.
* Every value except one occurs twice.
* Need cancellation of duplicates.
* Range is known.
* Need O(1) extra space.

# ------------------------------------------------------------

# WHEN NOT TO USE XOR

# ------------------------------------------------------------

Don't use XOR when:

* Multiple values are missing.
* Frequency of values is required.
* Values don't have a cancellation property.
* Order matters.
* You need all duplicates/frequencies.

# ------------------------------------------------------------

# XOR CORE PROPERTIES

# ------------------------------------------------------------

x ^ x = 0

x ^ 0 = x

a ^ b = b ^ a

(a ^ b) ^ c = a ^ (b ^ c)

The last two properties mean XOR can be rearranged.

That is why the expected and actual values can cancel.

# ------------------------------------------------------------

# COMMON OA TRAPS

# ------------------------------------------------------------

TRAP 1:

Forgetting that the range is:

0 to n

not:

0 to n-1

TRAP 2:

Using an integer sum when constraints may cause overflow.

TRAP 3:

Thinking XOR works for every missing-number problem.

It works because of the specific cancellation structure.

# ------------------------------------------------------------

# INTERVIEW EXPLANATION

# ------------------------------------------------------------

"The array should contain every number from 0 to n exactly
once except one. I XOR all expected numbers with all numbers
present in the array. Every number that exists cancels because
x XOR x is zero, leaving only the missing number. This gives
O(n) time and O(1) extra space."

# ------------------------------------------------------------

# MEMORY TRIGGER

# ------------------------------------------------------------

MISSING NUMBER
↓
0...n
↓
XOR EXPECTED + ACTUAL
↓
PAIRS CANCEL
↓
MISSING SURVIVES

# ============================================================

# 7. PROBLEM 12 — REMOVE DUPLICATES FROM SORTED ARRAY

# ============================================================

## PROBLEM

Given a sorted array, remove duplicates in-place such that
each unique element appears only once.

Return the number `k` of unique elements.

The first `k` positions of the array must contain the
unique values.

Example:

Input:

[1,1,2]

Output:

k = 2

Modified array:

[1,2,...]

# ------------------------------------------------------------

# PATTERN

# ------------------------------------------------------------

SORTED ARRAY
↓
DUPLICATES ARE ADJACENT
↓
TWO POINTERS
↓
LEFT = LAST UNIQUE
RIGHT = SCANNER

# ------------------------------------------------------------

# KEY OBSERVATION

# ------------------------------------------------------------

Because the array is sorted:

[1,1,2,2,3,3,4]

duplicates are next to each other.

Therefore, we don't need a HashSet.

We only need to compare:

nums[left]

with:

nums[right]

# ------------------------------------------------------------

# POINTER MEANING

# ------------------------------------------------------------

LEFT:

Position of the last unique element.

RIGHT:

Current element being examined.

Mental model:

[ UNIQUE VALUES ][ unexplored values ]
↑                 ↑
left             right

# ------------------------------------------------------------

# ALGORITHM

# ------------------------------------------------------------

1. If array is empty:
   return 0.

2. Set:

   left = 0
   right = 1

3. Move right through the array.

4. If:

   nums[left] != nums[right]

   then a new unique value is found.

5. Move left:

   left++

6. Copy:

   nums[left] = nums[right]

7. Continue.

8. Return:

   left + 1

# ------------------------------------------------------------

# C++ SOLUTION

# ------------------------------------------------------------

```cpp
int removeDuplicates(vector<int>& nums) {

    int n = nums.size();

    if (n == 0)
        return 0;

    int left = 0;

    for (int right = 1; right < n; right++) {

        if (nums[left] != nums[right]) {

            left++;

            nums[left] = nums[right];
        }
    }

    return left + 1;
}
```

# ------------------------------------------------------------

# DRY RUN

# ------------------------------------------------------------

nums:

[1,1,2,2,3]

Initial:

left = 0
right = 1

Array:

[1,1,2,2,3]
↑ ↑
L R

1 == 1

Duplicate.

Move right.

Now:

[1,1,2,2,3]
↑   ↑
L   R

1 != 2

New unique value.

left++

left = 1

Write:

nums[1] = nums[2]

Array becomes:

[1,2,2,2,3]

Move right.

Now:

[1,2,2,2,3]
↑   ↑
L   R

2 == 2

Duplicate.

Skip.

Next:

2 != 3

Move left:

left = 2

Write:

nums[2] = 3

Array:

[1,2,3,2,3]

Valid portion:

[1,2,3]

Return:

left + 1

= 3

# ------------------------------------------------------------

# IMPORTANT IN-PLACE CONCEPT

# ------------------------------------------------------------

The problem does NOT require physically shrinking the vector.

Only the first `k` elements matter.

Example:

Original:

[1,1,2,2,3]

After processing:

[1,2,3,2,3]

k = 3

Only:

[1,2,3]

is considered the valid result.

# ------------------------------------------------------------

# WHY left + 1?

# ------------------------------------------------------------

left is an INDEX.

If:

left = 0

then:

1 unique element exists.

If:

left = 1

then:

2 unique elements exist.

Therefore:

number of unique elements = left + 1

# ------------------------------------------------------------

# EDGE CASES

# ------------------------------------------------------------

Empty:

[]

→ 0

One element:

[5]

→ 1

All duplicates:

[2,2,2,2]

→ 1

No duplicates:

[1,2,3,4]

→ 4

# ------------------------------------------------------------

# COMPLEXITY

# ------------------------------------------------------------

Time:

O(n)

Space:

O(1)

# ------------------------------------------------------------

# WHY NOT HASH SET?

# ------------------------------------------------------------

A HashSet could detect duplicates.

But the array is already sorted.

Using a HashSet would require:

O(n) extra space.

Two pointers achieve:

O(1) extra space.

# ------------------------------------------------------------

# WHEN TO USE TWO POINTERS

# ------------------------------------------------------------

Think Two Pointers when:

* Array is sorted.
* Need to remove duplicates.
* Need in-place modification.
* Need to compare positions.
* Need to process from both ends.
* Need read/write positions.

# ------------------------------------------------------------

# WHEN NOT TO USE THIS EXACT APPROACH

# ------------------------------------------------------------

Do NOT use this approach if the array is unsorted.

Example:

[1,3,2,1,3]

Duplicates are not adjacent.

Use:

Hash Set

or sort first, depending on requirements.

# ------------------------------------------------------------

# IMPORTANT CONNECTION

# ------------------------------------------------------------

PROBLEM 10:

Unsorted duplicate detection

↓

HASH SET

PROBLEM 12:

Sorted duplicate removal

↓

TWO POINTERS

The sorted property changes the optimal strategy.

# ------------------------------------------------------------

# COMMON OA TRAPS

# ------------------------------------------------------------

TRAP 1:

Forgetting the array must be sorted.

TRAP 2:

Returning the vector instead of returning k.

TRAP 3:

Returning `left` instead of `left + 1`.

TRAP 4:

Creating a new array when the problem asks for in-place
modification.

TRAP 5:

Trying to erase elements from the vector repeatedly.

That can make the solution unnecessarily expensive.

# ------------------------------------------------------------

# INTERVIEW EXPLANATION

# ------------------------------------------------------------

"Because the array is sorted, duplicates are adjacent.
I maintain a left pointer at the last unique element and
a right pointer that scans the array. Whenever I find a new
unique value, I advance left and overwrite that position
with the current value. This modifies the array in-place
using O(1) extra space."

# ------------------------------------------------------------

# MEMORY TRIGGER

# ------------------------------------------------------------

SORTED
↓
DUPLICATES ADJACENT
↓
TWO POINTERS
↓
LEFT = LAST UNIQUE
RIGHT = SCANNER
↓
DIFFERENT?
├── YES → WRITE
└── NO  → SKIP

# ============================================================

# 8. PROBLEM 13 — COMMON ELEMENTS IN THREE SORTED ARRAYS

# ============================================================

## PROBLEM

Given three sorted arrays, find the elements that are
common to all three arrays.

Example:

A = [1,5,10,20,40,80]

B = [6,7,20,80,100]

C = [3,4,15,20,30,70,80,120]

Output:

[20,80]

# ------------------------------------------------------------

# PATTERN

# ------------------------------------------------------------

THREE SORTED ARRAYS
↓
THREE POINTERS
↓
i, j, k
↓
ALL EQUAL?
↓
FOUND

Otherwise:

MOVE THE SMALLEST VALUE

# ------------------------------------------------------------

# KEY OBSERVATION

# ------------------------------------------------------------

All arrays are sorted.

Therefore, if:

A[i] < B[j]

then A[i] cannot match B[j] or C[k] at the current positions.

We need to advance A.

General rule:

THE SMALLEST CURRENT VALUE
↓
MOVE THAT POINTER

# ------------------------------------------------------------

# POINTERS

# ------------------------------------------------------------

i → A

j → B

k → C

At any point:

A[i]
B[j]
C[k]

# ------------------------------------------------------------

# CASE 1 — ALL THREE EQUAL

# ------------------------------------------------------------

If:

A[i] == B[j]
AND
B[j] == C[k]

then:

A[i] is common to all three.

Add it:

ans.push_back(A[i])

Then:

i++
j++
k++

# ------------------------------------------------------------

# CASE 2 — A IS SMALLEST

# ------------------------------------------------------------

If:

A[i] < B[j]

then:

i++

Why?

Because A[i] is smaller than an element in B.

Since B is sorted, moving B forward cannot make it
smaller.

Therefore A[i] can never become common at these positions.

Move A.

# ------------------------------------------------------------

# CASE 3 — B IS SMALLEST

# ------------------------------------------------------------

If:

B[j] < C[k]

then:

j++

# ------------------------------------------------------------

# CASE 4 — C IS SMALLEST

# ------------------------------------------------------------

Otherwise:

k++

# ------------------------------------------------------------

# ALGORITHM

# ------------------------------------------------------------

1. Set:

   i = 0
   j = 0
   k = 0

2. Continue while all three pointers are valid.

3. If all three values are equal:
   add to answer
   increment all three.

4. Otherwise:
   move the pointer pointing to the smallest value.

5. Return answer.

# ------------------------------------------------------------

# C++ SOLUTION

# ------------------------------------------------------------

```cpp
vector<int> commonElements(
    vector<int>& A,
    vector<int>& B,
    vector<int>& C
) {

    int i = 0;
    int j = 0;
    int k = 0;

    vector<int> ans;

    while (i < A.size() &&
           j < B.size() &&
           k < C.size()) {

        if (A[i] == B[j] &&
            B[j] == C[k]) {

            ans.push_back(A[i]);

            i++;
            j++;
            k++;
        }
        else if (A[i] < B[j]) {

            i++;
        }
        else if (B[j] < C[k]) {

            j++;
        }
        else {

            k++;
        }
    }

    return ans;
}
```

# ------------------------------------------------------------

# DRY RUN

# ------------------------------------------------------------

A:

[1,5,10,20,40,80]

B:

[6,7,20,80,100]

C:

[3,4,15,20,30,70,80,120]

Initial:

i = 0
j = 0
k = 0

Current values:

A[i] = 1
B[j] = 6
C[k] = 3

Smallest:

1

Therefore:

i++

Now:

5, 6, 3

Smallest:

3

Therefore:

k++

Now:

5, 6, 4

Smallest:

4

Therefore:

k++

Now:

5, 6, 15

Smallest:

5

Therefore:

i++

Now:

10, 6, 15

Smallest:

6

Therefore:

j++

Now:

10, 7, 15

Smallest:

7

Therefore:

j++

Now:

10, 20, 15

Smallest:

10

Therefore:

i++

Now:

20, 20, 15

Smallest:

15

Therefore:

k++

Now:

20, 20, 20

ALL EQUAL.

Add:

20

Move all:

i++
j++
k++

Eventually:

80,80,80

ALL EQUAL.

Add:

80

Final:

[20,80]

# ------------------------------------------------------------

# WHY MOVE THE SMALLEST?

# ------------------------------------------------------------

Suppose:

A[i] = 5
B[j] = 10
C[k] = 15

Can 5 be common?

No.

B and C currently have values greater than 5.

Because they are sorted, moving B or C forward will only
increase their values.

Therefore the only useful move is:

5 → next value

This is the core reasoning.

# ------------------------------------------------------------

# COMPLEXITY

# ------------------------------------------------------------

Let:

n = A.size()
m = B.size()
p = C.size()

Each pointer moves only forward.

Therefore:

Time:

O(n + m + p)

Extra Space:

O(1)

excluding output.

# ------------------------------------------------------------

# IMPORTANT ASSUMPTION

# ------------------------------------------------------------

The arrays MUST be sorted.

Without sorting, the pointer elimination logic is invalid.

# ------------------------------------------------------------

# DUPLICATE ISSUE

# ------------------------------------------------------------

If arrays can contain duplicates:

A = [1,5,5,10]

B = [5,5,20]

C = [5,5,30]

The simple implementation may produce:

[5,5]

If the question asks for UNIQUE common elements:

[5]

then prevent repeated insertion.

Example:

```cpp
if (A[i] == B[j] &&
    B[j] == C[k]) {

    if (ans.empty() || ans.back() != A[i]) {
        ans.push_back(A[i]);
    }

    i++;
    j++;
    k++;
}
```

Only add this logic if the problem requires unique output
or duplicates are allowed.

# ------------------------------------------------------------

# WHEN TO USE THREE POINTERS

# ------------------------------------------------------------

Think multiple pointers when:

* Multiple arrays are sorted.
* Need intersection.
* Need common elements.
* Need merge-like traversal.
* Need compare values across sorted arrays.
* Sorted order can eliminate candidates.

# ------------------------------------------------------------

# WHEN NOT TO USE THREE POINTERS

# ------------------------------------------------------------

Don't use this approach when:

* Arrays are unsorted.
* Ordering provides no useful information.
* You need frequency rather than simple intersection.

For unsorted arrays, Hash Set / Hash Map may be more appropriate.

# ------------------------------------------------------------

# IMPORTANT CONNECTION

# ------------------------------------------------------------

TWO SORTED ARRAYS

↓

TWO POINTERS

THREE SORTED ARRAYS

↓

THREE POINTERS

The general principle is:

USE SORTED ORDER TO ELIMINATE IMPOSSIBLE VALUES.

# ------------------------------------------------------------

# COMMON OA TRAPS

# ------------------------------------------------------------

TRAP 1:

Forgetting that arrays must be sorted.

TRAP 2:

Moving the wrong pointer.

Always move the pointer pointing to the smallest value.

TRAP 3:

Moving only one pointer when all three are equal.

If:

A[i] == B[j] == C[k]

move:

i++
j++
k++

TRAP 4:

Ignoring duplicate-output requirements.

# ------------------------------------------------------------

# INTERVIEW EXPLANATION

# ------------------------------------------------------------

"Since all three arrays are sorted, I maintain one pointer
for each array. If all three current values are equal, that
value is common to all arrays, so I add it and move all
three pointers. Otherwise, I move the pointer pointing to
the smallest value because that value cannot match either
of the larger current values. Each pointer traverses its
array at most once, giving O(n+m+p) time."

# ------------------------------------------------------------

# MEMORY TRIGGER

# ------------------------------------------------------------

3 SORTED ARRAYS
↓
3 POINTERS
↓
ALL EQUAL?
├── YES → ADD + MOVE ALL
└── NO
↓
MOVE SMALLEST

# ============================================================

# 9. CONNECTIONS BETWEEN ALL 5 PROBLEMS

# ============================================================

# ------------------------------------------------------------

# CONNECTION 1 — HASHING

# ------------------------------------------------------------

TWO SUM

value → index

↓

HASH MAP

DUPLICATES

value → existence

↓

HASH SET

The important distinction:

Need associated information?

→ HASH MAP

Need only existence?

→ HASH SET

# ------------------------------------------------------------

# CONNECTION 2 — SORTED ARRAYS

# ------------------------------------------------------------

REMOVE DUPLICATES

SORTED
↓
TWO POINTERS

COMMON THREE ARRAYS

SORTED
↓
THREE POINTERS

The bigger concept:

SORTED ORDER
↓
ELIMINATE IMPOSSIBLE CANDIDATES

# ------------------------------------------------------------

# CONNECTION 3 — XOR

# ------------------------------------------------------------

MISSING NUMBER

EXPECTED VALUES
+
ACTUAL VALUES
↓
XOR
↓
PAIRS CANCEL
↓
MISSING SURVIVES

# ============================================================

# 10. MASTER DATA STRUCTURE CHEAT SHEET

# ============================================================

QUESTION
│
├── Need value → index?
│      ↓
│   HASH MAP
│
├── Need only "have I seen this?"
│      ↓
│   HASH SET
│
├── One number missing from known range?
│      ↓
│   XOR
│
├── Sorted array + remove duplicates?
│      ↓
│   TWO POINTERS
│
├── Sorted arrays + common values?
│      ↓
│   MULTIPLE POINTERS
│
└── Need in-place modification?
↓
READ + WRITE POINTERS

# ============================================================

# 11. WHEN TO USE WHAT?

# ============================================================

## HASH MAP

Use when:

* Need key → value.
* Need value → index.
* Need frequency.
* Need complement lookup.
* Need fast average lookup.

Examples:

* Two Sum
* Frequency counting
* Grouping

## HASH SET

Use when:

* Only existence matters.
* Need duplicate detection.
* Need membership checking.
* Need distinct values.
* Need fast average lookup.

Examples:

* Print Duplicates
* Dictionary membership
* Duplicate detection

## XOR

Use when:

* One number is missing.
* Duplicate values cancel.
* Every other value appears twice.
* Need O(1) extra space.

Example:

* Missing Number

## TWO POINTERS

Use when:

* Array/string is sorted.
* Need in-place modification.
* Working from both ends.
* Need remove duplicates.
* Need pair search in sorted data.

Examples:

* Two Sum sorted version
* Remove Duplicates
* Reverse

## THREE / MULTIPLE POINTERS

Use when:

* Multiple arrays are sorted.
* Need common/intersection values.
* Need simultaneous traversal.
* Sorted order allows elimination.

Example:

* Common Elements in Three Sorted Arrays

# ============================================================

# 12. WHEN NOT TO USE WHAT

# ============================================================

## DON'T USE HASH MAP AUTOMATICALLY

If you only need:

"Have I seen this?"

Use:

HASH SET

Don't store unnecessary information.

## DON'T USE HASH SET FOR FREQUENCY

If the problem asks:

"How many times does each value occur?"

Use:

HASH MAP

or:

FREQUENCY ARRAY

## DON'T USE TWO POINTERS ON UNSORTED DATA

The pointer elimination logic usually depends on sorted order.

If unsorted:

Consider:

* Hashing
* Sorting first
* Another appropriate technique

## DON'T USE XOR RANDOMLY

XOR is powerful but only when its cancellation property
matches the problem structure.

## DON'T USE THREE POINTERS WITHOUT SORTING

The "move the smallest" logic requires sorted arrays.

# ============================================================

# 13. COMMON OA TRAPS

# ============================================================

## TRAP 1 — TWO SUM

Question:

Can the same element be used twice?

Answer:

NO.

Check complement before storing current element.

## TRAP 2 — DUPLICATES

Question:

Does the answer want:

* Every repeated occurrence?

OR:

* Each duplicate value only once?

Read the wording carefully.

## TRAP 3 — MISSING NUMBER

Remember the range:

0 to n

There are:

n + 1 possible values.

## TRAP 4 — REMOVE DUPLICATES

The array must be sorted.

Also:

Return `k`.

Don't return the vector unless the problem explicitly asks for it.

## TRAP 5 — REMOVE DUPLICATES

Only the first `k` elements matter.

Elements after index `k-1` are irrelevant.

## TRAP 6 — COMMON THREE ARRAYS

When all three values are equal:

Move ALL THREE.

## TRAP 7 — COMMON THREE ARRAYS

When values differ:

Move the pointer containing the SMALLEST value.

## TRAP 8 — HASHING COMPLEXITY

`unordered_map` and `unordered_set` provide:

O(1) average

not guaranteed O(1) worst-case.

# ============================================================

# 14. INTERVIEW EXPLANATION TEMPLATES

# ============================================================

## TWO SUM

"I calculate the complement as target minus the current
element. I store previously seen values and their indices
in a hash map. If the complement exists, I have found the
required pair. This gives O(n) average time."

## PRINT DUPLICATES

"I only need to know whether each value has appeared before,
so I use a hash set. If the current value is already in the
set, it is a duplicate; otherwise I insert it."

## MISSING NUMBER

"I XOR all values from 0 to n with all values present in
the array. Every present value appears twice and cancels,
leaving only the missing value."

## REMOVE DUPLICATES

"Because the array is sorted, duplicates are adjacent.
I use a slow pointer for the last unique element and a fast
pointer to scan the array. When a new value appears, I write
it after the previous unique value."

## COMMON THREE ARRAYS

"Since all three arrays are sorted, I maintain one pointer
for each array. If all three values match, I add the value.
Otherwise, I advance the pointer with the smallest value
because it cannot match the larger values without moving
forward."

# ============================================================

# 15. MASTER STORY → PATTERN CHEAT SHEET

# ============================================================

STORY
│
├── "Find two values whose sum is target"
│      ↓
│   NEED = TARGET - CURRENT
│      ↓
│   HASH MAP
│
├── "Find repeated values"
│      ↓
│   HAVE I SEEN THIS?
│      ↓
│   HASH SET
│
├── "One number missing from 0...n"
│      ↓
│   XOR
│
├── "Remove duplicates from SORTED array"
│      ↓
│   TWO POINTERS
│
└── "Find common elements in THREE SORTED arrays"
↓
THREE POINTERS
↓
MOVE SMALLEST

# ============================================================

# 16. FIVE-PROBLEM PATTERN MAP

# ============================================================

```
                ARRAYS
                   │
      ┌────────────┴────────────┐
      │                         │
   HASHING                    SORTED
      │                         │
 ┌────┴────┐              ┌─────┴─────┐
 │         │              │           │
```

Two Sum   Duplicates    Remove Dup.   Common 3
│         │              │           │
Hash Map  Hash Set       2 Pointer    3 Pointer
│         │              │           │
value→idx  seen?         left/right    i/j/k
│
↓
move smallest

```
                SPECIAL
                   │
                   ↓
             Missing Number
                   │
                   ↓
                  XOR
```

# ============================================================

# 17. ULTRA-SHORT OA CHEAT SHEET

# ============================================================

## TWO SUM

Unsorted:

Hash Map

```cpp
need = target - nums[i];

if (mp.count(need))
    answer;

mp[nums[i]] = i;
```

## DUPLICATES

Need existence:

Hash Set

```cpp
if (st.count(x))
    duplicate;
else
    st.insert(x);
```

## MISSING NUMBER

Range:

0...n

Use XOR:

```cpp
int ans = n;

for (int i = 0; i < n; i++) {
    ans ^= i;
    ans ^= nums[i];
}

return ans;
```

## REMOVE DUPLICATES

Sorted:

Two pointers

```cpp
int left = 0;

for (int right = 1; right < n; right++) {

    if (nums[left] != nums[right]) {
        left++;
        nums[left] = nums[right];
    }
}

return left + 1;
```

## COMMON THREE ARRAYS

Sorted:

Three pointers

```cpp
while (i < A.size() &&
       j < B.size() &&
       k < C.size()) {

    if (A[i] == B[j] &&
        B[j] == C[k]) {

        ans.push_back(A[i]);

        i++;
        j++;
        k++;
    }
    else if (A[i] < B[j]) {
        i++;
    }
    else if (B[j] < C[k]) {
        j++;
    }
    else {
        k++;
    }
}
```

# ============================================================

# 18. FINAL COMPLEXITY TABLE

# ============================================================

| #  | Problem              | Pattern        | Time     | Space |
| -- | -------------------- | -------------- | -------- | ----- |
| 9  | Two Sum              | Hash Map       | O(n) avg | O(n)  |
| 10 | Print All Duplicates | Hash Set       | O(n) avg | O(n)  |
| 11 | Missing Number       | XOR            | O(n)     | O(1)  |
| 12 | Remove Duplicates    | Two Pointers   | O(n)     | O(1)  |
| 13 | Common 3 Arrays      | Three Pointers | O(n+m+p) | O(1)* |

*excluding output.

# ============================================================

# 19. FINAL PATTERN RECOGNITION

# ============================================================

When you see...

---

"PAIR + TARGET"

↓

Ask:

Is array sorted?

YES
→ TWO POINTERS

NO
→ HASH MAP

---

"DUPLICATES"

↓

Ask:

Only existence?

→ HASH SET

Frequency?

→ HASH MAP / FREQUENCY ARRAY

---

"MISSING NUMBER"

↓

Known range 0...n?

↓

XOR

---

"SORTED + REMOVE DUPLICATES"

↓

TWO POINTERS

---

"COMMON IN MULTIPLE SORTED ARRAYS"

↓

MULTIPLE POINTERS

---

"SMALLEST CURRENT VALUE"

↓

MOVE THAT POINTER

# ============================================================

# 20. FINAL MEMORY MAP

# ============================================================

ARRAY
│
├── PAIR + TARGET
│      ↓
│   COMPLEMENT
│      ↓
│   HASH MAP
│
├── DUPLICATES
│      ↓
│   SEEN?
│      ↓
│   HASH SET
│
├── ONE MISSING
│      ↓
│   XOR
│
├── SORTED + REMOVE
│      ↓
│   TWO POINTERS
│
└── SORTED + COMMON
↓
THREE POINTERS
↓
MOVE SMALLEST

# ============================================================

# 21. 10-SECOND OA DECISION TREE

# ============================================================

START
│
↓
Is it about a PAIR?
│
├── YES → Is array sorted?
│             │
│             ├── YES → TWO POINTERS
│             └── NO  → HASH MAP
│
↓
Is it about DUPLICATES?
│
├── YES → Need only existence?
│             │
│             └── YES → HASH SET
│
↓
Is ONE NUMBER MISSING from a known range?
│
└── YES → XOR
│
↓
Is array SORTED?
│
├── YES → Need remove duplicates?
│             │
│             └── YES → TWO POINTERS
│
↓
Are MULTIPLE arrays SORTED?
│
└── YES → MULTIPLE POINTERS

# ============================================================

# 22. MOST IMPORTANT THINGS TO REMEMBER

# ============================================================

1. TWO SUM

Current + Need = Target

Need:

target - current

Unsorted:

Hash Map

2. DUPLICATES

"Have I seen this?"

Hash Set.

3. MISSING NUMBER

Expected + Actual

XOR everything.

Pairs cancel.

4. REMOVE DUPLICATES

Sorted means duplicates are adjacent.

Use:

Two Pointers.

5. COMMON THREE ARRAYS

All sorted.

Use:

Three Pointers.

If not equal:

Move the smallest.

# ============================================================

# 23. FINAL MASTER CHEAT SHEET

# ============================================================

┌─────────────────────────────────────────────────────────┐
│                 ARRAY PATTERN RECOGNITION               │
├─────────────────────────────────────────────────────────┤
│                                                         │
│ Pair + Target                                           │
│       ↓                                                 │
│ Unsorted → Hash Map                                     │
│ Sorted   → Two Pointers                                │
│                                                         │
│ Duplicate Detection                                     │
│       ↓                                                 │
│ Hash Set                                                 │
│                                                         │
│ Missing from 0...n                                      │
│       ↓                                                 │
│ XOR                                                      │
│                                                         │
│ Sorted + Remove Duplicates                             │
│       ↓                                                 │
│ Two Pointers                                             │
│                                                         │
│ Multiple Sorted Arrays + Common Elements               │
│       ↓                                                 │
│ Multiple Pointers                                       │
│       ↓                                                 │
│ Move Smallest                                           │
│                                                         │
└─────────────────────────────────────────────────────────┘

# ============================================================

# FINAL ONE-LINE MEMORY

# ============================================================

TWO SUM
→ COMPLEMENT → HASH MAP

DUPLICATES
→ SEEN? → HASH SET

MISSING
→ CANCEL → XOR

SORTED + REMOVE
→ UNIQUE + SCAN → TWO POINTERS

SORTED + COMMON
→ COMPARE → MOVE SMALLEST

```

This gives you the same **pattern-first style** as the attached String notebook, rather than just five isolated solutions. The attached format explicitly emphasizes pattern recognition, data-structure choice, complexity, traps, and interview explanations, which I've preserved here. :contentReference[oaicite:1]{index=1}

**Arrays/Hashing 9–13 is now a proper revision notebook, not just a problem list.**
```
