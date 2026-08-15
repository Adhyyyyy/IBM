ADHY — yes. I’ll make this the **final clean notebook version**: no conversational commentary, no unnecessary repetition, and everything organized so you can paste it directly into your `.md` notes.

The structure follows the attached master-pattern style: **big picture → mental map → individual problem → intuition → algorithm → code → dry run → complexity → when to use → when not to use → traps → interview explanation → recognition cheat sheet**. 

````md
# STRING — MASTER PATTERN NOTEBOOK
## 8 HIGH-VALUE STRING PROBLEMS
### OA + INTERVIEW + PATTERN RECOGNITION

---

# TABLE OF CONTENTS

1. Length of Last Word
2. Pangram
3. Reverse String
4. String Compression
5. Valid Parentheses
6. Longest Substring Without Repeating Characters
7. Group Anagrams
8. Word Break / Concatenated-Word String

---

# ============================================================
# 0. STRING — BIG PICTURE
# ============================================================

STRING PROBLEMS
│
├── SIMPLE TRAVERSAL
│   │
│   ├── Length of Last Word
│   ├── Pangram
│   └── Reverse String
│
├── POINTER TECHNIQUES
│   │
│   ├── Reverse String
│   ├── Length of Last Word
│   └── String Compression
│
├── HASHING / FREQUENCY
│   │
│   ├── Pangram
│   ├── Longest Substring
│   └── Group Anagrams
│
├── STACK
│   │
│   └── Valid Parentheses
│
├── SLIDING WINDOW
│   │
│   └── Longest Substring Without Repeating Characters
│
└── DP + HASH SET
    │
    └── Word Break


# ============================================================
# 1. MASTER MENTAL MAP
# ============================================================

STRING
│
├── "I need the LAST word"
│       ↓
│   RIGHT → LEFT
│
├── "Do all alphabet letters exist?"
│       ↓
│   FREQUENCY / BOOLEAN ARRAY
│
├── "Reverse the string"
│       ↓
│   TWO POINTERS
│
├── "Compress consecutive characters"
│       ↓
│   READ + WRITE POINTER
│
├── "Match nested brackets"
│       ↓
│   STACK
│
├── "Longest substring with condition"
│       ↓
│   SLIDING WINDOW
│
├── "Group equivalent strings"
│       ↓
│   SIGNATURE + HASH MAP
│
└── "Can string be formed from words?"
        ↓
    DP + HASH SET


# ============================================================
# 2. MASTER PATTERN RECOGNITION
# ============================================================

When you read a String problem, ask these questions:

1. Is it asking about the END / LAST part?
   → Try RIGHT TO LEFT.

2. Is it asking about characters appearing / counting?
   → FREQUENCY ARRAY / HASH MAP.

3. Is it asking to reverse / compare both ends?
   → TWO POINTERS.

4. Does it involve CONSECUTIVE repeated characters?
   → GROUP + COUNT.

5. Does it involve nested matching / brackets?
   → STACK.

6. Does it ask for LONGEST / SHORTEST SUBSTRING?
   → Think SLIDING WINDOW.

7. Does it ask to GROUP strings based on same characters?
   → NORMALIZED SIGNATURE + HASH MAP.

8. Does it ask whether a string can be formed from pieces?
   → DP + HASH SET.


# ============================================================
# 3. PROBLEM 1 — LENGTH OF LAST WORD
# ============================================================

## PROBLEM

Given a string `s` consisting of words and spaces, return the length
of the LAST word.

A word is a maximal sequence of non-space characters.

Example:

Input:
"Hello World"

Output:
5


# ------------------------------------------------------------
# PATTERN
# ------------------------------------------------------------

LAST WORD
    ↓
START FROM END
    ↓
SKIP TRAILING SPACES
    ↓
COUNT CHARACTERS
    ↓
STOP AT SPACE / BEGINNING


# ------------------------------------------------------------
# KEY OBSERVATION
# ------------------------------------------------------------

We only need the LAST word.

Therefore, processing the entire string from the beginning is
unnecessary.

Start from the RIGHT.

Example:

"Hello World"

                 ↓
              LAST WORD

H e l l o   W o r l d
                ← ← ←


# ------------------------------------------------------------
# ALGORITHM
# ------------------------------------------------------------

1. Set `i = s.size() - 1`.
2. Skip all spaces at the end.
3. Start counting characters.
4. Continue until:
   - `i < 0`, OR
   - `s[i] == ' '`.
5. Return the count.


# ------------------------------------------------------------
# C++ SOLUTION
# ------------------------------------------------------------

```cpp
int lengthOfLastWord(string s) {

    int i = s.size() - 1;

    // Skip trailing spaces
    while (i >= 0 && s[i] == ' ')
        i--;

    int len = 0;

    // Count the last word
    while (i >= 0 && s[i] != ' ') {
        len++;
        i--;
    }

    return len;
}
````

# ------------------------------------------------------------

# DRY RUN

# ------------------------------------------------------------

s = "Hello World"

Index:

0 1 2 3 4 5 6 7 8 9 10
H e l l o   W o r l d

Start:

i = 10

Character = d
len = 1

i = 9
Character = l
len = 2

i = 8
Character = r
len = 3

i = 7
Character = o
len = 4

i = 6
Character = W
len = 5

i = 5
Character = ' '

STOP

Answer = 5

# ------------------------------------------------------------

# EDGE CASES

# ------------------------------------------------------------

"Hello World"
→ 5

"World"
→ 5

"Hello World   "
→ 5

"   World"
→ 5

"   Hello World   "
→ 5

# ------------------------------------------------------------

# COMPLEXITY

# ------------------------------------------------------------

Time:
O(n)

Space:
O(1)

# ------------------------------------------------------------

# WHEN TO USE

# ------------------------------------------------------------

Use RIGHT → LEFT when:

* Asked for last word
* Asked for trailing characters
* Asked for suffix information
* Only the final token matters

# ------------------------------------------------------------

# WHEN NOT TO USE

# ------------------------------------------------------------

If you need:

* Every word
* Number of words
* Word frequencies
* All tokens

then another approach may be more appropriate.

# ------------------------------------------------------------

# OA / INTERVIEW TIP

# ------------------------------------------------------------

Whenever you see:

"last"
"trailing"
"from the end"

Think:

RIGHT → LEFT

# ------------------------------------------------------------

# MEMORY TRIGGER

# ------------------------------------------------------------

LAST WORD
↓
RIGHT
↓
SKIP SPACES
↓
COUNT

# ============================================================

# 4. PROBLEM 2 — PANGRAM

# ============================================================

## PROBLEM

Given a string `sentence`, determine whether it contains every
letter of the English alphabet at least once.

Comparison is case-insensitive.

Example:

Input:
"The quick brown fox jumps over the lazy dog"

Output:
true

# ------------------------------------------------------------

# PATTERN

# ------------------------------------------------------------

PANGRAM
↓
NEED ALL 26 LETTERS
↓
BOOLEAN / FREQUENCY ARRAY
↓
CHECK 26 POSITIONS

# ------------------------------------------------------------

# KEY OBSERVATION

# ------------------------------------------------------------

We don't care:

* Order
* Position
* Number of times a letter appears

We only care:

"Did every letter from a to z appear?"

# ------------------------------------------------------------

# CHARACTER → INDEX

# ------------------------------------------------------------

'a' → 0
'b' → 1
'c' → 2
...
'z' → 25

Formula:

```cpp
c - 'a'
```

Example:

```text
'd' - 'a' = 3
```

# ------------------------------------------------------------

# C++ SOLUTION

# ------------------------------------------------------------

```cpp
bool isPangram(string sentence) {

    bool seen[26] = {};

    for (char c : sentence) {

        c = tolower(c);

        if (c >= 'a' && c <= 'z') {
            seen[c - 'a'] = true;
        }
    }

    for (int i = 0; i < 26; i++) {

        if (!seen[i])
            return false;
    }

    return true;
}
```

# ------------------------------------------------------------

# ALTERNATIVE — FREQUENCY ARRAY

# ------------------------------------------------------------

```cpp
int freq[26] = {};

