# 🧠 SOTI OA — DP & Optimization Master Recall Sheet

> **Goal:** Recognize the pattern quickly → define the state → write TAKE/SKIP or the correct recurrence → memoize → code.
>
> **Language:** C++
>
> **Level:** SOTI OA — do NOT overlearn advanced DP.

---

# 🚨 0. DP IN 30 SECONDS

## What is DP?

DP = **solve smaller problems once + remember their answers**.

Usually:

```text
Big problem
    ↓
smaller same-type problems
    ↓
same state appears again
    ↓
memoization
```

### DP recognition checklist

Ask:

```text
1. Am I optimizing / counting / checking possibilities?
2. Can I divide the problem into smaller choices?
3. Does the same smaller state occur again?
4. Does the future depend only on a small amount of information?
```

If YES → think DP.

---

# 🔥 THE MOST IMPORTANT QUESTION

Before coding, ask:

> **"What information do I need to know to completely describe where I am?"**

That becomes your `solve(...)` state.

Examples:

```text
Knapsack
→ solve(i, capacity)

Partition
→ solve(i, target)

Coin Change
→ solve(i, amount)

LIS
→ solve(i, prev)

LCS
→ solve(i, j)

Word Break
→ solve(i)

House Robber
→ solve(i)

Climbing Stairs
→ solve(i)

Edit Distance
→ solve(i, j)
```

---

# 🧩 MASTER PATTERN MAP

```text
                         DP
                          │
       ┌──────────────────┼──────────────────┐
       │                  │                  │
   CHOOSE ITEMS       SEQUENCES           ARRAY
       │                  │                  │
       │                  │                  ├── Kadane
       │                  │                  └── Product DP
       │                  │
       ├── 0/1 Knapsack   ├── LIS
       ├── Partition      ├── LCS
       └── Coin Change    └── Edit Distance
       │
       └── Word Break
       
Other:
Climbing Stairs
House Robber
Subarray Sum = K → Prefix Sum + HashMap
```

---

# ============================================================

# 1. 0/1 KNAPSACK ⭐⭐⭐⭐⭐

# ============================================================

## 🚨 Recognition keywords

```text
maximum value
maximum profit
limited capacity
each item can be selected ONCE
choose items
weight/time/cost <= capacity
```

Think:

```text
0/1 KNAPSACK
    ↓
TAKE / SKIP
```

---

## 🧠 Mental model

You are standing at item `i`.

Ask:

```text
Do I TAKE this item?
OR
Do I SKIP this item?
```

```text
                item i
                   │
          ┌────────┴────────┐
          ↓                 ↓
        SKIP              TAKE
          │                 │
       i + 1             i + 1
                         capacity-weight
```

---

## State

```cpp
solve(i, capacity)
```

Meaning:

> Maximum value I can obtain from index `i` onward with `capacity` remaining.

---

## Recurrence

```cpp
skip = solve(i+1, capacity);

take = value[i] +
       solve(i+1, capacity-weight[i]);
```

Answer:

```cpp
max(skip, take)
```

---

## C++ memoization template

```cpp
int solve(int i, int n, int W,
          vector<int>& weight,
          vector<int>& value,
          vector<vector<int>>& dp) {

    if(i == n || W == 0)
        return 0;

    if(dp[i][W] != -1)
        return dp[i][W];

    int skip = solve(i+1, n, W,
                     weight, value, dp);

    int take = 0;

    if(weight[i] <= W) {
        take = value[i] +
               solve(i+1, n, W-weight[i],
                     weight, value, dp);
    }

    return dp[i][W] = max(skip, take);
}

int knapsack(int n, int W,
             vector<int>& weight,
             vector<int>& value) {

    vector<vector<int>> dp(n, vector<int>(W+1, -1));

    return solve(0, n, W, weight, value, dp);
}
```

---

## 🔑 Your SOTI version

Projects:

```text
time[]  → weight
score[] → value
T       → capacity
```

Same exact problem.

---

## ⚠️ Biggest trap

If each item can be used **once**:

```cpp
take → solve(i+1, ...)
```

NOT:

```cpp
take → solve(i, ...)
```

---

# ============================================================

# 2. PARTITION EQUAL SUBSET SUM ⭐⭐⭐⭐⭐

# ============================================================

## 🚨 Recognition keywords

```text
divide array into two equal groups
equal sum
split into two subsets
can partition
```

Think:

```text
TOTAL SUM
    ↓
if odd → FALSE
    ↓
target = total / 2
    ↓
0/1 SUBSET SUM
```

---

## 🧠 Core insight

If:

```text
total = 20
```

two equal groups must each have:

```text
10
```

So we only need to ask:

> Can I select some elements whose sum is `10`?

That's just TAKE/SKIP.

---

## State

```cpp
solve(i, target)
```

Meaning:

> Can I make `target` using elements from `i` onward?

---

## Mental map

```text
Partition
    ↓
sum even?
    ↓
 target = sum/2
    ↓
Can I make target?
    ↓
TAKE / SKIP
```

---

## C++ memoization

