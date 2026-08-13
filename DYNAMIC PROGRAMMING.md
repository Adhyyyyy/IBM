Absolutely, ADHY. You want **one single Markdown code block**, so the UI gives you **one Copy button** and you can copy the entire Set 7 at once.

````markdown
# IBM OA — 96 PROBLEM MASTER PLAN
# SET 7 — DYNAMIC PROGRAMMING
# PROBLEMS #79–#87


# SET 7 — EXACT PROBLEM LIST

[ ] #79 Climbing Stairs
[ ] #80 House Robber
[ ] #81 Coin Change
[ ] #82 0/1 Knapsack
[ ] #83 Longest Increasing Subsequence
[ ] #84 Longest Common Subsequence
[ ] #85 Edit Distance
[ ] #86 Decode Ways
[ ] #87 Word Break


# SET 7 — PURPOSE

The goal is NOT:

"Learn every type of DP."

The goal is:

MASTER THESE 9 PROBLEMS
        ↓
RECOGNIZE THE DP PATTERNS
        ↓
TRANSFER THE PATTERNS
        ↓
SOLVE IBM OA VARIANTS


# DP — CORE IDEA

DYNAMIC PROGRAMMING
│
├── Problem has
│      │
│      ├── Overlapping Subproblems
│      └── Optimal Substructure
│
├── Break problem
│      ↓
│    into smaller states
│
├── Solve each state
│      ↓
│    only once
│
└── Reuse the stored result


# FIRST QUESTION IN ANY DP PROBLEM

DO NOT START WITH:

"How do I code dp?"


START WITH:

"What does dp[i] mean?"


Example:

dp[i]
=
number of ways to reach i


or:

dp[i]
=
maximum money possible
up to i


or:

dp[i]
=
minimum coins needed
for amount i


or:

dp[i][j]
=
answer for first i elements
and first j elements


# DP THREE-STEP RULE

Before coding:

1. DEFINE STATE

2. FIND TRANSITION

3. DEFINE BASE CASE


Only then:

CODE.


# DP RECOGNITION

COUNT WAYS
     ↓
DP


MINIMUM / MAXIMUM
     ↓
DP candidate


LONGEST / SHORTEST
     ↓
DP candidate


CAN IT BE DONE?
     ↓
BOOLEAN DP candidate


REPEATED SUBPROBLEMS
     ↓
DP


# MEMOIZATION

TOP-DOWN

Problem
 ↓
Recursion
 ↓
Check if state already solved
 ↓
YES → return stored answer
 ↓
NO → solve
 ↓
store answer


Typical structure:

if(dp[state] != -1)
    return dp[state];

return dp[state] = solve(...);


# TABULATION

BOTTOM-UP

Base states
 ↓
smaller states
 ↓
larger states
 ↓
final answer


Typical structure:

dp[base] = ...;

for(...)
{
    dp[i] = ...;
}

return dp[n];


# MEMOIZATION vs TABULATION

MEMOIZATION
│
├── Top-down
├── Recursion
├── Store calculated states
└── Natural conversion from recursion


TABULATION
│
├── Bottom-up
├── Iterative
├── Build states in order
└── Usually avoids recursion overhead


# IMPORTANT

Do NOT memorize:

"DP = array"


DP is:

STATE
+
TRANSITION
+
BASE CASE
+
STORED RESULTS


# ============================================================
# #79 CLIMBING STAIRS
# ============================================================

CLIMBING STAIRS
│
├── Given n stairs
│
├── Can climb
│      ├── 1 step
│      └── 2 steps
│
└── Find number of ways
    to reach the top


# TRIGGER WORDS

"number of ways"

"1 or 2 steps"

"reach the top"


        ↓

CLIMBING STAIRS


# STATE

dp[i]

=

number of ways
to reach stair i


# THINK BACKWARD

To reach stair i:

I can come from:

i - 1

OR:

i - 2


Therefore:

dp[i]
=
dp[i-1]
+
dp[i-2]


# VISUAL

             i
            ↑
       ┌────┴────┐
       │         │
     i-1        i-2
       ↑         ↑
     1 step    2 steps


# BASE CASES

dp[1] = 1

Only:

1


dp[2] = 2

Ways:

1 + 1

2


# PATTERN

CLIMBING STAIRS
        ↓
FIBONACCI-LIKE
        ↓
PREVIOUS 2 STATES


# CODE