for (char c : sentence) {

    c = tolower(c);

    if (c >= 'a' && c <= 'z')
        freq[c - 'a']++;
}
```

# ------------------------------------------------------------

# DRY RUN

# ------------------------------------------------------------

Input:

"abcde....xyz"

For every character:

a → seen[0] = true
b → seen[1] = true
c → seen[2] = true
...
z → seen[25] = true

Finally:

all 26 positions = true

Answer:

true

# ------------------------------------------------------------

# IMPORTANT DISTINCTION

# ------------------------------------------------------------

Pangram means:

ALL 26 LETTERS

NOT:

"26 characters"

Example:

"aaaaaaaaaaaaaaaaaaaaaaaa"

contains many characters.

But:

NOT A PANGRAM.

# ------------------------------------------------------------

# COMPLEXITY

# ------------------------------------------------------------

Time:
O(n)

Space:
O(1)

Why O(1)?

Because the array always contains only 26 positions.

# ------------------------------------------------------------

# WHEN TO USE

# ------------------------------------------------------------

Use a fixed frequency / boolean array when:

* Alphabet is known
* Alphabet is small
* Need character presence
* Need character frequency
* Characters are lowercase English letters

# ------------------------------------------------------------

# WHEN NOT TO USE

# ------------------------------------------------------------

If characters can be:

* Unicode
* Arbitrary symbols
* Huge / unknown character set

then a map/set may be more appropriate.

# ------------------------------------------------------------

# OA TIP

# ------------------------------------------------------------

Whenever you see:

"lowercase English letters"

immediately think:

```cpp
int freq[26] = {};
```

or:

```cpp
bool seen[26] = {};
```

# ------------------------------------------------------------

# MEMORY TRIGGER

# ------------------------------------------------------------

PANGRAM
↓
26 LETTERS
↓
ARRAY[26]
↓
CHECK ALL

# ============================================================

# 5. PROBLEM 3 — REVERSE STRING

# ============================================================

## PROBLEM

Given a string/character array, reverse it IN-PLACE.

Example:

Input:
"hello"

Output:
"olleh"

# ------------------------------------------------------------

# PATTERN

# ------------------------------------------------------------

REVERSE
↓
TWO POINTERS

# ------------------------------------------------------------

# MENTAL MODEL

# ------------------------------------------------------------

H E L L O
↑       ↑
L       R

Swap:

O E L L H

Move inward:

O E L L H
↑   ↑

Continue until:

left >= right

# ------------------------------------------------------------

# ALGORITHM

# ------------------------------------------------------------

1. `left = 0`
2. `right = n - 1`
3. Swap `s[left]` and `s[right]`.
4. `left++`
5. `right--`
6. Stop when `left >= right`.

# ------------------------------------------------------------

# C++ SOLUTION

# ------------------------------------------------------------

```cpp
void reverseString(string& s) {

    int left = 0;
    int right = s.size() - 1;

    while (left < right) {

        swap(s[left], s[right]);

        left++;
        right--;
    }
}
```

# ------------------------------------------------------------

# DRY RUN

# ------------------------------------------------------------

"HELLO"

Initial:

H E L L O
↑       ↑

Swap H and O:

O E L L H

Move:

O E L L H
↑   ↑

Swap E and L:

O L L E H

Move to center.

Answer:

"OLLEH"

# ------------------------------------------------------------

# COMPLEXITY

# ------------------------------------------------------------

Time:
O(n)

Space:
O(1)

# ------------------------------------------------------------

# WHEN TO USE

# ------------------------------------------------------------

Use TWO POINTERS when:

* Reversing
* Comparing both ends
* Checking palindrome
* Modifying in-place
* Working from both ends

# ------------------------------------------------------------

# COMMON MISTAKE

# ------------------------------------------------------------

If the problem says:

"in-place"

don't unnecessarily create another string.

# ------------------------------------------------------------

# CONNECTION

# ------------------------------------------------------------

REVERSE:

LEFT ↔ RIGHT

PALINDROME:

LEFT == RIGHT?

Both use:

TWO POINTERS.

# ------------------------------------------------------------

# MEMORY TRIGGER

# ------------------------------------------------------------

REVERSE
↓
LEFT + RIGHT
↓
SWAP
↓
MOVE INWARD

# ============================================================

# 6. PROBLEM 4 — STRING COMPRESSION

# ============================================================

## PROBLEM

Given an array of characters, compress consecutive repeated
characters.

For each group:

* Write the character.
* If count > 1, write the count.
* Modify the array IN-PLACE.
* Return the compressed length.

Example:

Input:

a a b b c c c

Output:

a 2 b 2 c 3

Length:

6

# ------------------------------------------------------------

# PATTERN

# ------------------------------------------------------------

STRING COMPRESSION
↓
CONSECUTIVE GROUPS
↓
COUNT EACH GROUP
↓
READ POINTER + WRITE POINTER

# ------------------------------------------------------------

# KEY OBSERVATION

# ------------------------------------------------------------

We need to:

READ the original array

while simultaneously:

WRITE the compressed array.

Therefore:

i
↓
READ POINTER

write
↓
WRITE POINTER

# ------------------------------------------------------------

# ALGORITHM

# ------------------------------------------------------------

1. `i = 0`
2. `write = 0`
3. Take current character.
4. Count consecutive occurrences.
5. Write the character.
6. If count > 1:

   * Convert count to string.
   * Write every digit.
7. Continue until end.
8. Return `write`.

# ------------------------------------------------------------

# C++ SOLUTION

# ------------------------------------------------------------

```cpp
int compress(vector<char>& chars) {

    int i = 0;
    int write = 0;

    while (i < chars.size()) {

        char current = chars[i];

        int count = 0;

        // Count current group
        while (i < chars.size() && chars[i] == current) {
            i++;
            count++;
        }

        // Write character
        chars[write] = current;
        write++;

        // Write count
        if (count > 1) {

            string num = to_string(count);

            for (char digit : num) {
                chars[write] = digit;
                write++;
            }
        }
    }

    return write;
}
```

# ------------------------------------------------------------

# DRY RUN

# ------------------------------------------------------------

Input:

a a b b c c c

Initial:

i = 0
write = 0

GROUP 1:

a a

count = 2

Write:

a 2

write = 2

GROUP 2:

b b

count = 2

Write:

b 2

write = 4

GROUP 3:

c c c

count = 3

Write:

c 3

write = 6

Final:

a 2 b 2 c 3

Return:

6

# ------------------------------------------------------------

# IMPORTANT TRICK — MULTI-DIGIT COUNT

# ------------------------------------------------------------

Suppose:

'a' appears 12 times.

Compressed form:

a 1 2

NOT:

a 12 as one character.

Therefore:

```cpp
string num = to_string(count);