```cpp
bool solve(int i, int n,
           int target,
           vector<int>& nums,
           vector<vector<int>>& dp) {

    if(target == 0)
        return true;

    if(i == n || target < 0)
        return false;

    if(dp[i][target] != -1)
        return dp[i][target];

    bool skip = solve(i+1, n, target,
                      nums, dp);

    bool take = false;

    if(nums[i] <= target) {
        take = solve(i+1, n,
                     target-nums[i],
                     nums, dp);
    }

    return dp[i][target] = (skip || take);
}

bool canPartition(vector<int>& nums) {

    int n = nums.size();
    int total = 0;

    for(int x : nums)
        total += x;

    if(total % 2 != 0)
        return false;

    int target = total / 2;

    vector<vector<int>> dp(
        n, vector<int>(target+1, -1)
    );

    return solve(0, n, target, nums, dp);
}
```

---

## 🔥 Interconnection

```text
0/1 Knapsack
      ↓
Instead of maximizing VALUE
      ↓
ask whether exact TARGET is possible
      ↓
Subset Sum
      ↓
Partition
```

---

# ============================================================

# 3. COIN CHANGE — UNBOUNDED KNAPSACK ⭐⭐⭐⭐⭐

# ============================================================

## 🚨 Recognition

```text
coins
minimum number of coins
make amount
unlimited supply
coin can be reused
```

Think:

```text
UNBOUNDED KNAPSACK
```

---

## 🧠 Biggest difference from 0/1 Knapsack

### 0/1:

```text
Take → i + 1
```

Because item is gone.

### Coin Change:

```text
Take → i
```

Because coin can be reused.

---

## Mental map

```text
                 COIN i
                    │
             ┌──────┴──────┐
             ↓             ↓
           SKIP          TAKE
             │             │
           i+1             i
                         amount-coin
```

---

## State

```cpp
solve(i, amount)
```

Meaning:

> Minimum coins required to make `amount` using coins from `i` onward.

---

## C++ template

```cpp
int solve(int i, int n,
          vector<int>& coins,
          int amount,
          vector<vector<int>>& dp) {

    if(amount == 0)
        return 0;

    if(i == n || amount < 0)
        return 1e9;

    if(dp[i][amount] != -1)
        return dp[i][amount];

    int skip = solve(i+1, n,
                     coins, amount, dp);

    int take = 1e9;

    if(coins[i] <= amount) {
        take = 1 + solve(i, n,
                         coins,
                         amount-coins[i],
                         dp);
    }

    return dp[i][amount] =
           min(skip, take);
}

int coinChange(vector<int>& coins, int amount) {

    int n = coins.size();

    vector<vector<int>> dp(
        n, vector<int>(amount+1, -1)
    );

    int ans = solve(0, n,
                    coins, amount, dp);

    return ans == 1e9 ? -1 : ans;
}
```

---

## 🚨 One-line recall

```text
0/1 → TAKE moves i+1
Coin Change → TAKE stays i
```

---

# ============================================================

# 4. LIS — LONGEST INCREASING SUBSEQUENCE ⭐⭐⭐⭐⭐

# ============================================================

## 🚨 Recognition

```text
longest
increasing
subsequence
```

Important:

```text
SUBSEQUENCE ≠ SUBARRAY
```

You CAN skip elements.

---

## 🧠 Key difficulty

For Knapsack:

```text
solve(i)
```

was enough.

For LIS, we need to know:

> What was the previous selected element?

Therefore:

```cpp
solve(i, prev)
```

---

## State

```cpp
solve(i, prev)
```

Meaning:

> Best increasing subsequence I can create from `i` onward when the previously selected element is `prev`.

`prev = -1` means:

```text
nothing selected yet
```

---

## Mental map

```text
                    nums[i]
                       │
              ┌────────┴────────┐
              ↓                 ↓
            SKIP              TAKE
              │                 │
           i+1             i+1, prev=i
                                │
                          only if nums[i]
                          > nums[prev]
```

---

## C++ memoization

```cpp
int solve(int i, int n, int prev,
          vector<int>& nums,
          vector<vector<int>>& dp) {

    if(i == n)
        return 0;

    if(dp[i][prev+1] != -1)
        return dp[i][prev+1];

    int skip = solve(i+1, n,
                     prev, nums, dp);

    int take = 0;

    if(prev == -1 ||
       nums[i] > nums[prev]) {

        take = 1 +
               solve(i+1, n,
                     i, nums, dp);
    }

    return dp[i][prev+1] =
           max(skip, take);
}

int lengthOfLIS(vector<int>& nums) {

    int n = nums.size();

    vector<vector<int>> dp(
        n, vector<int>(n+1, -1)
    );

    return solve(0, n, -1,
                 nums, dp);
}
```

---

## 🚨 Why `prev+1`?

`prev` can be:

```text
-1, 0, 1, 2, ...
```

Array index can't be `-1`.

So:

```text
prev = -1 → dp[][0]
prev = 0  → dp[][1]
prev = 1  → dp[][2]
```

---

## ⭐ Recall

> **LIS = TAKE/SKIP + remember PREVIOUS.**

---

# ============================================================

# 5. LCS — LONGEST COMMON SUBSEQUENCE ⭐⭐⭐⭐⭐

# ============================================================

## 🚨 Recognition

```text
two strings
longest common
subsequence
```

---

## State