```cpp
int climbStairs(int n)
{
    if(n <= 2)
        return n;

    int prev2 = 1;
    int prev1 = 2;

    for(int i = 3; i <= n; i++)
    {
        int curr = prev1 + prev2;

        prev2 = prev1;
        prev1 = curr;
    }

    return prev1;
}
````

# COMPLEXITY

Time:

O(n)

Space:

O(1)

# CONNECTION

#79 CLIMBING STAIRS
↓
PREVIOUS STATES

#86 DECODE WAYS
↓
ONE / TWO CHARACTER CHOICES

These two problems are directly connected.

# COMMON TRAPS

[ ] Wrong base cases

[ ] Confusing stair number with array index

[ ] Returning Fibonacci value with wrong indexing

[ ] Using O(n) memory unnecessarily

# MENTAL SENTENCE

"To reach the current position,
look at the valid previous positions."

# ============================================================

# #80 HOUSE ROBBER

# ============================================================

HOUSE ROBBER
│
├── Houses have money
│
├── Cannot rob adjacent houses
│
└── Maximize money

# TRIGGER WORDS

"rob houses"

"no adjacent"

"maximum money"

```
    ↓
```

TAKE / SKIP DP

# CORE DECISION

At every house:

TAKE
OR
SKIP

# IF SKIP

Don't rob current.

Answer:

dp[i-1]

# IF TAKE

Rob current.

Cannot take previous.

Therefore:

nums[i]
+
dp[i-2]

# TRANSITION

dp[i]

=

max(

```
dp[i-1],

nums[i] + dp[i-2]
```

)

# VISUAL

HOUSE i

```
   ┌──────────────┐
   │              │
 SKIP            TAKE
   │              │
```

dp[i-1]      nums[i] + dp[i-2]

# STATE

dp[i]

=

maximum money
using houses up to i

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

# CODE

```cpp
int rob(vector<int>& nums)
{
    int prev2 = 0;
    int prev1 = 0;

    for(int money : nums)
    {
        int curr =
            max(prev1,
                prev2 + money);

        prev2 = prev1;
        prev1 = curr;
    }

    return prev1;
}
```

# COMPLEXITY

Time:

O(n)

Space:

O(1)

# CONNECTION

CLIMBING STAIRS
↓
PREVIOUS STATES

HOUSE ROBBER
↓
PREVIOUS STATES
+
TAKE / SKIP

# IMPORTANT DIFFERENCE

Climbing Stairs asks:

"How many ways?"

House Robber asks:

"What is the maximum?"

Same DP framework.

Different operation:

SUM
vs
MAX

# MENTAL SENTENCE

"At every item, decide:

TAKE
or
SKIP."

This pattern will return in:

#82 0/1 Knapsack

# COMMON TRAPS

[ ] Taking current + previous

[ ] Wrong i-2 transition

[ ] Confusing skip with take

[ ] Forgetting single-house case

# ============================================================

# #81 COIN CHANGE

# ============================================================

COIN CHANGE
│
├── Given coin denominations
│
├── Given amount
│
└── Find minimum number
of coins

# TRIGGER WORDS

"minimum coins"

"minimum number of coins"

"amount"

```
    ↓
```

COIN CHANGE

# STATE

dp[x]

=

minimum number of coins
needed to make amount x

# BASE

dp[0] = 0

Why?

Zero coins are needed
to make amount zero.

# TRANSITION

Suppose current coin:

coin

Remaining amount:

x - coin

If we use this coin:

dp[x]

=

dp[x-coin] + 1

Try every coin.

Take minimum.

Therefore:

# dp[x]

min(
dp[x-coin] + 1
)

for all valid coins.

# EXAMPLE

coins:

[1,2,5]

amount:

5

Possibilities:

5
→ 1 coin

2 + 2 + 1
→ 3 coins

1 + 1 + 1 + 1 + 1
→ 5 coins

Answer:

1

# IMPORTANT DIFFERENCE

HOUSE ROBBER:

Item cannot necessarily be reused.

COIN CHANGE:

A coin can generally be reused.

Example:

coin = 2

For amount 6:

2 + 2 + 2

Same coin:

multiple times.

This is:

UNBOUNDED CHOICE

# CODE

```cpp
int coinChange(vector<int>& coins, int amount)
{
    const int INF = 1e9;

    vector<int> dp(amount + 1, INF);

    dp[0] = 0;

    for(int x = 1; x <= amount; x++)
    {
        for(int coin : coins)
        {
            if(x >= coin)
            {
                dp[x] =
                    min(dp[x],
                        dp[x - coin] + 1);
            }
        }
    }

    return dp[amount] == INF
           ? -1
           : dp[amount];
}
```

# COMPLEXITY

Time:

O(amount × number of coins)

Space:

O(amount)

# CONNECTION

CLIMBING STAIRS
↓
CURRENT STATE
↓
PREVIOUS STATES

COIN CHANGE
↓
CURRENT AMOUNT
↓
SMALLER AMOUNT

# BIG DIFFERENCE

CLIMBING STAIRS:

Fixed possible moves:

1
2

COIN CHANGE:

Possible moves:

coin values.

Therefore:

GENERALIZED POSITION DP.

# MENTAL SENTENCE

"For the current amount,
try every coin and take
the best valid previous answer."

# COMMON TRAPS

[ ] Forgetting dp[0] = 0

[ ] Returning INF instead of -1

[ ] Not checking x >= coin

[ ] Confusing Coin Change with 0/1 Knapsack

[ ] Assuming greedy always works

# GREEDY CONNECTION

Coin Change may look greedy:

"Take the largest coin first."

But arbitrary coin systems can make greedy fail.

Example:

coins:

[1,3,4]

amount:

6

Greedy:

4 + 1 + 1

=

3 coins

Optimal:

3 + 3

=

2 coins

Therefore:

COIN CHANGE
↓
DP

# ============================================================

# #82 0/1 KNAPSACK

# ============================================================

0/1 KNAPSACK
│
├── Items
│      ├── weight
│      └── value
│
├── Capacity
│
├── Each item:
│      ├── TAKE
│      └── SKIP
│
└── Each item used
AT MOST ONCE

# TRIGGER WORDS

"maximum value"

"capacity"

"weight"

"each item once"

```
    ↓