for (char digit : num)
    chars[write++] = digit;
```

# ------------------------------------------------------------

# VERY IMPORTANT DISTINCTION

# ------------------------------------------------------------

Compression works on:

CONSECUTIVE frequency.

Example:

a b a

Total frequency:

a = 2

But consecutive groups are:

a
b
a

So compressed result remains:

a b a

NOT:

a2b

# ------------------------------------------------------------

# COMPLEXITY

# ------------------------------------------------------------

Time:
O(n)

Auxiliary Space:
O(1)

# ------------------------------------------------------------

# WHEN TO USE

# ------------------------------------------------------------

Think READ + WRITE POINTER when:

* Modifying array in-place
* Compressing
* Removing elements
* Overwriting unwanted values
* Processing groups

# ------------------------------------------------------------

# WHEN NOT TO USE

# ------------------------------------------------------------

Don't confuse this with:

TOTAL CHARACTER FREQUENCY.

Compression cares about:

CONSECUTIVE GROUPS.

# ------------------------------------------------------------

# OA TIP

# ------------------------------------------------------------

Whenever you see:

"consecutive"

think:

GROUP

Then:

GROUP
↓
COUNT
↓
WRITE

# ------------------------------------------------------------

# MEMORY TRIGGER

# ------------------------------------------------------------

COMPRESSION
↓
READ GROUP
↓
COUNT
↓
WRITE CHARACTER
↓
WRITE COUNT

# ============================================================

# 7. PROBLEM 5 — VALID PARENTHESES

# ============================================================

## PROBLEM

Given a string containing:

()
{}
[]

determine whether it contains valid parentheses.

A valid string must:

1. Every opening bracket have a matching closing bracket.
2. Brackets close in the correct order.
3. No closing bracket appears without its opening bracket.

Examples:

"()"
→ true

"({[]})"
→ true

"([)]"
→ false

# ------------------------------------------------------------

# PATTERN

# ------------------------------------------------------------

VALID PARENTHESES
↓
NESTING
↓
LIFO
↓
STACK

# ------------------------------------------------------------

# WHY STACK?

# ------------------------------------------------------------

Consider:

({[]})

Opening order:

(
{
[

Closing order:

]
}
)

The LAST opening bracket must be closed FIRST.

That is:

LIFO

Last In First Out.

Exactly what a stack provides.

# ------------------------------------------------------------

# MENTAL MODEL

# ------------------------------------------------------------

OPENING
↓
PUSH

CLOSING
↓
CHECK TOP
↓
MATCH?
/ 
YES  NO
↓    ↓
POP  FALSE

# ------------------------------------------------------------

# ALGORITHM

# ------------------------------------------------------------

For every character:

If opening:

( { [

→ push

If closing:

) } ]

→

1. Stack must not be empty.
2. Top must match current closing bracket.
3. Pop.

At the end:

Stack MUST be empty.

# ------------------------------------------------------------

# C++ SOLUTION

# ------------------------------------------------------------

```cpp
bool isValid(string s) {

    stack<char> st;

    for (char c : s) {

        if (c == '(' || c == '{' || c == '[') {

            st.push(c);

        } else {

            if (st.empty())
                return false;

            if ((c == ')' && st.top() != '(') ||
                (c == '}' && st.top() != '{') ||
                (c == ']' && st.top() != '[')) {

                return false;
            }

            st.pop();
        }
    }

    return st.empty();
}
```

# ------------------------------------------------------------

# DRY RUN

# ------------------------------------------------------------

s = "({[]})"

Read '(':

stack:
(

Read '{':

stack:
(
{

Read '[':

stack:
(
{
[

Read ']':

top = '['

MATCH

pop

stack:
(
{

Read '}':

top = '{'

MATCH

pop

stack:
(

Read ')':

top = '('

MATCH

pop

stack:

EMPTY

Answer:

true

# ------------------------------------------------------------

# WHY CHECK st.empty() AT THE END?

# ------------------------------------------------------------

Consider:

"((("

There is no wrong closing bracket.

But it is still invalid.

At the end:

stack = (( (

Therefore:

```cpp
return st.empty();
```

is essential.

# ------------------------------------------------------------

# IMPORTANT TRAP

# ------------------------------------------------------------

Checking only counts is WRONG.

Example:

"([)]"

Counts are balanced:

( = 1
) = 1
[ = 1
] = 1

But ordering is wrong.

Therefore:

BALANCED COUNT ≠ VALID PARENTHESES

We need:

ORDER

→ STACK.

# ------------------------------------------------------------

# COMPLEXITY

# ------------------------------------------------------------

Time:
O(n)

Space:
O(n)

# ------------------------------------------------------------

# WHEN TO USE STACK

# ------------------------------------------------------------

Think STACK when:

* Nested structures
* Matching brackets
* Last opened → first closed
* Undo operations
* LIFO behavior
* Previous unresolved item must be handled first

# ------------------------------------------------------------

# MEMORY TRIGGER

# ------------------------------------------------------------

OPEN
↓
PUSH

CLOSE
↓
CHECK TOP
↓
MATCH?
↓
POP

END
↓
EMPTY?

# ============================================================

# 8. PROBLEM 6 — LONGEST SUBSTRING WITHOUT REPEATING CHARACTERS

# ============================================================

## PROBLEM

Given a string `s`, find the length of the longest substring that
contains no repeating characters.

Example:

Input:

"abcabcbb"

Output:

3

Longest valid substring:

"abc"

# ------------------------------------------------------------

# PATTERN

# ------------------------------------------------------------

LONGEST
+
SUBSTRING
+
NO REPEATING
↓
SLIDING WINDOW

# ------------------------------------------------------------

# FIRST CONCEPT — SUBSTRING

# ------------------------------------------------------------

SUBSTRING = CONTIGUOUS

Example:

"abcdef"

"bcd"

→ substring

"ace"

→ NOT a substring

# ------------------------------------------------------------

# KEY OBSERVATION

# ------------------------------------------------------------

We need the:

LONGEST

CONTIGUOUS

WINDOW

that satisfies:

NO DUPLICATES.

# ------------------------------------------------------------

# MENTAL MODEL

# ------------------------------------------------------------

left
↓
[a b c]
↑
right

RIGHT:

EXPANDS WINDOW

LEFT:

SHRINKS WINDOW

# ------------------------------------------------------------

# ALGORITHM

# ------------------------------------------------------------

1. Set `left = 0`.
2. Move `right` from left to right.
3. Add `s[right]` to frequency.
4. If duplicate occurs:

   * Move `left`.
   * Remove characters from the frequency.
5. Once valid:

   * Update maximum length.

# ------------------------------------------------------------

# C++ SOLUTION

# ------------------------------------------------------------

```cpp
int lengthOfLongestSubstring(string s) {

    int freq[256] = {};

    int left = 0;
    int ans = 0;

    for (int right = 0; right < s.size(); right++) {

        freq[s[right]]++;

        while (freq[s[right]] > 1) {

            freq[s[left]]--;
            left++;
        }

        ans = max(ans, right - left + 1);
    }

    return ans;
}
```

# ------------------------------------------------------------

# DRY RUN

# ------------------------------------------------------------

s = "abcabcbb"

RIGHT = 0

Window:

"a"

Valid.

ans = 1

RIGHT = 1

Window:

"ab"

Valid.

ans = 2

RIGHT = 2

Window:

"abc"

Valid.

ans = 3

RIGHT = 3

Add 'a':

Window:

"abca"

Duplicate!

Shrink from LEFT.

Remove 'a'.

Window:

"bca"

Valid.

ans = 3

RIGHT = 4

Add 'b':

Window temporarily:

"bcab"

Duplicate b.

Shrink:

"cab"

Valid.

ans = 3

Continue.

Final answer:

3

# ------------------------------------------------------------

# WHY WHILE, NOT IF?

# ------------------------------------------------------------

When a duplicate appears, moving `left` once may not always be
enough.

Therefore:

```cpp
while (freq[s[right]] > 1)
```

not simply:

```cpp
if (...)
```

# ------------------------------------------------------------

# CORE SLIDING WINDOW IDEA

# ------------------------------------------------------------

RIGHT EXPANDS

```
    ↓