```cpp
solve(i, j)
```

Meaning:

> LCS between `a[i...]` and `b[j...]`.

---

## 🧠 Main rule

If:

```cpp
a[i] == b[j]
```

TAKE BOTH:

```cpp
1 + solve(i+1, j+1)
```

If different:

```text
Skip A
OR
Skip B
```

---

## Mental map

```text
                 a[i], b[j]
                      │
             ┌────────┴────────┐
             ↓                 ↓
          SAME              DIFFERENT
             │                 │
          TAKE BOTH        ┌────┴────┐
             │             ↓         ↓
             │          SKIP A    SKIP B
             │             │         │
             ↓             ↓         ↓
        i+1,j+1         i+1,j      i,j+1
```

---

## C++ memoization

```cpp
int solve(int i, int j,
          int n, int m,
          string& a,
          string& b,
          vector<vector<int>>& dp) {

    if(i == n || j == m)
        return 0;

    if(dp[i][j] != -1)
        return dp[i][j];

    if(a[i] == b[j]) {

        return dp[i][j] =
            1 + solve(i+1, j+1,
                      n, m, a, b, dp);
    }

    int skipA =
        solve(i+1, j,
              n, m, a, b, dp);

    int skipB =
        solve(i, j+1,
              n, m, a, b, dp);

    return dp[i][j] =
           max(skipA, skipB);
}

int longestCommonSubsequence(
    string a, string b) {

    int n = a.size();
    int m = b.size();

    vector<vector<int>> dp(
        n, vector<int>(m, -1)
    );

    return solve(0, 0,
                 n, m,
                 a, b, dp);
}
```

---

## 🚨 Important

When characters are equal:

```text
DON'T skip unnecessarily.
TAKE BOTH.
```

For standard LCS, this recurrence is enough.

---

# ============================================================

# 6. WORD BREAK ⭐⭐⭐⭐⭐

# ============================================================

## 🚨 Recognition

```text
string
dictionary
can string be split into words?
```

Think:

```text
PREFIX / INDEX DP
```

---

## State

```cpp
solve(i)
```

Meaning:

> Can the substring starting at `i` be successfully broken into dictionary words?

---

## Mental map

```text
                   solve(i)
                      │
          try every possible ending j
                      │
               word = s[i...j]
                      │
              ┌───────┴───────┐
              ↓               ↓
          NOT VALID          VALID
              │               │
          skip candidate      TAKE
                              │
                         solve(j+1)
```

### Important:

DO NOT do:

```cpp
skip = solve(i+1);  // ❌
```

because that would allow characters to be thrown away.

"Skip" means:

> Skip this candidate word and try a longer word.

---

## C++ memoization

```cpp
bool solve(int i, int n,
           string& s,
           unordered_set<string>& dict,
           vector<int>& dp) {

    if(i == n)
        return true;

    if(dp[i] != -1)
        return dp[i];

    for(int j = i; j < n; j++) {

        string word =
            s.substr(i, j-i+1);

        if(dict.count(word)) {

            bool take =
                solve(j+1, n,
                      s, dict, dp);

            if(take)
                return dp[i] = true;
        }
    }

    return dp[i] = false;
}

bool wordBreak(
    string s,
    vector<string>& wordDict) {

    unordered_set<string> dict(
        wordDict.begin(),
        wordDict.end()
    );

    int n = s.size();

    vector<int> dp(n, -1);

    return solve(0, n,
                 s, dict, dp);
}
```

---

## ⭐ Recall

> **Word Break = TAKE a valid WORD, then JUMP to its end.**

---

# ============================================================

# 7. CLIMBING STAIRS ⭐⭐⭐⭐

# ============================================================

## 🚨 Recognition

```text
1 or 2 steps
number of ways
reach nth stair
```

Think:

```text
1D DP
```

---

## 🧠 Intuition

To reach stair `i`, the last move must be:

```text
from i-1
OR
from i-2
```

Therefore:

```text
ways(i) =
ways(i-1) + ways(i-2)
```

---

## Mental map

```text
              stair i
                 │
          ┌──────┴──────┐
          ↓             ↓
       from i-1       from i-2
          │             │
          └──────┬──────┘
                 ↓
                SUM
```

---

## Memoization

```cpp
int solve(int i, vector<int>& dp) {

    if(i == 0)
        return 1;

    if(i == 1)
        return 1;

    if(dp[i] != -1)
        return dp[i];

    return dp[i] =
        solve(i-1, dp) +
        solve(i-2, dp);
}

int climbStairs(int n) {

    vector<int> dp(n+1, -1);

    return solve(n, dp);
}
```

---

## 🚨 Recognition shortcut

```text
"ways to reach"
+
"1 or 2 steps"
=
FIBONACCI DP
```

---

# ============================================================

# 8. HOUSE ROBBER ⭐⭐⭐⭐

# ============================================================

## 🚨 Recognition

```text
houses
money
can't rob adjacent houses
maximum money
```

Think:

```text
0/1 CHOICE DP
```

---

## 🧠 At every house

Either:

```text
SKIP house
```

or:

```text
TAKE house
```

But if you TAKE:

```text
previous house cannot be taken
```

Therefore:

```text
take =
money[i] + solve(i+2)
```

---

## Mental map

```text
                HOUSE i
                   │
            ┌──────┴──────┐
            ↓             ↓
          SKIP           TAKE
            │             │
          i+1       money[i] + solve(i+2)
```

---

## C++ memoization

```cpp
int solve(int i,
          int n,
          vector<int>& nums,
          vector<int>& dp) {

    if(i >= n)
        return 0;

    if(dp[i] != -1)
        return dp[i];

    int skip =
        solve(i+1, n, nums, dp);

    int take =
        nums[i] +
        solve(i+2, n, nums, dp);

    return dp[i] =
           max(skip, take);
}

int rob(vector<int>& nums) {

    int n = nums.size();

    vector<int> dp(n, -1);

    return solve(0, n, nums, dp);
}
```

---

## 🔥 Interconnection

House Robber is basically:

```text
TAKE / SKIP
    +
TAKE causes a jump of 2
```

Compare:

```text
Knapsack:
TAKE → i+1

House Robber:
TAKE → i+2
```

---

# ============================================================

# 9. MAXIMUM PRODUCT SUBARRAY ⭐⭐⭐

# ============================================================

## 🚨 Recognition

```text
maximum product
contiguous subarray
```

Think:

```text
MAX + MIN DP
```

⚠️ Do NOT use normal Kadane with only one variable.

---

## 🧠 Why?

Because a negative number can turn:

```text
negative × negative = positive
```

Example:

```text
[-2, 3, -4]
```

At `-4`:

```text
minimum previous = -6

-6 × -4 = 24
```

So we must remember BOTH:

```text
maximum product ending here
minimum product ending here
```

---

## Mental map

```text
                 nums[i]
                    │
          ┌─────────┼─────────┐
          ↓         ↓         ↓
        start     extend     extend
                   max        min
                    │
             negative can swap
             max ↔ min
```

---

## C++ version

```cpp
int maxProduct(vector<int>& nums) {

    int curMax = nums[0];
    int curMin = nums[0];

    int ans = nums[0];

    for(int i = 1;
        i < nums.size();
        i++) {

        if(nums[i] < 0)
            swap(curMax, curMin);

        curMax =
            max(nums[i],
                curMax * nums[i]);

        curMin =
            min(nums[i],
                curMin * nums[i]);

        ans = max(ans, curMax);
    }

    return ans;
}
```

---

## ⭐ Recall

```text
Maximum SUM subarray
→ remember MAX

Maximum PRODUCT subarray
→ remember MAX + MIN
```

Because:

```text
negative × negative = positive
```

---

# ============================================================

# 10. EDIT DISTANCE ⭐⭐⭐

# ============================================================

## 🚨 Recognition

Two strings:

```text
convert A → B
minimum operations
insert
delete
replace
```

Think:

```text
2D STRING DP
```

---

## State

```cpp
solve(i, j)
```

Meaning:

> Minimum operations required to convert `a[i...]` into `b[j...]`.

---

## Base cases

If A finishes:

```text
i == n
```

we need to insert the rest of B:

```text
m-j
```

If B finishes:

```text
j == m
```

we need to delete the rest of A:

```text
n-i
```

---

## 🧠 Main decision

If:

```cpp
a[i] == b[j]
```

No operation needed:

```cpp
solve(i+1, j+1)
```

Otherwise three possibilities:

```text
INSERT
DELETE
REPLACE
```

---

## Mental map

```text
                 a[i] vs b[j]
                      │
             ┌────────┴────────┐
             ↓                 ↓
           SAME             DIFFERENT
             │                 │
             ↓          ┌──────┼──────┐
        move both       ↓      ↓      ↓
                     INSERT DELETE REPLACE
                       │      │       │
                     i,j+1  i+1,j   i+1,j+1
```

---

## C++ memoization

```cpp
int solve(int i, int j,
          int n, int m,
          string& a,
          string& b,
          vector<vector<int>>& dp) {

    if(i == n)
        return m - j;

    if(j == m)
        return n - i;

    if(dp[i][j] != -1)
        return dp[i][j];

    if(a[i] == b[j]) {

        return dp[i][j] =
            solve(i+1, j+1,
                  n, m, a, b, dp);
    }

    int insertOp =
        1 + solve(i, j+1,
                  n, m, a, b, dp);

    int deleteOp =
        1 + solve(i+1, j,
                  n, m, a, b, dp);

    int replaceOp =
        1 + solve(i+1, j+1,
                  n, m, a, b, dp);

    return dp[i][j] =
        min({insertOp,
             deleteOp,
             replaceOp});
}

int minDistance(string a, string b) {

    int n = a.size();
    int m = b.size();

    vector<vector<int>> dp(
        n, vector<int>(m, -1)
    );

    return solve(0, 0,
                 n, m,
                 a, b, dp);
}
```

---

# ============================================================

# 11. MAXIMUM SUBARRAY — KADANE ⭐⭐⭐⭐⭐

# ============================================================

## 🚨 Recognition

```text
maximum sum
contiguous subarray
```

Think:

```text
KADANE
```

---

## 🧠 Main decision

At every number:

```text
START NEW
OR
CONTINUE
```

---

## Recurrence

