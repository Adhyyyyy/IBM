# IBM OA — MASTER PATTERN NOTEBOOK
# SET 9 — GREEDY + INTERVALS


# SOURCE BASIS

The DSA Geetha identifies GREEDY with:

- Interval problems
- Minimum platforms
- Activity selection
- Jump game

Trigger words:

- minimum number of
- maximum activities
- intervals
- schedule

Core thinking:

SORT
   ↓
MAKE LOCALLY BEST CHOICE
   ↓
PROVE YOU NEVER NEED TO UNDO


The source explicitly describes the greedy property as:

LOCAL OPTIMAL
      ↓
GLOBAL OPTIMAL


Important:

Greedy cannot be applied automatically.

You need a reason/proof that the local choice does not destroy
the possibility of the global optimum.


# 109. WHAT IS GREEDY?

GREEDY
│
├── Make a choice
│
├── Choose what looks best NOW
│
├── Commit to that choice
│
└── Never go back


The key question:

"Can I safely make the best local choice?"


If YES:

GREEDY


If NO:

You may need:

DP
Backtracking
Graph algorithm
etc.


# THE MOST IMPORTANT GREEDY DIFFERENCE

DP:

Try/consider different choices
        ↓
Remember results


GREEDY:

Choose one best-looking option
        ↓
Commit
        ↓
Move forward


# GREEDY MENTAL MODEL

PROBLEM
   ↓
SORT / ORGANIZE
   ↓
IDENTIFY WHAT MATTERS
   ↓
MAKE BEST LOCAL CHOICE
   ↓
UPDATE STATE
   ↓
CONTINUE


# 110. GREEDY CHOICE PROPERTY

A greedy solution works when:

making the locally optimal choice
at each step
leads to a globally optimal solution.


Think:

LOCAL BEST
    ↓
Does it ever hurt me later?


If:

NO

    ↓

GREEDY MAY WORK.


# IMPORTANT PROOF QUESTION

Ask:

"Is there ever a reason NOT to make this locally best choice?"


If you can construct a counterexample:

GREEDY
   ↓
FAILS


Then investigate:

DP
or another algorithm.


# 111. GREEDY vs DP

This is one of the most important connections
from Set 7 → Set 9.


DP:

"I need to consider multiple possibilities
because a local choice may hurt later."


GREEDY:

"I can prove that one local choice
is always safe."


# EXAMPLE — COIN CHANGE

Coins:

1, 3, 4

Amount:

6


Greedy:

take 4
 ↓
remaining 2
 ↓
1 + 1

Total:

3 coins


Optimal:

3 + 3

Total:

2 coins


Therefore:

GREEDY FAILS.


This is exactly why arbitrary coin change should not
automatically be treated as greedy.


Use:

DP


# CONNECTION

COIN CHANGE
 ↓
"Minimum"
 ↓
Could look greedy
 ↓
But local choice may fail
 ↓
DP


GREEDY RULE:

Never assume:

"minimum"
=
greedy.


# 112. 0/1 KNAPSACK — GREEDY TRAP

0/1 KNAPSACK

Each item:

TAKE
OR
SKIP


A tempting greedy idea:

"value / weight"
 ↓
take highest ratio first


But:

this does not guarantee the optimal answer
for discrete 0/1 items.


Therefore:

0/1 KNAPSACK
 ↓
DP


This is explicitly listed as a greedy trap
in the DSA reference.


# CORE DECISION

Can I prove:

"Taking this item now
can never hurt the final answer?"


If no:

Don't blindly use greedy.


# 113. INTERVAL PROBLEMS

INTERVAL
=
[start, end]


Example:

[1,4]


means:

starts at 1
ends at 4


Common interval questions:

├── Merge overlapping intervals
├── Select maximum non-overlapping intervals
├── Find minimum platforms
├── Meeting rooms
└── Scheduling


# INTERVAL MASTER IDEA

Most interval problems start with:

SORT


But:

SORT BY WHAT?


This is the critical question.


Different problems require different sorting criteria.


# INTERVAL SORTING MAP

MERGE INTERVALS
        ↓
SORT BY START


ACTIVITY SELECTION
        ↓
SORT BY END


MINIMUM PLATFORMS
        ↓
SORT ARRIVALS
+
SORT DEPARTURES