```

0/1 KNAPSACK

# WHY "0/1"?

Each item has two possibilities:

0

→ don't take

1

→ take

Therefore:

0/1

# STATE

dp[i][w]

=

maximum value using
the first i items
with capacity w

# CHOICE

For item i:

SKIP

OR

TAKE

# SKIP

dp[i-1][w]

# TAKE

If:

weight[i] <= w

then:

value[i]
+
dp[i-1][w-weight[i]]

Why i-1?

Because:

item can only be used once.

# TRANSITION

dp[i][w]

=

max(

```
dp[i-1][w],

value[i]
+
dp[i-1][w-weight[i]]
```

)

# VISUAL

ITEM i

```
    ┌───────────────┐
    │               │
  SKIP             TAKE
    │               │
```

dp[i-1][w]      value[i]
+
dp[i-1][w-weight]

# CONNECTION

HOUSE ROBBER

TAKE
or
SKIP

KNAPSACK

TAKE
or
SKIP

Same decision pattern.

Difference:

HOUSE ROBBER
→ adjacency constraint

KNAPSACK
→ capacity constraint

# CODE

```cpp
int knapsack(
    vector<int>& weight,
    vector<int>& value,
    int capacity)
{
    int n = weight.size();

    vector<vector<int>> dp(
        n + 1,
        vector<int>(capacity + 1, 0)
    );

    for(int i = 1; i <= n; i++)
    {
        for(int w = 0; w <= capacity; w++)
        {
            dp[i][w] =
                dp[i-1][w];

            if(weight[i-1] <= w)
            {
                dp[i][w] =
                    max(
                        dp[i][w],
                        value[i-1]
                        +
                        dp[i-1]
                        [w-weight[i-1]]
                    );
            }
        }
    }

    return dp[n][capacity];
}
```

# COMPLEXITY

Time:

O(n × capacity)

Space:

O(n × capacity)

Can later be optimized to:

O(capacity)

But first:

UNDERSTAND THE 2D TABLE.

# COMMON TRAPS

[ ] Reusing an item

[ ] Using dp[i] instead of dp[i-1] after TAKE

[ ] Confusing weight and value

[ ] Forgetting capacity constraint

# MENTAL SENTENCE

"For each item:

Can I take it,
or should I skip it?"

# ============================================================

# #83 LONGEST INCREASING SUBSEQUENCE

# ============================================================

# LIS

LONGEST INCREASING SUBSEQUENCE

# IMPORTANT

SUBSEQUENCE

means:

order maintained

but:

elements do NOT need to be adjacent.

Example:

[10,9,2,5,3,7,101,18]

One LIS:

2 5 7 101

Length:

4

# TRIGGER WORDS

"longest increasing subsequence"

```
    ↓