```cpp
current =
    max(nums[i],
        current + nums[i]);
```

---

## Mental map

```text
                 nums[i]
                    │
             ┌──────┴──────┐
             ↓             ↓
        START NEW       CONTINUE
             │             │
          nums[i]    previous + nums[i]
             │             │
             └──────┬──────┘
                    ↓
                   MAX
```

---

## C++ OA version

```cpp
int maxSubArray(vector<int>& nums) {

    int current = nums[0];
    int ans = nums[0];

    for(int i = 1;
        i < nums.size();
        i++) {

        current =
            max(nums[i],
                current + nums[i]);

        ans = max(ans, current);
    }

    return ans;
}
```

---

## ⭐ Key difference

```text
Subsequence:
can skip

Subarray:
cannot skip
must be contiguous
```

---

# ============================================================

# 12. SUBARRAY SUM = K ⭐⭐⭐⭐⭐

# ============================================================

## 🚨 Recognition

```text
COUNT
+
CONTIGUOUS SUBARRAY
+
SUM = K
```

Think immediately:

```text
PREFIX SUM + HASHMAP
```

Not normal TAKE/SKIP DP.

---

## 🧠 Magic formula

Current prefix:

```text
P
```

Need previous prefix:

```text
P - K
```

Because:

```text
P - oldPrefix = K
```

Therefore:

```text
oldPrefix = P-K
```

---

## Mental map

```text
current prefix
      │
      ↓
need = prefix - K
      │
      ↓
hashmap[need]
      │
      ↓
how many previous prefixes?
      │
      ↓
add to answer
```

---

## C++

```cpp
int subarraySum(vector<int>& nums, int k) {

    unordered_map<int, int> mp;

    mp[0] = 1;

    int prefix = 0;
    int ans = 0;

    for(int x : nums) {

        prefix += x;

        int need = prefix - k;

        if(mp.count(need))
            ans += mp[need];

        mp[prefix]++;
    }

    return ans;
}
```

---

## 🚨 MUST REMEMBER

```cpp
mp[0] = 1;
```

means:

> There is one empty prefix before the array.

Without this, subarrays starting at index `0` can be missed.

---

# ============================================================

# 13. AMPLIFIER ARRAY — SOTI 2024 🟡

# ============================================================

## ⚠️ IMPORTANT

Do NOT force this into your DP template.

The publicly reported SOTI 2024 question is an **Amplifier Array** problem involving amplifier values and reaching a target signal/product.

The available public recollection is not detailed enough to establish one universally reliable DP recurrence.

Therefore:

```text
Amplifier Array
      ↓
DO NOT MEMORIZE AS DP
      ↓
recognize from exact statement
```

If your actual OA has the exact statement, use its constraints and operation rules.

---

# ============================================================

# 14. THE BIG CONNECTIONS

# ============================================================

## 🔥 Family 1 — TAKE / SKIP

These are your most important family:

```text
0/1 Knapsack
Partition Equal Subset Sum
House Robber
LIS
```

### 0/1 Knapsack

```text
TAKE → i+1
SKIP → i+1
capacity changes on TAKE
```

### Partition

```text
TAKE → i+1
SKIP → i+1
target changes on TAKE
```

### House Robber

```text
TAKE → i+2
SKIP → i+1
```

### LIS

```text
TAKE → i+1 + update prev
SKIP → i+1 + keep prev
```

---

# 🔥 Family 2 — UNBOUNDED CHOICE

```text
Coin Change
```

Main difference:

```text
TAKE → i
```

because we can reuse the same coin.

---

# 🔥 Family 3 — TWO STRING INDEX DP

```text
LCS
Edit Distance
```

Both:

```text
solve(i,j)
```

But the action differs.

### LCS

```text
same → TAKE BOTH
different → SKIP A / SKIP B
```

### Edit Distance

```text
same → move both
different → INSERT / DELETE / REPLACE
```

---

# 🔥 Family 4 — 1D ARRAY DP

```text
Climbing Stairs
House Robber
Maximum Subarray
Maximum Product Subarray
```

### Climbing Stairs

```text
previous 1 + previous 2
```

### House Robber

```text
TAKE / SKIP
```

### Maximum Subarray

```text
CONTINUE / START NEW
```

### Maximum Product

```text
MAX + MIN
```

---

# 🔥 Family 5 — STRING / PREFIX DP

```text
Word Break
```

```text
solve(i)
   ↓
try every word starting at i
   ↓
TAKE word
   ↓
jump
```

---

# 🔥 Family 6 — NOT REALLY DP

```text
Subarray Sum = K
       ↓
Prefix Sum + HashMap
```

Recognition:

```text
COUNT contiguous subarrays
whose sum = K
```

---

# ============================================================

# 15. SIMILARITY / DIFFERENCE TABLE

# ============================================================