```

WINDOW BECOMES INVALID

```
    ↓
```

LEFT SHRINKS

```
    ↓
```

WINDOW BECOMES VALID

```
    ↓
```

UPDATE ANSWER

# ------------------------------------------------------------

# COMPLEXITY

# ------------------------------------------------------------

Time:
O(n)

Space:
O(1)

for a fixed character set such as ASCII.

# ------------------------------------------------------------

# WHY O(n)?

# ------------------------------------------------------------

Even though there is a nested `while`:

Each character:

* enters the window once
* leaves the window once

Therefore total pointer movement is O(n).

# ------------------------------------------------------------

# WHEN TO USE SLIDING WINDOW

# ------------------------------------------------------------

Strong clues:

* substring
* subarray
* contiguous
* longest
* shortest
* maximum
* minimum
* at most K
* no duplicates
* satisfy a condition

# ------------------------------------------------------------

# WHEN NOT TO USE

# ------------------------------------------------------------

Don't automatically use sliding window for:

SUBSEQUENCE

A subsequence does NOT have to be contiguous.

Example:

"ace"

is a subsequence of:

"abcde"

but not a substring.

# ------------------------------------------------------------

# COMMON MISTAKE

# ------------------------------------------------------------

When duplicate appears:

DO NOT RESET THE ENTIRE WINDOW.

Instead:

SHRINK FROM LEFT.

That is the key advantage of sliding window.

# ------------------------------------------------------------

# MEMORY TRIGGER

# ------------------------------------------------------------

LONGEST SUBSTRING
↓
SLIDING WINDOW
↓
RIGHT EXPANDS
↓
INVALID?
↓
LEFT SHRINKS
↓
UPDATE MAX

# ============================================================

# 9. PROBLEM 7 — GROUP ANAGRAMS

# ============================================================

## PROBLEM

Given an array of strings, group all anagrams together.

Example:

Input:

[
"eat",
"tea",
"tan",
"ate",
"nat",
"bat"
]

Output:

[
["eat","tea","ate"],
["tan","nat"],
["bat"]
]

# ------------------------------------------------------------

# PATTERN

# ------------------------------------------------------------

GROUP ANAGRAMS
↓
SAME CHARACTERS
↓
SAME FREQUENCY
↓
COMMON SIGNATURE
↓
HASH MAP

# ------------------------------------------------------------

# WHAT IS AN ANAGRAM?

# ------------------------------------------------------------

Two strings are anagrams if:

* Same characters
* Same frequency
* Different order allowed

Example:

eat

tea

ate

All contain:

a = 1
e = 1
t = 1

Therefore they are anagrams.

# ------------------------------------------------------------

# KEY IDEA

# ------------------------------------------------------------

We need to convert every anagram into the SAME KEY.

Two major methods:

1. SORTING
2. FREQUENCY SIGNATURE

# ============================================================

# METHOD 1 — SORTING

# ============================================================

eat
↓
aet

tea
↓
aet

ate
↓
aet

All produce:

"aet"

Therefore:

same key
↓
same group

# ------------------------------------------------------------

# C++ SOLUTION — SORTING

# ------------------------------------------------------------

```cpp
vector<vector<string>> groupAnagrams(vector<string>& strs) {

    unordered_map<string, vector<string>> mp;

    for (string word : strs) {

        string key = word;

        sort(key.begin(), key.end());

        mp[key].push_back(word);
    }

    vector<vector<string>> ans;

    for (auto& [key, group] : mp) {
        ans.push_back(group);
    }

    return ans;
}
```

# ------------------------------------------------------------

# DRY RUN

# ------------------------------------------------------------

eat
→ aet

tea
→ aet

tan
→ ant

ate
→ aet

nat
→ ant

bat
→ abt

Hash map:

aet → [eat, tea, ate]

ant → [tan, nat]

abt → [bat]

# ------------------------------------------------------------

# COMPLEXITY — SORTING

# ------------------------------------------------------------

Let:

n = number of strings

k = average string length

Sorting each string:

O(k log k)

For n strings:

O(n × k log k)

Space:

O(nk)

because we store the grouped strings / keys.

# ============================================================

# METHOD 2 — FREQUENCY SIGNATURE

# ============================================================

Instead of sorting each word:

Create:

freq[26]

For:

"eat"

Frequency:

a = 1
e = 1
t = 1

For:

"tea"

Frequency is exactly the same.

Therefore:

same frequency
↓
same signature
↓
same group

# ------------------------------------------------------------

# WHEN SORTING IS BETTER

# ------------------------------------------------------------

Use sorting when:

* You want simple code
* Constraints are moderate
* OA speed matters
* Easy explanation is preferred

# ------------------------------------------------------------

# WHEN FREQUENCY IS BETTER

# ------------------------------------------------------------

Use frequency signature when:

* Only lowercase English letters
* Strings can be long
* Need better asymptotic complexity
* Interviewer asks for optimization

# ------------------------------------------------------------

# IMPORTANT CONNECTION

# ------------------------------------------------------------

PANGRAM:

character
↓
frequency

GROUP ANAGRAMS:

word
↓
frequency signature
↓
hash map

Same underlying concept:

CHARACTER FREQUENCY

# ------------------------------------------------------------

# GENERAL PATTERN

# ------------------------------------------------------------

If a problem says:

"Group things that are equivalent"

ask:

"What makes two objects equivalent?"

For anagrams:

SAME CHARACTER COUNTS

Therefore:

NORMALIZE
↓
HASH MAP
↓
GROUP

# ------------------------------------------------------------

# COMMON MISTAKE

# ------------------------------------------------------------

Do NOT use the original word as the key.

"eat"

and:

"tea"

are different strings.

Need:

COMMON NORMALIZED KEY

# ------------------------------------------------------------

# MEMORY TRIGGER

# ------------------------------------------------------------

ANAGRAM
↓
SAME CHARACTERS
↓
SAME FREQUENCY
↓
SAME KEY
↓
HASH MAP
↓
GROUP

# ============================================================

# 10. PROBLEM 8 — WORD BREAK / CONCATENATED-WORD STRING

# ============================================================

## PROBLEM

Given a string `s` and a dictionary `wordDict`, determine whether
`s` can be formed by concatenating one or more dictionary words.

Each dictionary word may be used multiple times.

Example:

s = "leetcode"

wordDict = ["leet", "code"]

Output:

true

Because:

"leet" + "code"
= "leetcode"

# ------------------------------------------------------------

# COMMON NAME

# ------------------------------------------------------------

This pattern is commonly known as:

WORD BREAK

# ------------------------------------------------------------

# PATTERN

# ------------------------------------------------------------

WORD BREAK
↓
PREFIX PROBLEM
↓
DYNAMIC PROGRAMMING
+
HASH SET

# ------------------------------------------------------------

# MOST IMPORTANT DP DEFINITION

# ------------------------------------------------------------

Define:

dp[i]

as:

"Can the FIRST `i` characters of `s` be formed using
dictionary words?"

This definition should be remembered exactly.

# ------------------------------------------------------------

# WHY dp[0] = true?

# ------------------------------------------------------------

`dp[0]` represents:

Can the first 0 characters be formed?

YES.

The empty prefix requires zero words.

Therefore:

```cpp
dp[0] = true;
```

This is what allows the first dictionary word to be selected.

# ------------------------------------------------------------

# TRANSITION

# ------------------------------------------------------------

To calculate:

dp[i]

try every previous split:

0 ... j ... i

If:

dp[j] == true

AND:

s[j ... i-1]

is a dictionary word,

then:

dp[i] = true.

# ------------------------------------------------------------

# FORMULA

# ------------------------------------------------------------

```text
dp[i] = true