```

LIS

# STATE

dp[i]

=

length of the longest
increasing subsequence
ENDING AT INDEX i

This wording is critical.

It does NOT mean:

"LIS of first i elements."

It means:

"ending exactly at i."

# TRANSITION

Look at every previous:

j < i

If:

nums[j] < nums[i]

then:

nums[i]

can extend the sequence ending at j.

Therefore:

# dp[i]

max(
dp[i],
dp[j] + 1
)

# VISUAL

previous smaller
↓
sequence
↓
current element

# CODE

```cpp
int lengthOfLIS(vector<int>& nums)
{
    int n = nums.size();

    vector<int> dp(n, 1);

    int ans = 1;

    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < i; j++)
        {
            if(nums[j] < nums[i])
            {
                dp[i] =
                    max(dp[i],
                        dp[j] + 1);
            }
        }

        ans = max(ans, dp[i]);
    }

    return ans;
}
```

# COMPLEXITY

Basic DP:

O(n²)

Space:

O(n)

# MENTAL MODEL

CURRENT ELEMENT
↓
LOOK BACK
↓
FIND PREVIOUS SMALLER
↓
EXTEND BEST SEQUENCE

# CONNECTION

HOUSE ROBBER

looks at:

previous compatible states

LIS

looks at:

previous smaller states

Same principle:

CURRENT STATE
↓
FIND VALID PREVIOUS STATES

# IMPORTANT DIFFERENCE

HOUSE ROBBER:

Only needs nearby states:

i-1
i-2

LIS:

May need ANY previous j:

0 ≤ j < i

Therefore:

nested loop.

# COMMON TRAPS

[ ] Thinking subsequence must be contiguous

[ ] Using <= when problem says strictly increasing

[ ] Defining dp[i] as LIS of prefix instead of ending at i

[ ] Returning dp[n-1] instead of max(dp[i])

# ============================================================

# #84 LONGEST COMMON SUBSEQUENCE

# ============================================================

# LCS

LONGEST COMMON SUBSEQUENCE

# INPUT

Two strings:

A

B

# GOAL

Find longest subsequence
common to both.

Example:

A:

abcde

B:

ace

LCS:

ace

Length:

3

# TRIGGER WORDS

"longest common subsequence"

"two strings"

"common subsequence"

```
    ↓
```

LCS

# STATE

dp[i][j]

=

LCS length between:

first i characters of A

and:

first j characters of B

# WHY 2D?

We have:

POSITION IN A

*

POSITION IN B

Therefore:

2 dimensions.

# CASE 1 — MATCH

If:

A[i-1] == B[j-1]

Then:

use that character.

dp[i][j]

=

1 + dp[i-1][j-1]

# CASE 2 — MISMATCH

If:

A[i-1] != B[j-1]

We have two possibilities:

skip A character

OR

skip B character

Therefore:

dp[i][j]

=

max(
dp[i-1][j],
dp[i][j-1]
)

# VISUAL

MATCH:

A[i-1] == B[j-1]

```
   ↓
```

TAKE BOTH

```
   ↓
```

1 + diagonal

MISMATCH:

```
   ┌─────────────┐
   │             │
skip A        skip B
   │             │
```

dp[i-1][j]    dp[i][j-1]

```
   ↓
```

MAX

# CODE

```cpp
int lcs(string a, string b)
{
    int n = a.size();
    int m = b.size();

    vector<vector<int>> dp(
        n + 1,
        vector<int>(m + 1, 0)
    );

    for(int i = 1; i <= n; i++)
    {
        for(int j = 1; j <= m; j++)
        {
            if(a[i-1] == b[j-1])
            {
                dp[i][j] =
                    1 + dp[i-1][j-1];
            }
            else
            {
                dp[i][j] =
                    max(
                        dp[i-1][j],
                        dp[i][j-1]
                    );
            }
        }
    }

    return dp[n][m];
}
```

# COMPLEXITY

Time:

O(n × m)

Space:

O(n × m)

# CONNECTION

LIS:

ONE sequence
+
previous index

LCS:

TWO sequences
+
two indices

Both are:

SUBSEQUENCE DP.

# VERY IMPORTANT

SUBSEQUENCE
≠
SUBSTRING

SUBSEQUENCE:

characters can be skipped.

SUBSTRING:

must be contiguous.

# COMMON TRAPS

[ ] Using one-dimensional DP

[ ] Confusing substring with subsequence

[ ] Using i instead of i-1 for string index

[ ] Forgetting empty-string base row/column

# MENTAL SENTENCE

"Two strings:

If characters match,
take them.

If they don't,
skip one side and keep the better answer."

# ============================================================

# #85 EDIT DISTANCE

# ============================================================

EDIT DISTANCE
│
├── Two strings
│
├── Operations:
│      ├── Insert
│      ├── Delete
│      └── Replace
│
└── Find minimum operations

# TRIGGER WORDS

"minimum operations"

"convert one string to another"

"insert"

"delete"

"replace"

```
    ↓
```

EDIT DISTANCE

# STATE

dp[i][j]

=

minimum operations
to convert first i characters
of A
into first j characters
of B

# BASE CASE

If A is empty:

Need:

j insertions.

Therefore:

dp[0][j] = j

If B is empty:

Need:

i deletions.

Therefore:

dp[i][0] = i

# CASE 1 — MATCH

If:

A[i-1] == B[j-1]

No operation needed.

# dp[i][j]

dp[i-1][j-1]

# CASE 2 — MISMATCH

Three choices:

INSERT

dp[i][j-1]

DELETE

dp[i-1][j]

REPLACE

dp[i-1][j-1]

Therefore:

dp[i][j]

=

1 + min(

```
dp[i][j-1],