| Problem         | State        | Choice        | Key idea              |
| --------------- | ------------ | ------------- | --------------------- |
| 0/1 Knapsack    | `(i,W)`      | Take/Skip     | Item once             |
| Partition       | `(i,target)` | Take/Skip     | Exact half            |
| Coin Change     | `(i,amount)` | Take/Skip     | Take stays `i`        |
| LIS             | `(i,prev)`   | Take/Skip     | Previous matters      |
| LCS             | `(i,j)`      | Take/Skip A/B | Compare strings       |
| Word Break      | `i`          | Take word     | Jump                  |
| Climbing Stairs | `i`          | Last step     | `i-1/i-2`             |
| House Robber    | `i`          | Take/Skip     | Take → `i+2`          |
| Max Subarray    | `i`          | Continue/New  | Kadane                |
| Max Product     | `i`          | Extend/New    | Max + Min             |
| Edit Distance   | `(i,j)`      | 3 operations  | Insert/Delete/Replace |
| Subarray Sum K  | prefix       | Count         | HashMap               |

---

# ============================================================

# 16. 🚨 KEYWORD → PATTERN CHEAT SHEET

# ============================================================

```text
"maximum value"
"capacity"
"weight"
"profit"
"choose items once"
        ↓
0/1 KNAPSACK
```

```text
"equal partition"
"two subsets equal"
"equal sum"
        ↓
PARTITION / SUBSET SUM
```

```text
"minimum coins"
"make amount"
"unlimited coins"
        ↓
COIN CHANGE
```

```text
"longest increasing subsequence"
        ↓
LIS
```

```text
"longest common subsequence"
"two strings"
        ↓
LCS
```

```text
"dictionary"
"split string"
"form string using words"
        ↓
WORD BREAK
```

```text
"number of ways"
"1 or 2 steps"
        ↓
CLIMBING STAIRS
```

```text
"houses"
"can't rob adjacent"
"maximum money"
        ↓
HOUSE ROBBER
```

```text
"maximum sum"
"CONTIGUOUS subarray"
        ↓
KADANE
```

```text
"maximum product"
"CONTIGUOUS subarray"
        ↓
MAX PRODUCT
→ MAX + MIN
```

```text
"convert string A to B"
"insert/delete/replace"
"minimum operations"
        ↓
EDIT DISTANCE
```

```text
"COUNT"
"CONTIGUOUS subarray"
"sum = K"
        ↓
PREFIX SUM + HASHMAP
```

---

# ============================================================

# 17. THE MOST IMPORTANT DIFFERENCE: SUBARRAY vs SUBSEQUENCE

# ============================================================

## SUBARRAY

Must be continuous:

```text
[1,2,3,4]
```

Can choose:

```text
[2,3]
```

Cannot choose:

```text
[1,3] ❌
```

Typical:

```text
Maximum Subarray
Subarray Sum K
Maximum Product Subarray
```

---

## SUBSEQUENCE

Can skip:

```text
[1,2,3,4]
```

Can choose:

```text
[1,3]
```

Typical:

```text
LIS
LCS
```

### 🚨 OA trigger

```text
CONTIGUOUS → SUBARRAY

NOT necessarily contiguous → SUBSEQUENCE
```

---

# ============================================================

# 18. TAKE / SKIP MASTER TEMPLATE

# ============================================================

When you see a selection problem, first try:

```cpp
int skip = solve(nextIndex, sameState);

int take = ...

return max/min/OR(skip, take);
```

But determine what changes after TAKE.

---

## 0/1

```cpp
take → i+1
```

## Unbounded

```cpp
take → i
```

## House Robber

```cpp
take → i+2
```

## LIS

```cpp
take → i+1
prev = i
```

## Partition

```cpp
take → target - nums[i]
```

## Knapsack

```cpp
take → capacity - weight[i]
```

---

# ============================================================

# 19. BASE CASES — QUICK RECALL

# ============================================================

## Knapsack

```cpp
if(i == n || W == 0)
    return 0;
```

---

## Partition

```cpp
if(target == 0)
    return true;

if(i == n || target < 0)
    return false;
```

---

## Coin Change

```cpp
if(amount == 0)
    return 0;

if(i == n || amount < 0)
    return INF;
```

---

## LIS

```cpp
if(i == n)
    return 0;
```

---

## LCS

```cpp
if(i == n || j == m)
    return 0;
```

---

## Word Break

```cpp
if(i == n)
    return true;
```

---

## Climbing Stairs

```cpp
if(i == 0 || i == 1)
    return 1;
```

---

## House Robber

```cpp
if(i >= n)
    return 0;
```

---

## Edit Distance

```cpp
if(i == n)
    return m-j;

if(j == m)
    return n-i;
```

---

# ============================================================

# 20. MEMOIZATION TEMPLATE

# ============================================================

For almost all recursive DP:

```cpp
returnType solve(state...) {

    // 1. BASE CASE

    // 2. ALREADY SOLVED?
    if(dp[state] != -1)
        return dp[state];

    // 3. CHOICES
    ...

    // 4. SAVE
    return dp[state] = answer;
}
```

---

# ============================================================

# 21. HOW TO DEBUG YOUR DP

# ============================================================

If your code is wrong, check these in order:

### 1. Did I define the state correctly?

Ask:

> Does `solve(...)` contain ALL information needed for the future?

---

### 2. Did I move the index correctly?

```text
0/1 → i+1
unbounded TAKE → i
robber TAKE → i+2
```

---

### 3. Did I forget the value/count?

Knapsack:

```cpp
take = value[i] + ...
```

Coin Change:

```cpp
take = 1 + ...
```

LCS:

```cpp
take = 1 + ...
```

---

### 4. Is my DP dimension correct?

If state is:

```text
(i, target)
```

you need:

```cpp
dp[n][target+1]
```

If:

```text
(i,j)
```

you need:

```cpp
dp[n][m]
```

If:

```text
(i,prev)
```

you need:

```cpp
dp[n][n+1]
```

---

# ============================================================

# 22. COMPLEXITY RECALL

# ============================================================

## 0/1 Knapsack

```text
States = n × W
Time   = O(nW)
Space  = O(nW)
```

## Partition

```text
O(n × target)
```

## Coin Change

```text
O(n × amount)
```

## LIS memoization

```text
O(n²)
```

## LCS

```text
O(nm)
```

## Word Break

Roughly:

```text
O(n² × substring/hash cost)
```

For SOTI-level constraints, focus on recognizing it.

## Climbing Stairs

```text
O(n)
```

## House Robber

```text
O(n)
```

## Maximum Subarray

```text
O(n)
```

## Maximum Product

```text
O(n)
```

## Edit Distance

```text
O(nm)
```

## Subarray Sum K

```text
O(n)
```

average hashmap complexity.

---

# ============================================================

# 23. 🚨 "WHAT SHOULD I THINK FIRST?" FLOWCHART

# ============================================================

```text
                    ARRAY / STRING
                         │
                         ▼
               What is the question?
                         │
        ┌────────────────┼─────────────────┐
        │                │                 │
     MAX/MIN           COUNT            BOOLEAN
        │                │                 │
        ▼                ▼                 ▼
   Is it             Is it              Can it
   contiguous?       subarray sum?      be formed?
        │                │                 │
     ┌──┴──┐             │                 │
     YES   NO             ▼                 ▼
      │     │        Prefix Sum         TAKE/SKIP
      │     │        + HashMap              │
      │     │                              │
      ▼     ▼                       Which pattern?
   Kadane  DP                             │
      │                              ┌────┼─────┐
      │                              ▼    ▼     ▼
      │                           subset coin  word
      │                           sum   change break
      │
      └── Product?
              │
              ▼
          MAX + MIN
```

---

# ============================================================

# 24. 🧠 10-SECOND SOTI RECOGNITION

# ============================================================

## If you see...

```text
CAPACITY + VALUE + CHOOSE
→ KNAPSACK
```

```text
EQUAL TWO GROUPS
→ PARTITION
```

```text
UNLIMITED + MINIMUM COINS
→ COIN CHANGE
```

```text
LONGEST + INCREASING + SUBSEQUENCE
→ LIS
```

```text
TWO STRINGS + LONGEST COMMON
→ LCS
```

```text
DICTIONARY + SPLIT STRING
→ WORD BREAK
```

```text
WAYS + STAIRS + 1/2
→ CLIMBING STAIRS
```

```text
MAX MONEY + NO ADJACENT
→ HOUSE ROBBER
```

```text
MAX SUM + CONTIGUOUS
→ KADANE
```

```text
MAX PRODUCT + CONTIGUOUS
→ MAX + MIN
```

```text
CONVERT STRING + INSERT/DELETE/REPLACE
→ EDIT DISTANCE
```

```text
COUNT + SUBARRAY + SUM K
→ PREFIX SUM + HASHMAP
```

---

# ============================================================

# 25. 🔥 THE 6 MOST IMPORTANT INTERCONNECTIONS

# ============================================================

## Connection 1

```text
0/1 Knapsack
      ↓
Subset Sum
      ↓
Partition
```

Partition is basically:

> "Can I use 0/1 Knapsack-style TAKE/SKIP to create `total/2`?"

---

## Connection 2

```text
0/1 Knapsack
      ↓
Coin Change
```

Difference:

```text
0/1 → item once
Coin → item reusable
```

This changes:

```cpp
take → i+1
```

to:

```cpp
take → i
```

---

## Connection 3

```text
TAKE/SKIP
     ↓
LIS
```

Same philosophy, but now:

```text
"Can I TAKE?"
```

depends on:

```text
previous selected element
```

So state becomes:

```cpp
(i, prev)
```

---

## Connection 4

```text
LCS
  ↓
Edit Distance
```

Both use:

```cpp
solve(i,j)
```

because two strings are involved.

Difference:

```text
LCS:
match → take

Edit:
match → move
mismatch → 3 operations
```

---

## Connection 5

```text
Maximum Subarray
        ↓
Maximum Product Subarray
```

Both care about:

```text
CONTIGUOUS
```

But:

```text
SUM
→ one running best

PRODUCT
→ positive/negative interaction
→ MAX + MIN
```

---

## Connection 6

```text
Word Break
     ↓
Prefix / index DP
```

It looks like string manipulation, but underneath:

```text
At position i
    ↓
make a choice
    ↓
jump forward
    ↓
memoize i
```

---

# ============================================================

# 26. 🚨 DON'T MIX THESE UP

# ============================================================

### Knapsack vs Coin Change

```text
Can reuse?
YES → Coin Change
NO  → 0/1 Knapsack
```

---

### Subarray vs Subsequence

```text
CONTIGUOUS?
YES → Subarray
NO  → Subsequence
```