This distinction is extremely important.


# 114. MERGE INTERVALS

The DSA Geetha lists:

#15 Merge Intervals

Pattern:

SORT + GREEDY MERGE

Trigger words:

overlapping intervals
merge
combine


Optimal approach:

Sort by start time.

Maintain current interval.

If overlap:

extend:

end = max(currentEnd, newEnd)


Complexity:

O(n log n)


The source marks this problem:

CRITICAL


# MERGE INTERVALS — STORY

Input:

[1,3]
[2,6]
[8,10]
[9,12]


Sort by start:

[1,3]
[2,6]
[8,10]
[9,12]


Start with:

current = [1,3]


Next:

[2,6]


Do they overlap?

2 <= 3

YES.


Merge:

[1, max(3,6)]

=

[1,6]


Next:

[8,10]


8 > 6

No overlap.


Store:

[1,6]


Start new:

[8,10]


Next:

[9,12]


9 <= 10

Overlap.


Merge:

[8,12]


Final:

[1,6]
[8,12]


# MERGE INTERVALS — MENTAL STRUCTURE

SORT BY START
      ↓
CURRENT INTERVAL
      ↓
LOOK AT NEXT
      ↓
OVERLAP?
   /       \
 YES        NO
 ↓           ↓
MERGE       STORE CURRENT
 ↓           ↓
MAX END     START NEW
      \     /
       CONTINUE


# HOW TO DETECT OVERLAP

Current:

[start, end]


Next:

[nextStart, nextEnd]


If:

nextStart <= end


then:

OVERLAP


Therefore:

newEnd
=
max(end, nextEnd)


# WHY max?

Suppose:

current:

[1,10]


next:

[2,5]


They overlap.


If you blindly use:

nextEnd = 5


you would shrink the interval:

[1,5]


WRONG.


Correct:

max(10,5)
=
10


Therefore:

[1,10]


This is explicitly identified as a common mistake
in the source.


# MERGE INTERVALS — CORE CODE