dp[i-1][j],

dp[i-1][j-1]
```

)

# VISUAL

MISMATCH
↓
┌───────┬────────┬─────────┐
│       │        │         │
INSERT  DELETE   REPLACE
│       │        │
↓       ↓        ↓
LEFT    UP      DIAGONAL

Take:

MIN

# CODE

```cpp
int editDistance(string a, string b)
{
    int n = a.size();
    int m = b.size();

    vector<vector<int>> dp(
        n + 1,
        vector<int>(m + 1)
    );

    for(int i = 0; i <= n; i++)
        dp[i][0] = i;

    for(int j = 0; j <= m; j++)
        dp[0][j] = j;

    for(int i = 1; i <= n; i++)
    {
        for(int j = 1; j <= m; j++)
        {
            if(a[i-1] == b[j-1])
            {
                dp[i][j] =
                    dp[i-1][j-1];
            }
            else
            {
                dp[i][j] =
                    1 + min({
                        dp[i][j-1],
                        dp[i-1][j],
                        dp[i-1][j-1]
                    });
            }
        }
    }

    return dp[n][m];
}
```

# COMPLEXITY

Time:

O(n × m)

Space:

O(n × m)

# CONNECTION

LCS:

TWO STRINGS
+
2D DP

EDIT DISTANCE:

TWO STRINGS
+
2D DP

But:

LCS:

maximize length

Edit Distance:

minimize operations

# MENTAL SENTENCE

"If the characters match:

do nothing.

If they don't:

insert,
delete,
or replace.

Take the minimum."

# COMMON TRAPS

[ ] Wrong base row

[ ] Wrong base column

[ ] Forgetting +1 on mismatch

[ ] Mixing insert/delete directions

[ ] Confusing LCS with Edit Distance

# ============================================================

# #86 DECODE WAYS

# ============================================================

DECODE WAYS
│
├── Digits represent letters
│
│   1 → A
│   2 → B
│   ...
│   26 → Z
│
└── Find number of valid decodings

# EXAMPLE

"12"

Can decode as:

1 2
A B

OR:

12
L

Answer:

2

# TRIGGER WORDS

"number of ways"

"decode"

"1 to 26"

"digits to letters"

```
    ↓
```

DECODE WAYS

# CORE CONNECTION

This is:

CLIMBING STAIRS

with validity conditions.

CLIMBING:

1 step
or
2 steps

DECODE:

1 digit
or
2 digits

# STATE

dp[i]

=

number of ways
to decode the first i characters

# ONE-DIGIT CHOICE

Current character can stand alone
if it is not:

0

Example:

"3"

valid.

"0"

not independently valid.

# TWO-DIGIT CHOICE

Two digits are valid if:

10 through 26

Examples:

10 → valid

12 → valid

26 → valid

27 → invalid

# TRANSITION

dp[i]

=

valid one-digit ways
+
valid two-digit ways

# VISUAL

CURRENT POSITION
↓
┌───────────────┐
│               │
ONE DIGIT      TWO DIGITS
│               │
↓               ↓
i-1             i-2
│               │
dp[i-1]        dp[i-2]

# IMPORTANT EDGE CASE

"0"

No standalone decoding.

Therefore:

zero handling is essential.

# EXAMPLES

"10"

10

→ J

Answer:

1

"01"

Leading zero:

invalid.

# CODE

```cpp
int numDecodings(string s)
{
    int n = s.size();

    if(n == 0 || s[0] == '0')
        return 0;

    vector<int> dp(n + 1, 0);

    dp[0] = 1;
    dp[1] = 1;

    for(int i = 2; i <= n; i++)
    {
        int one =
            s[i-1] - '0';

        if(one >= 1 && one <= 9)
        {
            dp[i] += dp[i-1];
        }

        int two =
            (s[i-2] - '0') * 10
            +
            (s[i-1] - '0');

        if(two >= 10 && two <= 26)
        {
            dp[i] += dp[i-2];
        }
    }

    return dp[n];
}
```

# COMPLEXITY

Time:

O(n)

Space:

O(n)

Can later be optimized to:

O(1)

# CONNECTION

CLIMBING STAIRS
↓
1 STEP / 2 STEPS

DECODE WAYS
↓
1 DIGIT / 2 DIGITS

But:

Decode Ways
has:

VALIDITY CONDITIONS.

# COMMON TRAPS

[ ] Treating 0 as valid alone

[ ] Allowing 27–99 as two-digit codes

[ ] Forgetting leading zero

[ ] Wrong dp[0]

[ ] Wrong dp[1]

# MENTAL SENTENCE

"At every position:

Can I use one digit?

Can I use two digits?

If valid, add those ways."

# ============================================================

# #87 WORD BREAK

# ============================================================

WORD BREAK
│
├── Given string
├── Given dictionary
└── Determine whether
string can be segmented
into dictionary words

# EXAMPLE

s:

"leetcode"

dictionary:

["leet", "code"]

Can split:

leet | code

Therefore:

true

# TRIGGER WORDS

"dictionary"

"split string"

"segment"

"formed using words"

```
    ↓