---

### Maximum Sum vs Number of Subarrays

```text
MAXIMUM SUM
→ Kadane

COUNT subarrays SUM = K
→ Prefix Sum + HashMap
```

---

### LCS vs LIS

```text
ONE sequence
+ increasing
→ LIS

TWO sequences/strings
+ common
→ LCS
```

---

### LCS vs Edit Distance

```text
LONGEST COMMON
→ LCS

MINIMUM OPERATIONS TO CONVERT
→ Edit Distance
```

---

# ============================================================

# 27. 🧠 FINAL MASTER MEMORY MAP

# ============================================================

```text
                         SOTI DP
                            │
       ┌────────────────────┼────────────────────┐
       │                    │                    │
     CHOOSE                STRING              ARRAY
       │                    │                    │
       │                    │                    │
 ┌─────┼─────┐        ┌────┼────┐         ┌─────┼─────┐
 │     │     │        │         │         │     │     │
0/1  PART  COIN      LCS      EDIT       KADANE PROD  ROBBER
 │     │     │         │         │         │     │     │
 │     │     │         │         │         │     │     │
TAKE  TAKE  TAKE     i,j       i,j       cont  max/min take/skip
SKIP  SKIP  SKIP
 │     │     │
i+1   target i
      change
```

And:

```text
WORD BREAK
    ↓
solve(i)
    ↓
TAKE WORD
    ↓
JUMP
```

And:

```text
SUBARRAY SUM K
    ↓
PREFIX SUM
    ↓
HASHMAP
```

---

# ============================================================

# 28. 🏆 THE ULTIMATE SOTI DP CHEAT SHEET

# ============================================================

```text
KNAPSACK
solve(i,W)
TAKE/SKIP
TAKE → i+1
MAX
```

```text
PARTITION
sum/2
solve(i,target)
TAKE/SKIP
BOOLEAN
```

```text
COIN CHANGE
solve(i,amount)
TAKE/SKIP
TAKE → i
MIN
```

```text
LIS
solve(i,prev)
TAKE/SKIP
previous matters
MAX
```

```text
LCS
solve(i,j)
same → TAKE BOTH
different → SKIP A/B
MAX
```

```text
WORD BREAK
solve(i)
try words
TAKE word
jump
BOOLEAN
```

```text
CLIMBING STAIRS
solve(i)
solve(i-1)+solve(i-2)
COUNT
```

```text
HOUSE ROBBER
solve(i)
TAKE → i+2
SKIP → i+1
MAX
```

```text
MAX SUBARRAY
continue OR restart
KADANE
MAX SUM
```

```text
MAX PRODUCT
MAX + MIN
negative can flip
MAX PRODUCT
```

```text
EDIT DISTANCE
solve(i,j)
INSERT / DELETE / REPLACE
MIN
```

```text
SUBARRAY SUM K
prefix-K
HASHMAP
COUNT
```

---

# 🎯 LAST-MINUTE SOTI REVISION ORDER

If you have very little time, revise in this order:

```text
1. 0/1 Knapsack
        ↓
2. Partition
        ↓
3. Coin Change
        ↓
4. LIS
        ↓
5. LCS
        ↓
6. Word Break
        ↓
7. House Robber
        ↓
8. Maximum Subarray
        ↓
9. Subarray Sum K
        ↓
10. Climbing Stairs
        ↓
11. Maximum Product
        ↓
12. Edit Distance
```

## ⭐ Highest ROI

```text
████████████████  0/1 Knapsack
████████████████  Partition
████████████████  Coin Change
██████████████    LIS
██████████████    LCS
██████████████    Word Break
████████████      House Robber
████████████      Maximum Subarray
████████████      Subarray Sum K
██████████        Climbing Stairs
████████          Maximum Product
██████            Edit Distance
```

---

# 🧠 FINAL RULE

When you enter the OA, DON'T ask:

> "Which DP algorithm do I remember?"

Ask:

> **"What is my state, and what choices do I have from this state?"**

Then:

```text
STATE
  ↓
CHOICES
  ↓
TRANSITION
  ↓
BASE CASE
  ↓
MEMOIZATION
```

For your style, the most powerful mental shortcut is:

```text
CAN I CHOOSE ITEMS?
        ↓
TAKE / SKIP

CAN I REUSE?
        ↓
TAKE stays i

DO I NEED PREVIOUS?
        ↓
Add prev to state

TWO STRINGS?
        ↓
Usually i,j

CONTIGUOUS MAX SUM?
        ↓
Kadane

CONTIGUOUS COUNT SUM K?
        ↓
Prefix Sum + HashMap

STRING DICTIONARY?
        ↓
Word Break / index DP

PRODUCT?
        ↓
Think about negative → MAX + MIN
```

# 🏁 SOTI DP MISSION

You do **NOT** need to become a DP expert.

You need to become someone who sees:

```text
Problem statement
      ↓
"Ah, this is TAKE/SKIP."
      ↓
"What changes when I TAKE?"
      ↓
write solve(...)
      ↓
memoize
      ↓
submit
```

**Recognition > memorizing 50 problems.**

**8–12 patterns deeply internalized > 30 patterns half-known.**