if:

dp[j] == true

AND

s.substr(j, i-j) exists in dictionary
```

# ------------------------------------------------------------

# MENTAL MODEL

# ------------------------------------------------------------

STRING:

leetcode

Try:

0 → 4

"leet"

exists?

YES

Therefore:

dp[4] = true

Then:

4 → 8

"code"

exists?

YES

Therefore:

dp[8] = true

Answer:

dp[8] = true

# ------------------------------------------------------------

# C++ SOLUTION

# ------------------------------------------------------------

```cpp
bool wordBreak(string s, vector<string>& wordDict) {

    unordered_set<string> dict;

    for (const string& word : wordDict) {
        dict.insert(word);
    }

    int n = s.size();

    vector<bool> dp(n + 1, false);

    dp[0] = true;

    for (int i = 1; i <= n; i++) {

        for (int j = 0; j < i; j++) {

            string part = s.substr(j, i - j);

            if (dp[j] && dict.count(part)) {

                dp[i] = true;
                break;
            }
        }
    }

    return dp[n];
}
```

# ------------------------------------------------------------

# DETAILED DRY RUN

# ------------------------------------------------------------

s:

"leetcode"

Dictionary:

["leet", "code"]

n = 8

Initial DP:

index:
0 1 2 3 4 5 6 7 8

dp:
T F F F F F F F F

# i = 1

Try:

"l"

Not in dictionary.

dp[1] = false

# i = 2

Try:

"le"

Not in dictionary.

dp[2] = false

# i = 3

Try:

"lee"

Not in dictionary.

dp[3] = false

# i = 4

Try:

j = 0

substring:

"leet"

Dictionary?

YES

dp[0] = true

Therefore:

dp[4] = true

DP:

T F F F T F F F F

# i = 5

Useful previous true state:

j = 4

substring:

"c"

Not in dictionary.

dp[5] = false

# i = 6

j = 4

substring:

"co"

Not in dictionary.

dp[6] = false

# i = 7

j = 4

substring:

"cod"

Not in dictionary.

dp[7] = false

# i = 8

j = 4

dp[4] = true

substring:

"code"

Dictionary?

YES

Therefore:

dp[8] = true

Final DP:

T F F F T F F F T

Answer:

true

# ------------------------------------------------------------

# SECOND EXAMPLE

# ------------------------------------------------------------

s:

"applepenapple"

wordDict:

["apple", "pen"]

Break:

apple | pen | apple

Therefore:

true.

# ------------------------------------------------------------

# FALSE EXAMPLE

# ------------------------------------------------------------

s:

"catsandog"

wordDict:

["cats", "dog", "sand", "and", "cat"]

Possible:

cat | sand | og

But:

"og" does not exist.

Another:

cats | and | og

Again:

"og" does not exist.

Therefore:

false.

# ------------------------------------------------------------

# WHY HASH SET?

# ------------------------------------------------------------

We only need:

"Does this word exist?"

We don't need:

* Frequency
* Ordering
* Associated value

Therefore:

HASH SET

is appropriate.

# ------------------------------------------------------------

# WHY DP?

# ------------------------------------------------------------

Because one valid word is not enough.

We need to know whether:

PREVIOUS PREFIX

was already constructible.

Example:

leet | code

When checking "code", we rely on:

dp[4] = true

# ------------------------------------------------------------

# COMPLEXITY

# ------------------------------------------------------------

There are O(n²) possible `(j, i)` pairs.

With straightforward `substr()` and hashing, the practical/worst-case
cost can be higher due to substring creation and hashing.

For the standard OA implementation:

Time is commonly treated as approximately:

O(n²)

under simplified substring/hash assumptions.

With actual string-copy costs:

it can approach O(n³) in the worst case.

Space:

O(n + dictionary size)

# ------------------------------------------------------------

# OPTIMIZATION IDEA

# ------------------------------------------------------------

Let:

maxWordLength = longest word in dictionary.

Instead of checking every possible `j`, only check word lengths
that can actually exist in the dictionary.

This avoids unnecessary substring checks.

# ------------------------------------------------------------

# WHEN TO USE

# ------------------------------------------------------------

Strong clues:

* Can string be formed?
* Can string be segmented?
* Can string be split?
* Dictionary of words
* Concatenate words
* Break into valid words
* Prefix can be formed

# ------------------------------------------------------------

# WHEN NOT TO USE

# ------------------------------------------------------------

If the problem simply asks:

"Does this word exist in the dictionary?"

Use:

HASH SET

No DP is needed.

DP is needed when:

MULTIPLE WORDS

must combine to form:

THE ENTIRE STRING.

# ------------------------------------------------------------

# IMPORTANT DP RECOGNITION

# ------------------------------------------------------------

Whenever you see:

"Can the first i characters be formed?"

Think:

```text
dp[i]
```

This is:

PREFIX DP

# ------------------------------------------------------------

# MEMORY TRIGGER

# ------------------------------------------------------------

WORD BREAK
↓
PREFIX
↓
dp[i]
↓
TRY SPLIT j
↓
dp[j] + VALID WORD
↓
dp[i] = true

# ============================================================

# 11. CONNECTIONS BETWEEN ALL 8 PROBLEMS

# ============================================================

# ------------------------------------------------------------

# CONNECTION 1 — CHARACTER FREQUENCY

# ------------------------------------------------------------

PANGRAM
↓
CHARACTER PRESENCE

GROUP ANAGRAMS
↓
CHARACTER FREQUENCY

LONGEST SUBSTRING
↓
CHARACTER FREQUENCY

STRING COMPRESSION
↓
CONSECUTIVE FREQUENCY

The underlying concept:

TRACK CHARACTER INFORMATION

But the purpose changes.

# ------------------------------------------------------------

# CONNECTION 2 — TWO POINTERS

# ------------------------------------------------------------

LENGTH OF LAST WORD
↓
RIGHT → LEFT

REVERSE STRING
↓
LEFT ↔ RIGHT

LONGEST SUBSTRING
↓
LEFT → RIGHT WINDOW

STRING COMPRESSION
↓
READ + WRITE

Same broad idea:

CONTROL HOW YOU MOVE THROUGH THE STRING.

# ------------------------------------------------------------

# CONNECTION 3 — HASHING

# ------------------------------------------------------------

PANGRAM
↓
FREQUENCY / PRESENCE

LONGEST SUBSTRING
↓
FREQUENCY MAP

GROUP ANAGRAMS
↓
SIGNATURE + HASH MAP

WORD BREAK
↓
HASH SET

# ------------------------------------------------------------

# CONNECTION 4 — STACK

# ------------------------------------------------------------

VALID PARENTHESES
↓
NESTING
↓
LIFO
↓
STACK

# ------------------------------------------------------------

# CONNECTION 5 — DP

# ------------------------------------------------------------

WORD BREAK
↓
PREFIX DP

Question:

"Can the previous prefix be formed?"

Then:

"Can I append one valid dictionary word?"

# ============================================================

# 12. MASTER STORY → PATTERN CHEAT SHEET

# ============================================================

STORY
│
├── "Length of final word"
│      ↓
│   RIGHT → LEFT
│
├── "Contains every alphabet letter"
│      ↓
│   ARRAY[26]
│
├── "Reverse"
│      ↓
│   TWO POINTERS
│
├── "Compress consecutive characters"
│      ↓
│   READ + WRITE + COUNT
│
├── "Valid / nested brackets"
│      ↓
│   STACK
│
├── "Longest substring without duplicate"
│      ↓
│   SLIDING WINDOW
│
├── "Group anagrams"
│      ↓
│   SIGNATURE + HASH MAP
│
└── "Can string be formed from dictionary?"
↓
DP + HASH SET

# ============================================================

# 13. MASTER DATA STRUCTURE CHEAT SHEET

# ============================================================

QUESTION
│
├── Need character presence?
│      ↓
│   bool[26]
│
├── Need character frequency?
│      ↓
│   int[26] / map
│
├── Need reverse?
│      ↓
│   TWO POINTERS
│
├── Need consecutive groups?
│      ↓
│   READ + COUNT
│
├── Need nested matching?
│      ↓
│   STACK
│
├── Need longest/shortest substring?
│      ↓
│   SLIDING WINDOW
│
├── Need group equivalent strings?
│      ↓
│   HASH MAP + SIGNATURE
│
└── Need dictionary segmentation?
↓
DP + HASH SET

# ============================================================

# 14. WHEN TO USE WHAT?

# ============================================================

## FREQUENCY ARRAY

Use when:

* Alphabet is small
* Alphabet is known
* Need counts
* Need character presence
* Need compare character frequencies

Examples:

* Pangram
* Group Anagrams
* Longest Substring

## HASH MAP

Use when:

* Keys are dynamic
* Need grouping
* Need frequency of arbitrary objects
* Need key → value relationship

Example:

Group Anagrams

## HASH SET

Use when:

* Only existence matters
* Need fast membership lookup
* No associated value is required

Example:

Word Break dictionary

## STACK

Use when:

* Nested structures
* Matching brackets
* LIFO behavior
* Last opened must close first

Example:

Valid Parentheses

## TWO POINTERS

Use when:

* Working from both ends
* Reversing
* Comparing ends
* In-place modification
* Maintaining two positions

Examples:

* Reverse String
* Length of Last Word
* Compression

## SLIDING WINDOW

Use when:

* Substring
* Subarray
* Contiguous
* Longest
* Shortest
* Maximum
* Minimum
* At most K
* No duplicates
* Maintain a validity condition

Example:

Longest Substring Without Repeating

## DP

Use when:

* Multiple choices exist
* Previous results can be reused
* Prefix/suffix states matter
* Asked whether something can be formed
* Problem can be divided into smaller states

Example:

Word Break

# ============================================================

# 15. WHEN NOT TO USE WHAT

# ============================================================

## DON'T USE SLIDING WINDOW

Automatically for every substring problem.

First ask:

Is the condition maintainable while moving left/right?

If yes:

Sliding Window is likely useful.

Also remember:

SUBSTRING = CONTIGUOUS

SUBSEQUENCE = NOT NECESSARILY CONTIGUOUS.

## DON'T USE STACK

Just because brackets exist.

The key clue is:

NESTING / ORDER.

## DON'T USE HASH MAP

When the possible characters are only:

a-z

A fixed array of 26 is usually simpler.

## DON'T USE DP

If a direct:

* counting
* two-pointer
* hashing
* stack
* greedy

solution already solves the problem.

DP should solve a real overlapping-subproblem/state problem.

## DON'T USE SORTING

Automatically for Group Anagrams.

Sorting is simple and valid, but frequency signatures can be
better when the alphabet is fixed and strings are long.

# ============================================================

# 16. COMMON OA TRAPS

# ============================================================

## TRAP 1 — SUBSTRING VS SUBSEQUENCE

SUBSTRING:

CONTIGUOUS

SUBSEQUENCE:

NOT NECESSARILY CONTIGUOUS.

## TRAP 2 — CONSECUTIVE VS TOTAL FREQUENCY

Input:

a b a

Total:

a = 2

But consecutive groups:

a
b
a

Compression:

a b a

NOT:

a2b

## TRAP 3 — VALID PARENTHESES

Equal counts are not enough.

"([)]"

is invalid.

Need:

CORRECT ORDER.

## TRAP 4 — GROUP ANAGRAMS

Don't compare every pair if avoidable.

Normalize every word.

Then:

SIGNATURE → HASH MAP.

## TRAP 5 — WORD BREAK

Don't only check:

```cpp
dict.count(s)
```

The entire string may need multiple dictionary words.

## TRAP 6 — STRING COMPRESSION

10 repetitions:

a a a a a a a a a a

becomes:

a 1 0

NOT:

a 10 as one character.

## TRAP 7 — LONGEST SUBSTRING

When duplicate appears:

DO NOT RESET.

Shrink from LEFT.

## TRAP 8 — DP DEFINITION

Don't randomly define `dp`.

First clearly state:

"What exactly does dp[i] mean?"

For Word Break:

`dp[i] = whether first i characters can be formed.`

# ============================================================

# 17. INTERVIEW EXPLANATION TEMPLATES

# ============================================================

## LENGTH OF LAST WORD

"I start from the end because only the last word matters. I first
skip trailing spaces and then count characters until I reach another
space or the beginning."

## PANGRAM

"I only need to know whether each of the 26 English letters appears,
so I use a fixed-size boolean or frequency array."

## REVERSE STRING

"I use two pointers, one at each end, and swap the characters while
moving toward the center. This gives O(n) time and O(1) extra space."

## STRING COMPRESSION

"I process the string in consecutive groups. One pointer reads and
counts a group, while another pointer writes the compressed result
in-place."

## VALID PARENTHESES

"I use a stack because brackets close in the reverse order in which
they are opened. Every closing bracket must match the stack top."

## LONGEST SUBSTRING

"I maintain a sliding window containing unique characters. The right
pointer expands the window, and when it becomes invalid, the left
pointer shrinks it until it becomes valid again."

## GROUP ANAGRAMS

"I normalize each word into a common signature. Using sorted
characters as the key makes all anagrams map to the same hash-map
entry."

## WORD BREAK

"I use prefix DP. `dp[i]` represents whether the first `i` characters
can be formed. For every possible previous split `j`, if `dp[j]`
is true and the substring from `j` to `i-1` is in the dictionary,
then `dp[i]` becomes true."

# ============================================================

# 18. MASTER COMPLEXITY TABLE

# ============================================================

| # | Problem             | Pattern            | Time              | Space             |
| - | ------------------- | ------------------ | ----------------- | ----------------- |
| 1 | Length of Last Word | Right-to-Left      | O(n)              | O(1)              |
| 2 | Pangram             | Frequency Array    | O(n)              | O(1)              |
| 3 | Reverse String      | Two Pointers       | O(n)              | O(1)              |
| 4 | String Compression  | Read + Write       | O(n)              | O(1)              |
| 5 | Valid Parentheses   | Stack              | O(n)              | O(n)              |
| 6 | Longest Substring   | Sliding Window     | O(n)              | O(1)*             |
| 7 | Group Anagrams      | Hash Map + Sorting | O(n·k log k)      | O(nk)             |
| 8 | Word Break          | DP + Hash Set      | ~O(n²) to O(n³)** | O(n + dictionary) |

`*` O(1) when the character set is fixed, such as ASCII.

`**` The exact complexity depends on substring creation, hashing,
dictionary constraints, and implementation details. The standard
DP formulation has O(n²) state transitions, while repeated
`substr()` creation can add another factor.

# ============================================================

# 19. FINAL 8-PROBLEM RECOGNITION SHEET

# ============================================================

## 1. LENGTH OF LAST WORD

Story:

"Find length of final word"

Think:

RIGHT → LEFT

Core:

SKIP SPACES → COUNT

## 2. PANGRAM

Story:

"Does sentence contain every alphabet letter?"

Think:

ARRAY[26]

Core:

CHECK ALL 26

## 3. REVERSE STRING

Story:

"Reverse in-place"

Think:

TWO POINTERS

Core:

SWAP LEFT/RIGHT

## 4. STRING COMPRESSION

Story:

"Compress consecutive characters"

Think:

READ + WRITE + COUNT

Core:

GROUP → COUNT → WRITE

## 5. VALID PARENTHESES

Story:

"Are brackets valid/nested?"

Think:

STACK

Core:

OPEN → PUSH
CLOSE → MATCH TOP → POP

## 6. LONGEST SUBSTRING WITHOUT REPEATING

Story:

"Longest contiguous section with no duplicate"

Think:

SLIDING WINDOW

Core:

RIGHT EXPANDS → LEFT SHRINKS

## 7. GROUP ANAGRAMS

Story:

"Group words with same characters"

Think:

SIGNATURE + HASH MAP

Core:

NORMALIZE → HASH → GROUP

## 8. WORD BREAK

Story:

"Can string be formed from dictionary words?"

Think:

DP + HASH SET

Core:

dp[j] + valid word → dp[i]

# ============================================================

# 20. ULTRA-SHORT OA CHEAT SHEET

# ============================================================

LAST WORD
→ RIGHT TO LEFT

PANGRAM
→ ARRAY[26]

REVERSE
→ TWO POINTERS

COMPRESSION
→ READ + WRITE + COUNT

PARENTHESES
→ STACK

LONGEST UNIQUE SUBSTRING
→ SLIDING WINDOW

ANAGRAMS
→ SIGNATURE + HASH MAP

WORD BREAK
→ PREFIX DP + HASH SET

# ============================================================

# 21. STRING PROBLEM DECISION TREE

# ============================================================

START
│
↓
What is the problem asking?
│
├── LAST / TRAILING?
│      ↓
│   RIGHT → LEFT
│
├── CHARACTER COUNT / PRESENCE?
│      ↓
│   FREQUENCY ARRAY / HASH MAP
│
├── REVERSE / BOTH ENDS?
│      ↓
│   TWO POINTERS
│
├── CONSECUTIVE GROUPS?
│      ↓
│   READ + COUNT
│
├── NESTED BRACKETS?
│      ↓
│   STACK
│
├── LONGEST / SHORTEST SUBSTRING?
│      ↓
│   SLIDING WINDOW
│
├── GROUP ANAGRAMS / EQUIVALENT STRINGS?
│      ↓
│   SIGNATURE + HASH MAP
│
└── CAN STRING BE BUILT / SEGMENTED?
↓
DP + HASH SET

# ============================================================

# 22. THE MOST IMPORTANT PATTERN CONNECTIONS

# ============================================================

## CONNECTION A — FREQUENCY

Pangram
↓
Character presence

Group Anagrams
↓
Character frequency

Longest Substring
↓
Character frequency

Compression
↓
Consecutive frequency

The common idea:

TRACK CHARACTER INFORMATION.

## CONNECTION B — POINTERS

Length of Last Word
↓
Right → Left

Reverse
↓
Left ↔ Right

Longest Substring
↓
Left → Right window

Compression
↓
Read + Write

The common idea:

CONTROL POINTER MOVEMENT.

## CONNECTION C — HASHING

Frequency
↓
Hash Map / Set

Signature
↓
Hash Map

Dictionary lookup
↓
Hash Set

The common idea:

FAST LOOKUP.

## CONNECTION D — STACK

Nested structure
↓
LIFO
↓
Stack

## CONNECTION E — DP

Can prefix be formed?
↓
dp[i]

Can another valid word extend it?
↓
dp[i] = true

# ============================================================

# 23. HIGH-CONFIDENCE OA CHECKLIST

# ============================================================

Before coding any String problem:

[ ] Identify whether characters must be contiguous.

[ ] Decide whether this is substring or subsequence.

[ ] Look for "last" / "trailing" → consider right-to-left.

[ ] Look for character counting → frequency array/map.

[ ] Look for "reverse" → two pointers.

[ ] Look for "consecutive" → group + count.

[ ] Look for brackets/nesting → stack.

[ ] Look for "longest substring" → sliding window.

[ ] Look for grouping equivalent strings → signature + hash map.

[ ] Look for dictionary segmentation → DP + hash set.

[ ] Define variables before coding.

[ ] If using DP, define exactly what `dp[i]` means.

[ ] Check edge cases.

[ ] State time complexity.

[ ] State space complexity.

# ============================================================

# 24. EDGE CASE CHECKLIST

# ============================================================

For String OAs, mentally test:

[ ] Empty string

[ ] Single character

[ ] All characters same

[ ] No spaces

[ ] Leading spaces

[ ] Trailing spaces

[ ] Multiple spaces

[ ] Duplicate characters

[ ] No duplicate characters

[ ] All characters unique

[ ] Nested brackets

[ ] Wrong bracket order

[ ] Only opening brackets

[ ] Only closing brackets

[ ] Count greater than 9

[ ] Empty dictionary

[ ] Dictionary contains repeated words

[ ] Entire string is one dictionary word

[ ] String requires multiple dictionary words

[ ] String cannot be segmented

# ============================================================

# 25. FINAL MASTER MEMORY TREE

# ============================================================

```
                     STRING
                        │
    ┌───────────────────┼────────────────────┐
    │                   │                    │
  SIMPLE              STRUCTURE            ADVANCED
    │                   │                    │
    ├── Last Word       ├── Stack            ├── Sliding Window
    │     ↓             │     ↓              │      ↓
    │  Right→Left       │ Parentheses        │ Longest Substring
    │                   │                    │
    ├── Pangram         └── Compression      ├── Anagrams
    │     ↓                    ↓             │      ↓
    │  Array[26]          Read + Write       │ Hash Map + Signature
    │                                           │
    └── Reverse                                └── Word Break
          ↓                                           ↓
     Two Pointers                                DP + Hash Set