```

WORD BREAK

# STATE

dp[i]

=

whether the first i characters
can be formed using
dictionary words

This is:

BOOLEAN DP.

# BASE CASE

dp[0] = true

Why?

The empty prefix
requires no words.

# TRANSITION

For current position i:

Look for an earlier position j.

If:

dp[j] == true

AND:

s[j...i-1]

is a dictionary word,

then:

dp[i] = true

# VISUAL

0
│
├── word ──→ j
│
└── word ──→ i

If:

position j is reachable

AND

j → i is a valid dictionary word

then:

i is reachable.

# MENTAL MODEL

STRING
↓
TRY A WORD
↓
CAN I REACH THIS POSITION?
↓
YES
↓
CONTINUE

# CODE

```cpp
bool wordBreak(
    string s,
    vector<string>& wordDict)
{
    int n = s.size();

    unordered_set<string> dict(
        wordDict.begin(),
        wordDict.end()
    );

    vector<bool> dp(n + 1, false);

    dp[0] = true;

    for(int i = 1; i <= n; i++)
    {
        for(int j = 0; j < i; j++)
        {
            if(!dp[j])
                continue;

            string word =
                s.substr(j, i - j);

            if(dict.count(word))
            {
                dp[i] = true;
                break;
            }
        }
    }

    return dp[n];
}
```

# COMPLEXITY

The straightforward implementation:

O(n²) state/transition checks,
plus string/dictionary operation costs
depending on implementation.

# CONNECTION

CLIMBING STAIRS
↓
REACH POSITION

DECODE WAYS
↓
REACH POSITION

WORD BREAK
↓
REACH POSITION

The common idea:

CURRENT POSITION
↓
WHICH PREVIOUS POSITIONS
CAN VALIDLY REACH ME?

# COMMON TRAPS

[ ] Forgetting dp[0] = true

[ ] Checking dictionary without checking dp[j]

[ ] Confusing substring with subsequence

[ ] Returning before checking all valid cuts

[ ] Mishandling empty string

# MENTAL SENTENCE

"Can I reach an earlier position,
and is everything between there
and here a valid word?"

# ============================================================

# SET 7 — CONNECTION MAP

# ============================================================

```
                DP
                 │
      ┌──────────┼──────────┐
      │          │          │
      ↓          ↓          ↓
   POSITION   DECISION    STRING
      │          │          │
      ↓          ↓          ↓
```

Climbing       House      LCS
Stairs        Robber      Edit Distance
│          │       Decode Ways
│          │       Word Break
↓          ↓
Decode      Knapsack
Ways

# CONNECTION 1

#79 CLIMBING STAIRS
↓
COUNT WAYS
↓
PREVIOUS 1/2 STATES

#86 DECODE WAYS
↓
COUNT WAYS
↓
PREVIOUS 1/2 STATES
+
VALIDITY

# CONNECTION 2

#80 HOUSE ROBBER
↓
TAKE / SKIP

#82 0/1 KNAPSACK
↓
TAKE / SKIP
+
CAPACITY

# CONNECTION 3

#81 COIN CHANGE
↓
MINIMUM

#85 EDIT DISTANCE
↓
MINIMUM

Both use:

MIN

But states are different.

# CONNECTION 4

#83 LIS
↓
SUBSEQUENCE
↓
ONE ARRAY

#84 LCS
↓
SUBSEQUENCE
↓
TWO STRINGS

# CONNECTION 5

#84 LCS
↓
TWO STRINGS
↓
2D DP

#85 EDIT DISTANCE
↓
TWO STRINGS
↓
2D DP

Common structure:

dp[i][j]

But:

LCS:

MATCH → +1

MISMATCH → MAX

Edit Distance:

MATCH → no cost

MISMATCH → 1 + MIN(3)

# CONNECTION 6

#86 DECODE WAYS
↓
POSITION DP

#87 WORD BREAK
↓
POSITION DP

Both:

ask whether previous positions
can lead to the current position.

Difference:

Decode:

fixed 1/2 digit choices

Word Break:

variable-length dictionary words

# ============================================================

# SET 7 — PATTERN MAP

# ============================================================

PROBLEM
│
├── #79 Climbing Stairs
│      ↓
│    1D COUNT DP
│
├── #80 House Robber
│      ↓
│    TAKE / SKIP DP
│
├── #81 Coin Change
│      ↓
│    UNBOUNDED MIN DP
│
├── #82 0/1 Knapsack
│      ↓
│    TAKE / SKIP + CAPACITY
│
├── #83 LIS
│      ↓
│    SUBSEQUENCE DP
│
├── #84 LCS
│      ↓
│    TWO-STRING 2D DP
│
├── #85 Edit Distance
│      ↓
│    TWO-STRING MIN DP
│
├── #86 Decode Ways
│      ↓
│    POSITION + VALIDITY DP
│
└── #87 Word Break
↓
BOOLEAN POSITION DP

# ============================================================

# SET 7 — STORY RECOGNITION

# ============================================================

"1 or 2 steps"

```
    ↓