```cpp
vector<vector<int>> merge(vector<vector<int>>& intervals)
{
    sort(intervals.begin(), intervals.end());

    vector<vector<int>> ans;

    for(auto interval : intervals)
    {
        if(ans.empty() ||
           interval[0] > ans.back()[1])
        {
            ans.push_back(interval);
        }
        else
        {
            ans.back()[1] =
                max(ans.back()[1], interval[1]);
        }
    }

    return ans;
}

WHY DOES THIS WORK?

After sorting by start:

all future intervals start
at or after the current interval's start.

So we only need to know:

the current merged interval's farthest end.

If nextStart <= currentEnd:

it belongs to the current group.

If:

nextStart > currentEnd:

there is a gap.

Therefore:

start a new interval.

MERGE INTERVALS — COMPLEXITY

SORT:

O(n log n)

SCAN:

O(n)

TOTAL:

O(n log n)

Extra output:

O(n)

EDGE CASES

MERGE INTERVALS

├── [ ] one interval
├── [ ] no overlap
├── [ ] all overlap
├── [ ] nested intervals
├── [ ] duplicate intervals
└── [ ] touching intervals

TOUCHING INTERVALS

Example:

[1,2]
[2,3]

Question:

Are they overlapping?

This depends on the problem's definition.

The source explicitly flags this as an edge case:

"is [1,2],[2,3] overlap?"

Therefore:

READ THE STATEMENT.

Do not blindly assume.

COMMON MERGE MISTAKES

├── [ ] Forgetting to sort
├── [ ] Sorting by wrong field
├── [ ] Using newEnd instead of max
├── [ ] Wrong overlap condition
└── [ ] Mishandling touching intervals

CONNECTION

MERGE INTERVALS
↓
SORT BY START
↓
MAINTAIN CURRENT END
↓
MERGE IF OVERLAP

This pattern is different from:

ACTIVITY SELECTION

because the goal differs.

115. ACTIVITY SELECTION

ACTIVITY SELECTION

Goal:

Select the maximum number
of non-overlapping activities.

Example:

Activity:

[start, end]

You want:

MAXIMUM NUMBER
of compatible activities.

GREEDY CHOICE

Choose the activity
that finishes earliest.

Therefore:

SORT BY END TIME.

WHY EARLIEST END?

Suppose:

Activity A ends at 3.

Activity B ends at 7.

If you choose A:

you free the timeline earlier.

If you choose B:

you block more future time.

Therefore:

EARLIEST FINISH
leaves maximum room
for future activities.

ACTIVITY SELECTION — STORY

Activities:

A = [1,2]
B = [3,4]
C = [0,6]
D = [5,7]
E = [8,9]

Sort by END:

[1,2]
[3,4]
[0,6]
[5,7]
[8,9]

Choose:

[1,2]

Next:

[3,4]

3 >= 2

Choose.

Next:

[0,6]

0 < 4

Skip.

Next:

[5,7]

5 >= 4

Choose.

Next:

[8,9]

8 >= 7

Choose.

Selected:

[1,2]
[3,4]
[5,7]
[8,9]

MENTAL STRUCTURE

SORT BY END
↓
PICK EARLIEST FINISH
↓
UPDATE LAST END
↓
IF NEXT START >= LAST END
↓
PICK
↓
CONTINUE

CORE CODE
int activitySelection(vector<pair<int,int>>& activities)
{
    sort(
        activities.begin(),
        activities.end(),
        [](auto &a, auto &b)
        {
            return a.second < b.second;
        }
    );

    int count = 0;
    int lastEnd = -1;

    for(auto [start, end] : activities)
    {
        if(start >= lastEnd)
        {
            count++;
            lastEnd = end;
        }
    }

    return count;
}
IMPORTANT

The exact initialization of:

lastEnd

depends on the constraints.

If negative start times are possible,
do not blindly use -1.

Safer:

use the appropriate smallest possible value
or initialize from the first activity after sorting.

ACTIVITY SELECTION — CORE REASON

The greedy choice is:

EARLIEST END.

Because:

earlier finish

more remaining room.

CONNECTION

ACTIVITY SELECTION
↓
MAXIMUM ACTIVITIES
↓
SORT BY END

MERGE INTERVALS
↓
MERGE OVERLAPS
↓
SORT BY START

Same data type:

INTERVALS

Different objective:

ACTIVITY SELECTION:
maximize number selected

MERGE:
combine overlapping ranges

Therefore:

SAME INPUT STYLE
≠
SAME GREEDY SORT.

116. MINIMUM PLATFORMS

The DSA Geetha explicitly identifies:

Minimum Platforms

as a greedy pattern.

Problem idea:

Given train arrival and departure times,

find the minimum number of platforms
needed so that no train waits.

KEY IDEA

At any moment:

number of trains present

=
number of platforms needed.

We need to process:

ARRIVALS
+
DEPARTURES

MENTAL MODEL

ARRIVAL
↓
platform needed
↓
count++

DEPARTURE
↓
platform freed
↓
count--

Track:

current platforms

and:

maximum platforms.

TWO SORTED ARRAYS

arrivals:

[900, 940, 950, 1100]

departures:

[910, 1200, 1120, 1130]

Sort both.

Then use:

i = arrival pointer
j = departure pointer

Compare:

arrival[i]
vs
departure[j]

If:

arrival[i] <= departure[j]

A train arrives
before the earliest departure.

Need another platform.

count++

Otherwise:

a departure happens first.

count--

VISUAL

ARRIVAL
↓
need platform
↓
CURRENT++

DEPARTURE
↓
free platform
↓
CURRENT--

MAX(CURRENT)

ANSWER

CORE TEMPLATE
int minPlatforms(vector<int>& arr,
                 vector<int>& dep)
{
    sort(arr.begin(), arr.end());
    sort(dep.begin(), dep.end());

    int i = 0;
    int j = 0;

    int current = 0;
    int maxi = 0;

    while(i < arr.size())
    {
        if(arr[i] <= dep[j])
        {
            current++;
            maxi = max(maxi, current);
            i++;
        }
        else
        {
            current--;
            j++;
        }
    }

    return maxi;
}
IMPORTANT TIE CONDITION

If:

arrival == departure

you must carefully follow
the problem's convention.

The common interpretation for
platform scheduling is:

arrival at the same time as departure
may require another platform,

therefore:

arrival <= departure

means:

ARRIVAL FIRST.

But:

READ THE EXACT QUESTION.

CONNECTION

MINIMUM PLATFORMS
↓
EVENT PROCESSING
↓
ARRIVAL = +1
DEPARTURE = -1
↓
MAXIMUM ACTIVE COUNT

This connects strongly to:

SWEEP LINE

117. SWEEP LINE IDEA

Many interval problems can be viewed as:

EVENTS
│
├── START
│ ↓
│ +1
│
└── END
↓
-1

Sort events by time.

Walk from left to right.

Maintain:

current active intervals.

Maximum active intervals:

MAXIMUM OVERLAP.

This is the deeper connection behind:

Minimum Platforms.

CONNECTION TO MEETING ROOMS

MEETING INTERVALS

[9,10]
[9,12]
[11,13]

At time:

9

two meetings active.

At time:

11

three? depending on exact intervals.

Question:

How many rooms are needed?

Same fundamental idea:

COUNT OVERLAPPING INTERVALS.

Therefore:

MINIMUM PLATFORMS
≈
MINIMUM ROOMS

Both are:

INTERVAL OVERLAP

118. JUMP GAME

The source's Greedy reference says:

Track farthest reachable position.

If:

current <= farthest

keep going.

JUMP GAME

Given:

nums[i]

meaning:

maximum jump length
from position i.

Question:

Can we reach the final index?

Example:

[2,3,1,1,4]

Start:

index 0

maximum jump:

2

Reachable:

0 → 1
0 → 2

From index 1:

3 more positions.

Can reach end.

Answer:

true

KEY VARIABLE

farthest

Meaning:

farthest position reachable
from all positions processed so far.

MENTAL MODEL

current position
↓
nums[i]
↓
i + nums[i]
↓
update farthest

If:

i > farthest

then:

current position
is unreachable.

Therefore:

FALSE.

CORE CODE
bool canJump(vector<int>& nums)
{
    int farthest = 0;

    for(int i = 0; i < nums.size(); i++)
    {
        if(i > farthest)
            return false;

        farthest =
            max(farthest, i + nums[i]);
    }

    return true;
}
JUMP GAME — THE BIG IDEA

Do NOT think:

"Which exact jump should I take?"

Think:

"What is the farthest position
I can reach so far?"

This removes unnecessary branching.

CONNECTION TO BFS

Imagine:

all positions reachable
within the current jump range.

Instead of explicitly creating a BFS queue,

we can track the reachable boundary.

Therefore:

JUMP GAME
↓
RANGE TRACKING
↓
GREEDY

119. JUMP GAME II

The DSA Geetha gives:

Pattern:

Greedy (BFS-like)

Trigger words:

minimum jumps
reach end
maximum jump

Optimal approach:

Track:

current range end

and:

farthest reachable.

When we reach the end of
the current range:

increment jumps.

Complexity:

O(n)

JUMP GAME II — STORY

Example:

[2,3,1,1,4]

At index 0:

current jump range:

0 → 2

Within this range,
find the farthest next reach.

index 1:

1 + 3 = 4

So:

farthest = 4

When we reach the end
of the current range:

we must use another jump.

Answer:

2

THREE VARIABLES

jumps
currentEnd
farthest

Meaning:

jumps

number of jumps already used

currentEnd

furthest position reachable
with current number of jumps

farthest

furthest position reachable
from positions in current range

VISUAL

CURRENT RANGE

[ currentEnd ]

 ↓

explore all positions
inside current range

 ↓

find farthest

 ↓

current range ends

 ↓

JUMP++

 ↓

new range = farthest

CORE CODE
int jump(vector<int>& nums)
{
    int jumps = 0;
    int currentEnd = 0;
    int farthest = 0;

    for(int i = 0; i < nums.size() - 1; i++)
    {
        farthest =
            max(farthest, i + nums[i]);

        if(i == currentEnd)
        {
            jumps++;
            currentEnd = farthest;
        }
    }

    return jumps;
}
CRITICAL TRAP

The source explicitly warns:

Do NOT increment jumps
before updating farthest
within the current range.

Correct order:

UPDATE FARTHEST

then:

if current range ends:

INCREMENT JUMPS.

JUMP GAME vs JUMP GAME II

JUMP GAME

Question:

CAN I reach the end?

Answer:

BOOLEAN

Main variable:

farthest

JUMP GAME II

Question:

MINIMUM number of jumps?

Answer:

COUNT

Variables:

farthest
currentEnd
jumps

CONNECTION

JUMP GAME
↓
REACHABILITY

JUMP GAME II
↓
MINIMUM REACHABLE RANGES

Both:

farthest reach

But:

different objective.

120. INTERVAL SCHEDULING

General interval scheduling:

Goal:

choose compatible intervals.

The key greedy strategy:

sort by earliest finish.

Therefore:

ACTIVITY SELECTION

classic interval scheduling.

INTERVAL SCHEDULING STORY

Intervals:

[1,4]
[2,3]
[3,5]
[5,7]

Sort by end:

[2,3]
[1,4]
[3,5]
[5,7]

Pick:

[2,3]

Then:

[3,5]

Then:

[5,7]

Maximum compatible set.

WHY SORT BY END?

Because:

EARLY FINISH
↓
MORE SPACE
↓
MORE FUTURE OPTIONS

This is the central greedy proof intuition.

121. MERGE vs SELECT

This distinction must become automatic.

MERGE INTERVALS

Goal:

combine overlaps.

Sort:

START TIME.

Operation:

MERGE.

State:

current end.

Answer:

merged intervals.

ACTIVITY SELECTION

Goal:

maximize number of compatible intervals.

Sort:

END TIME.

Operation:

SELECT / SKIP.

State:

last selected end.

Answer:

count.

VISUAL

MERGE

START
↓
OVERLAP?
↓
MERGE

ACTIVITY SELECTION

END
↓
CAN SELECT?
↓
SELECT

122. INTERVAL DECISION TREE

SEE:

[ start, end ]

Ask:

"What does the problem want?"

    ┌───────────────────────────┐
    │                           │
    ↓                           ↓

MERGE OVERLAPS MAX ACTIVITIES
↓ ↓
SORT START SORT END
│ │
↓ ↓
MERGE SELECT

If asks:

MAXIMUM OVERLAP / MINIMUM ROOMS
↓
EVENT SWEEP
↓
ARRIVAL + DEPARTURE

123. GREEDY SORTING CRITERIA

QUESTION TYPE
│
├── Merge overlapping intervals
│ ↓
│ START
│
├── Maximum non-overlapping activities
│ ↓
│ END
│
├── Minimum platforms
│ ↓
│ ARRIVAL + DEPARTURE
│
└── Jump Game
↓
No interval sort
↓
FARTHEST REACH

This is a high-value recognition table.

124. GREEDY PROOF INTUITION

For:

ACTIVITY SELECTION

Choice:

earliest ending activity.

Why safe?

Suppose an optimal solution chooses
some activity that ends later.

Replace it with the activity that ends earlier.

The replacement:

does not reduce available future time.

Therefore:

we can make the greedy choice
without making the solution worse.

This is the exchange-style intuition
behind the greedy choice.

IMPORTANT

You do NOT need to write a formal mathematical proof
in every OA.

But mentally ask:

"If I replace the optimal solution's first choice
with my greedy choice,
does anything become worse?"

If:

NO

greedy is promising.

125. GREEDY FAILURE TEST

Before using greedy:

ASK:

What is my local best choice?

What future opportunity does it preserve?

Could choosing it now prevent a better solution later?

Can I construct a counterexample?

If yes:

Greedy is probably wrong.

EXAMPLE

COIN CHANGE:

local:

largest coin

counterexample:

[1,3,4]
amount 6

largest:

4

remaining:

2

total:

3 coins

better:

3 + 3

Therefore:

greedy fails.

126. GREEDY vs DP — MASTER CONNECTION

GREEDY

Local choice
↓
commit

DP

Local choices
↓
multiple possibilities
↓
store subproblem answers

WHEN TO THINK DP

If:

"Taking this choice now
might affect many future possibilities."

Especially:

├── overlapping subproblems
├── optimization
├── count ways
└── multiple interacting choices

WHEN TO THINK GREEDY

If:

"I can prove this locally best choice
is always safe."

Especially:

├── scheduling
├── intervals
├── reachability/range expansion
└── certain optimization structures

127. GREEDY STORY DECODER

STORY:

"Maximum number of activities"

    ↓

ACTIVITY SELECTION

    ↓

SORT BY END

STORY:

"Merge overlapping intervals"

    ↓

MERGE INTERVALS

    ↓

SORT BY START

STORY:

"Minimum platforms"

    ↓

EVENT SWEEP

    ↓

ARRIVAL / DEPARTURE

STORY:

"Can reach the end"

    ↓

JUMP GAME

    ↓

FARTHEST

STORY:

"Minimum jumps"

    ↓

JUMP GAME II

    ↓

RANGE + FARTHEST

STORY:

"Maximum overlap"

    ↓

SWEEP LINE

128. SET 9 — PATTERN MAP

GREEDY
│
├── INTERVALS
│ │
│ ├── Merge Intervals
│ │ ↓
│ │ Sort START
│ │
│ ├── Activity Selection
│ │ ↓
│ │ Sort END
│ │
│ └── Minimum Platforms
│ ↓
│ Events
│
├── JUMP
│ │
│ ├── Jump Game
│ │ ↓
│ │ Farthest Reach
│ │
│ └── Jump Game II
│ ↓
│ Farthest
│ +
│ Current Range
│
└── GREEDY VALIDATION
│
├── Local choice
├── Future remains feasible
└── No counterexample

129. SET 9 — CONNECTION MAP

MERGE INTERVALS
↓
SORT + SCAN
↓
CURRENT END

ACTIVITY SELECTION
↓
SORT + SCAN
↓
LAST SELECTED END

MINIMUM PLATFORMS
↓
SORT EVENTS
↓
CURRENT ACTIVE COUNT

JUMP GAME
↓
SCAN
↓
FARTHEST REACH

JUMP GAME II
↓
SCAN RANGE
↓
FARTHEST NEXT RANGE

All of them avoid:

EXHAUSTIVE SEARCH.

That is the common greedy theme.

130. SET 9 — COMPLEXITY CHEAT SHEET

MERGE INTERVALS

Sort:

O(n log n)

Scan:

O(n)

Total:

O(n log n)

ACTIVITY SELECTION

Sort:

O(n log n)

Scan:

O(n)

Total:

O(n log n)

MINIMUM PLATFORMS

Sort arrivals:

O(n log n)

Sort departures:

O(n log n)

Two-pointer scan:

O(n)

Total:

O(n log n)

JUMP GAME

O(n)

Space:

O(1)

JUMP GAME II

O(n)

Space:

O(1)

131. EDGE CASES

MERGE INTERVALS

├── [ ] one interval
├── [ ] no overlap
├── [ ] complete overlap
├── [ ] nested intervals
├── [ ] duplicate intervals
└── [ ] touching endpoints

ACTIVITY SELECTION

├── [ ] one activity
├── [ ] all overlap
├── [ ] no overlap
├── [ ] same end times
└── [ ] negative/zero times if allowed

MINIMUM PLATFORMS

├── [ ] one train
├── [ ] all trains overlap
├── [ ] no overlap
├── [ ] same arrival/departure
└── [ ] equal times

JUMP GAME

├── [ ] one element
├── [ ] zero jump
├── [ ] unreachable position
└── [ ] large jump

JUMP GAME II

├── [ ] one element
├── [ ] already at end
├── [ ] direct jump to end
└── [ ] multiple possible ranges

132. COMMON GREEDY TRAPS

├── [ ] Assuming greedy without proof
├── [ ] Sorting by wrong criterion
├── [ ] Using start instead of end
├── [ ] Using end instead of start
├── [ ] Forgetting overlap definition
├── [ ] Ignoring equal endpoints
├── [ ] Confusing Jump Game with Jump Game II
├── [ ] Updating jumps before farthest
├── [ ] Using greedy for arbitrary coin change
└── [ ] Using greedy for 0/1 knapsack

133. MOST IMPORTANT SORTING CONNECTION

SORTING IS NOT THE GREEDY ALGORITHM.

Sorting:

prepares the data
so that the greedy decision
becomes easy.

Example:

Activity Selection:

unsorted
↓
sort by END
↓
earliest-ending activity appears first
↓
greedy selection

Merge Intervals:

unsorted
↓
sort by START
↓
overlapping intervals become adjacent
↓
greedy merge

Therefore:

SORT

ENABLER

GREEDY

DECISION STRATEGY

134. SET 9 — CODE PATTERN SUMMARY
MERGE INTERVALS
sort(intervals.begin(), intervals.end());

for(auto interval : intervals)
{
    if(ans.empty() ||
       interval[0] > ans.back()[1])
    {
        ans.push_back(interval);
    }
    else
    {
        ans.back()[1] =
            max(ans.back()[1], interval[1]);
    }
}

MENTAL:

SORT START
→
COMPARE NEXT START WITH CURRENT END
→
MERGE OR NEW

ACTIVITY SELECTION
sort(
    activities.begin(),
    activities.end(),
    [](auto &a, auto &b)
    {
        return a.second < b.second;
    }
);

for(auto [start, end] : activities)
{
    if(start >= lastEnd)
    {
        count++;
        lastEnd = end;
    }
}

MENTAL:

SORT END
→
EARLIEST FINISH
→
SELECT IF COMPATIBLE

JUMP GAME
int farthest = 0;

for(int i = 0; i < nums.size(); i++)
{
    if(i > farthest)
        return false;

    farthest =
        max(farthest, i + nums[i]);
}

return true;

MENTAL:

CAN I EVEN REACH i?
→
UPDATE FARTHEST

JUMP GAME II
int jumps = 0;
int currentEnd = 0;
int farthest = 0;

for(int i = 0; i < nums.size() - 1; i++)
{
    farthest =
        max(farthest, i + nums[i]);

    if(i == currentEnd)
    {
        jumps++;
        currentEnd = farthest;
    }
}

return jumps;

MENTAL:

EXPLORE CURRENT RANGE
→
FIND FARTHEST
→
RANGE ENDS
→
JUMP
→
NEW RANGE

135. SET 9 — PRIORITY
TIER 1 — MUST MASTER

├── [ ] Merge Intervals
├── [ ] Activity Selection
├── [ ] Jump Game
└── [ ] Jump Game II

These are the core patterns because they teach:

├── Sort + Greedy
├── End-time greedy
├── Farthest-reach greedy
└── Range-expansion greedy

The DSA source specifically marks:

Merge Intervals:
CRITICAL

Jump Game II:
HIGH

TIER 2 — IMPORTANT

├── [ ] Minimum Platforms
├── [ ] Interval Scheduling
└── [ ] Meeting-room style overlap problems

TIER 3 — CONCEPTUAL

├── [ ] Greedy choice property
├── [ ] Exchange intuition
├── [ ] Greedy vs DP
├── [ ] Greedy counterexample test
└── [ ] Sorting criterion recognition

SET 9 — CHECKLIST

SET 9 — GREEDY + INTERVALS

│
├── GREEDY
│ ├── [ ] Understand local vs global optimum
│ ├── [ ] Know when greedy is dangerous
│ ├── [ ] Counterexample test
│ └── [ ] Greedy choice reasoning
│
├── INTERVALS
│ ├── [ ] Merge Intervals
│ ├── [ ] Activity Selection
│ ├── [ ] Interval Scheduling
│ └── [ ] Minimum Platforms
│
├── JUMP
│ ├── [ ] Jump Game
│ └── [ ] Jump Game II
│
└── RECOGNITION
├── [ ] Sort START for merge
├── [ ] Sort END for selection
├── [ ] Events for overlap
└── [ ] Farthest for jump

SET 9 — THE SORTING RULE TO MEMORIZE

MERGE
↓
START

SELECT MAXIMUM ACTIVITIES
↓
END

PLATFORM / ROOM COUNT
↓
ARRIVAL + DEPARTURE EVENTS

JUMP
↓
NO SORT
↓
FARTHEST REACH

SET 9 — THE BIGGEST CONNECTION

INTERVALS

   ┌─────────────────────────┐
   │                         │
   ↓                         ↓

MERGE SELECT
↓ ↓
SORT START SORT END
↓ ↓
OVERLAP COMPATIBILITY

Then:

OVERLAP COUNT
↓
EVENT SWEEP

And:

RANGE REACHABILITY
↓
FARTHEST GREEDY

SET 9 — GREEDY MASTER DECISION TREE

SEE A PROBLEM
↓
Is there an optimization/
selection decision?
↓
Can I make one choice
and never need to undo?
↓
Can I prove the choice is safe?
↓
YES
↓
GREEDY

For intervals:
↓
What is the objective?

MERGE?
↓
SORT START

MAX ACTIVITIES?
↓
SORT END

MAXIMUM OVERLAP?
↓
EVENT SWEEP

For jumps:
↓
Can reach?
↓
FARTHEST

Minimum jumps?
↓
CURRENT RANGE
+
FARTHEST

SET 9 — GREEDY FAILURE MEMORY

DO NOT USE GREEDY JUST BECAUSE
THE QUESTION SAYS:

"minimum"
or
"maximum".

Examples where greedy can fail:

ARBITRARY COIN CHANGE
↓
DP

0/1 KNAPSACK
↓
DP

Therefore:

OPTIMIZATION
≠
AUTOMATIC GREEDY.

SET 9 — FINAL RECOGNITION RULES
GREEDY = make a local choice and commit.
The local choice must be provably safe.
Always ask what criterion makes the greedy choice safe.
Merge Intervals → sort by START.
Activity Selection → sort by END.
Earlier finishing activity leaves more room.
Minimum Platforms → process arrivals and departures as events.
Maximum simultaneous intervals → active-count sweep.
Jump Game → track FARTHEST reachable.
Jump Game II → track CURRENT RANGE + FARTHEST.
In Jump Game II, update farthest before increasing jumps.
Sorting is often the preparation step, not the greedy decision itself.
Same interval input does not mean same sorting criterion.
Greedy must survive the counterexample test.
If a local decision can hurt future choices, investigate DP.
Arbitrary Coin Change → do not assume greedy.
0/1 Knapsack → do not assume greedy.
SET 9 — COMPLETE STORY

GREEDY
│
├── PROVE LOCAL CHOICE SAFE
│
├── INTERVALS
│ │
│ ├── MERGE
│ │ ↓
│ │ START
│ │
│ ├── SELECT
│ │ ↓
│ │ END
│ │
│ └── OVERLAP
│ ↓
│ EVENTS
│
├── JUMP GAME
│ ↓
│ FARTHEST
│
└── JUMP GAME II
↓
CURRENT RANGE
+
FARTHEST

SET 9 — CONNECTION TO PREVIOUS SETS

SET 7 — DP
│
├── Coin Change
│ ↓
│ DP
│
└── 0/1 Knapsack
↓
DP

SET 9 — GREEDY
│
├── Activity Selection
│ ↓
│ Greedy
│
├── Merge Intervals
│ ↓
│ Greedy
│
└── Jump Game
↓
Greedy

Important lesson:

Two problems can both say:

"minimum"

but require completely different patterns.

SET 9 — SPACED REVISION

After solving:

DAY 0
↓
Understand greedy choice

DAY 3
↓
Solve without looking at sorting criterion

DAY 7
↓
Identify pattern from problem statement
in under 30 seconds

DAY 21
↓
Mental walkthrough

For every problem write:

What triggers this pattern?
What is the greedy choice?
Why is it safe?
What sorting criterion is required?
What is the trap?
SET 9 — FINAL MENTAL MAP

"OVERLAPPING INTERVALS"
↓
MERGE
↓
SORT START

"MAXIMUM NON-OVERLAPPING ACTIVITIES"
↓
ACTIVITY SELECTION
↓
SORT END

"MINIMUM PLATFORMS"
↓
EVENT SWEEP
↓
ARRIVAL / DEPARTURE

"CAN REACH END"
↓
JUMP GAME
↓
FARTHEST

"MINIMUM JUMPS"
↓
JUMP GAME II
↓
CURRENT END + FARTHEST

"CAN I PROVE LOCAL BEST IS SAFE?"
↓
GREEDY

"CAN I FIND A COUNTEREXAMPLE?"
↓
IF YES:
RECONSIDER GREEDY
↓
DP / OTHER PATTERN

SET 9 — COMPLETION TARGET

Before moving to Set 10, you should be able to see:

"Merge overlapping intervals"
↓
SORT START

"Maximum number of activities"
↓
SORT END

"Minimum platforms"
↓
SORT EVENTS

"Can reach end"
↓
FARTHEST

"Minimum jumps"
↓
RANGE + FARTHEST

And most importantly:

"Why is this greedy choice safe?"

You should be able to answer that,
not merely memorize the code.