```

# ============================================================

# 26. FINAL RECOGNITION RULES

# ============================================================

1. LAST WORD
   → Start from the RIGHT.

2. PANGRAM
   → Think ARRAY[26].

3. REVERSE
   → Think TWO POINTERS.

4. CONSECUTIVE CHARACTERS
   → Think GROUP + COUNT.

5. VALID BRACKETS
   → Think STACK.

6. LONGEST SUBSTRING
   → Think SLIDING WINDOW.

7. ANAGRAMS
   → Think NORMALIZED SIGNATURE.

8. GROUPING
   → Think HASH MAP.

9. DICTIONARY SEGMENTATION
   → Think DP + HASH SET.

10. SUBSTRING
    → CONTIGUOUS.

11. SUBSEQUENCE
    → NOT NECESSARILY CONTIGUOUS.

12. STACK
    → LIFO.

13. SLIDING WINDOW
    → RIGHT EXPANDS, LEFT SHRINKS.

14. TWO POINTERS
    → CONTROL TWO POSITIONS.

15. FREQUENCY ARRAY
    → BEST WHEN CHARACTER SET IS SMALL/FIXED.

16. HASH SET
    → FAST EXISTENCE CHECK.

17. HASH MAP
    → KEY → VALUE / GROUPING.

18. DP
    → DEFINE THE STATE FIRST.

19. WORD BREAK:
    `dp[i]` = first `i` characters can be formed.

20. STRING COMPRESSION:
    CONSECUTIVE frequency ≠ TOTAL frequency.

# ============================================================

# 27. FINAL CONFIDENCE MAP

# ============================================================

If the OA gives you:

"Last word"
↓
RIGHT → LEFT

"Every alphabet letter"
↓
ARRAY[26]

"Reverse"
↓
TWO POINTERS

"Compress repeated characters"
↓
READ + WRITE

"Valid brackets"
↓
STACK

"Longest substring without repeating"
↓
SLIDING WINDOW

"Group anagrams"
↓
SIGNATURE + HASH MAP

"Can form string using dictionary"
↓
DP + HASH SET

# ============================================================

# FINAL ONE-LINE MEMORY

# ============================================================

LAST → RIGHT

COUNT → FREQUENCY

REVERSE → TWO POINTER

CONSECUTIVE → GROUP + COUNT

NESTED → STACK

LONGEST SUBSTRING → SLIDING WINDOW

ANAGRAM → SIGNATURE + HASH MAP

CAN FORM → DP + HASH SET

# ============================================================

# END — STRING MASTER PATTERN NOTEBOOK

# ============================================================

```
```