```

#79 CLIMBING STAIRS

"Cannot choose adjacent"

```
    ↓
```

#80 HOUSE ROBBER

"Minimum coins"

```
    ↓
```

#81 COIN CHANGE

"Capacity + items + maximum value"

```
    ↓
```

#82 0/1 KNAPSACK

"Longest increasing subsequence"

```
    ↓
```

#83 LIS

"Common subsequence of two strings"

```
    ↓
```

#84 LCS

"Minimum operations to convert strings"

```
    ↓
```

#85 EDIT DISTANCE

"Decode digits into letters"

```
    ↓
```

#86 DECODE WAYS

"Can string be formed from dictionary words?"

```
    ↓
```

#87 WORD BREAK

# ============================================================

# SET 7 — OPERATION MAP

# ============================================================

COUNT

#79 Climbing Stairs
#86 Decode Ways

MAX

#80 House Robber
#82 0/1 Knapsack
#83 LIS
#84 LCS

MIN

#81 Coin Change
#85 Edit Distance

BOOLEAN

#87 Word Break

# ============================================================

# SET 7 — STATE MAP

# ============================================================

#79

dp[i]

#80

dp[i]

#81

dp[amount]

#82

dp[i][capacity]

#83

dp[i]

#84

dp[i][j]

#85

dp[i][j]

#86

dp[i]

#87

dp[i]

# IMPORTANT OBSERVATION

Most of Set 7:

1D DP

But:

#82 Knapsack
#84 LCS
#85 Edit Distance

are:

2D DP.

Therefore:

SET 7
↓
1D
+
2D

# ============================================================

# SET 7 — WHAT TO MEMORIZE

# ============================================================

DO NOT MEMORIZE:

"These 9 codes."

MEMORIZE:

THE 9 STORIES

#79

previous 2
+
SUM

#80

TAKE / SKIP
+
MAX

#81

TRY EVERY COIN
+
MIN

#82

TAKE / SKIP
+
CAPACITY

#83

LOOK BACK
+
PREVIOUS SMALLER
+
MAX

#84

MATCH → DIAGONAL + 1
MISMATCH → MAX(UP, LEFT)

#85

MATCH → DIAGONAL
MISMATCH → 1 + MIN(3)

#86

ONE DIGIT
+
TWO DIGIT
+
VALIDITY

#87

PREVIOUS VALID CUT
+
DICTIONARY WORD

# ============================================================

# SET 7 — COMMON DP TRAPS

# ============================================================

[ ] Defining dp vaguely

[ ] Writing code before state

[ ] Wrong base case

[ ] Wrong transition

[ ] Forgetting an available choice

[ ] Confusing take with skip

[ ] Reusing a 0/1 item

[ ] Confusing subsequence with substring

[ ] Using wrong string index

[ ] Mishandling zero in Decode Ways

[ ] Forgetting dp[0] = true in Word Break

[ ] Returning the wrong LIS state

[ ] Forgetting both dimensions in LCS/Edit Distance

# ============================================================

# SET 7 — COMPLEXITY CHEAT SHEET

# ============================================================

#79 Climbing Stairs

Time: O(n)
Space: O(1)

#80 House Robber

Time: O(n)
Space: O(1)

#81 Coin Change

Time: O(amount × coins)
Space: O(amount)

#82 0/1 Knapsack

Time: O(n × capacity)
Space: O(n × capacity)

#83 LIS

Time: O(n²)
Space: O(n)

#84 LCS

Time: O(n × m)
Space: O(n × m)

#85 Edit Distance

Time: O(n × m)
Space: O(n × m)

#86 Decode Ways

Time: O(n)
Space: O(n)

#87 Word Break

Typical straightforward DP:
O(n²) state/transition checks,
plus string/dictionary operation costs.

# ============================================================

# SET 7 — PRIORITY

# ============================================================

## TIER 1 — FOUNDATION

[ ] #79 Climbing Stairs
[ ] #80 House Robber
[ ] #81 Coin Change

Mental progression:

Climbing Stairs
↓
DP recurrence

House Robber
↓
TAKE / SKIP

Coin Change
↓
multiple choices
+
MIN

## TIER 2 — CORE

[ ] #82 0/1 Knapsack
[ ] #83 Longest Increasing Subsequence
[ ] #84 Longest Common Subsequence

## TIER 3 — STRING DP

[ ] #85 Edit Distance
[ ] #86 Decode Ways
[ ] #87 Word Break

# ============================================================

# SET 7 — CHECKLIST

# ============================================================

DP FOUNDATION

[ ] I can define overlapping subproblems.

[ ] I can explain memoization.

[ ] I can explain tabulation.

[ ] I can define dp[i] in English.

[ ] I can derive a recurrence.

[ ] I can identify base cases.

PROBLEMS

[ ] #79 Climbing Stairs

[ ] #80 House Robber

[ ] #81 Coin Change

[ ] #82 0/1 Knapsack

[ ] #83 LIS

[ ] #84 LCS

[ ] #85 Edit Distance

[ ] #86 Decode Ways

[ ] #87 Word Break

PATTERN RECOGNITION

[ ] Count ways → DP

[ ] Take/skip → decision DP

[ ] Minimum coins → Coin Change

[ ] Capacity + items → Knapsack

[ ] Increasing subsequence → LIS

[ ] Two strings → 2D DP candidate

[ ] Convert strings → Edit Distance

[ ] Decode 1/2 digits → Decode Ways

[ ] Dictionary segmentation → Word Break

# ============================================================

# SET 7 — FINAL MENTAL MAP

# ============================================================

DP
│
├── POSITION
│      │
│      ├── Climbing Stairs
│      │      ↓
│      │    1 / 2 previous states
│      │
│      ├── Decode Ways
│      │      ↓
│      │    1 / 2 valid digits
│      │
│      └── Word Break
│             ↓
│           previous valid cut
│
├── DECISION
│      │
│      ├── House Robber
│      │      ↓
│      │    TAKE / SKIP
│      │
│      └── 0/1 Knapsack
│             ↓
│           TAKE / SKIP
│           + CAPACITY
│
├── OPTIMIZATION
│      │
│      ├── Coin Change
│      │      ↓
│      │    MIN
│      │
│      ├── LIS
│      │      ↓
│      │    MAX
│      │
│      └── LCS
│             ↓
│           MAX
│
└── STRING TRANSFORMATION
│
└── Edit Distance
↓
MIN operations

# ============================================================

# SET 7 — ONE-PAGE MEMORY

# ============================================================

#79 CLIMBING STAIRS

ways[i] = ways[i-1] + ways[i-2]

#80 HOUSE ROBBER

max(
skip,
take
)

#81 COIN CHANGE

min(
dp[amount - coin] + 1
)

#82 KNAPSACK

max(
skip,
take + previous capacity
)

#83 LIS

if:

nums[j] < nums[i]

then:

dp[i] = max(dp[i], dp[j] + 1)

#84 LCS

MATCH:

1 + diagonal

MISMATCH:

max(up, left)

#85 EDIT DISTANCE

MATCH:

diagonal

MISMATCH:

1 + min(
insert,
delete,
replace
)

#86 DECODE WAYS

one digit
+
two digit

#87 WORD BREAK

reachable previous position
+
valid dictionary word

# ============================================================

# SET 7 — FINAL RULE

# ============================================================

DO NOT MEMORIZE:

"These 9 codes."

MEMORIZE:

THE 9 STORIES

Climbing:
"Where could I have come from?"

House Robber:
"Take or skip?"

Coin Change:
"Which coin gives the minimum?"

Knapsack:
"Take or skip under capacity?"

LIS:
"Which previous smaller element can extend me?"

LCS:
"Do the two current characters match?"

Edit Distance:
"How do I transform these prefixes?"

Decode Ways:
"Can I take one digit or two?"

Word Break:
"Can a previous valid position reach here?"

# SET 7 — COMPLETION CONDITION

We do NOT move to Set 8
just because you have read these notes.

You should be able to:

1. See the problem.

2. Identify the DP pattern.

3. Define the state.

4. Explain the transition.

5. State base cases.

6. Code it without copying.

7. Explain complexity.

8. Handle the important edge cases.

ONLY THEN:

SET 7 = COMPLETE.

# SET 7 — ORIGINAL PLAN BOUNDARY

This set contains ONLY:

#79 Climbing Stairs
#80 House Robber
#81 Coin Change
#82 0/1 Knapsack
#83 Longest Increasing Subsequence
#84 Longest Common Subsequence
#85 Edit Distance
#86 Decode Ways
#87 Word Break

