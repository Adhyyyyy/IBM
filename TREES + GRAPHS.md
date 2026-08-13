# IBM OA — MASTER PATTERN NOTEBOOK
# SET 6 — TREES + GRAPHS

# SOURCE BASIS

The IBM PYQ question bank lists these Trees & Graphs problems:

- Binary tree inorder traversal
- Maximum depth of binary tree
- Validate binary search tree
- Lowest common ancestor
- Level order traversal
- Binary tree from preorder/inorder
- Number of islands
- Course schedule (topological sort)
- Clone graph
- Word ladder problem
- Graph valid tree
- Alien dictionary :contentReference[oaicite:1]{index=1}

The DSA Geetha identifies the core Graph concepts as:

- BFS
- DFS
- Cycle detection
- Topological sort
- Union-Find

It gives these pattern triggers:

- Count regions/components → DFS/BFS + visited
- Shortest path, unweighted → BFS
- Shortest path, weighted → Dijkstra
- Dependencies/ordering → Topological sort
- Connected components → Union-Find :contentReference[oaicite:2]{index=2}

Its memory mapping is:

BFS = SHORTEST PATH
DFS = CONNECTED / EXISTS
TOPO = DEPENDENCIES
UNION-FIND = DYNAMIC CONNECTIVITY :contentReference[oaicite:3]{index=3}

The Geetha specifically recommends:

Number of Islands
        ↓
Course Schedule
        ↓
Dijkstra for weighted shortest path :contentReference[oaicite:4]{index=4}


# SET 6 — BIG PICTURE

SET 6
│
├── TREES
│      │
│      ├── Binary Tree
│      ├── DFS
│      ├── Recursion
│      ├── Inorder
│      ├── Preorder
│      ├── Postorder
│      ├── BFS
│      ├── BST
│      └── LCA
│
└── GRAPHS
       │
       ├── Representation
       ├── DFS
       ├── BFS
       ├── Visited
       ├── Connected Components
       ├── Cycle Detection
       ├── Topological Sort
       ├── Union-Find
       └── Shortest Path


# THE BIG TRANSITION

LINKED LIST
│
└── One node
    points to next

        ↓

TREE
│
└── One node
    can point to multiple children

        ↓

GRAPH
│
└── Any node
    can connect to many nodes


The key progression is:

LINKED LIST
    ↓
ONE-DIRECTION CONNECTION

TREE
    ↓
HIERARCHICAL CONNECTION

GRAPH
    ↓
ARBITRARY CONNECTION


# 67. TREE NODE

Before traversal, understand the basic structure.

struct TreeNode
{
    int val;
    TreeNode* left;
    TreeNode* right;

    TreeNode(int x)
    {
        val = x;
        left = nullptr;
        right = nullptr;
    }
};


VISUAL:

             10
            /  \
           5    15
          / \
         3   7


TREE NODE
│
├── value
│
├── left
│
└── right


Unlike a linked list:

Linked List:

node
│
└── next


Tree:

node
│
├── left
└── right


# TREE TERMINOLOGY

             10
            /  \
           5    15
          / \
         3   7

10
↓
ROOT


5, 15
↓
CHILDREN


3, 7
↓
LEAF NODES


10 → 5 → 3
↓
PATH


The tree has:

ROOT
CHILDREN
LEAVES
SUBTREES


# TREE CORE MENTAL MODEL

TREE
│
├── Current node
│      ↓
│   process it
│
├── Left subtree
│      ↓
│   recurse
│
└── Right subtree
       ↓
    recurse


This gives the fundamental DFS structure:

solve(root)
│
├── solve(root->left)
└── solve(root->right)


# 68. BINARY TREE INORDER TRAVERSAL

## SOURCE CONNECTION

Binary tree inorder traversal is explicitly listed in the IBM Trees & Graphs question bank. :contentReference[oaicite:5]{index=5}

---

INORDER
│
├── ORDER
│
│      LEFT
│       ↓
│      ROOT
│       ↓
│      RIGHT
│
└── MEMORY

L → ROOT → R


Example:

             10
            /  \
           5    15
          / \
         3   7


INORDER:

3 5 7 10 15


# MENTAL MODEL

At every node:

1. Go left
2. Process current
3. Go right


# RECURSIVE TEMPLATE

void inorder(TreeNode* root)
{
    if(root == nullptr)
        return;

    inorder(root->left);

    cout << root->val;

    inorder(root->right);
}


# CONNECTION

TREE
 ↓
DFS
 ↓
RECURSION


INORDER
 ↓
LEFT → ROOT → RIGHT


# IMPORTANT BST CONNECTION

For a BST:

INORDER
    ↓
SORTED ORDER


Example:

             8
            / \
           3   10
          / \
         1   6


Inorder:

1 3 6 8 10


Therefore:

BST
 ↓
INORDER
 ↓
SORTED


This connection becomes extremely important for:

Validate BST
Kth Smallest in BST


# 69. MAXIMUM DEPTH OF BINARY TREE

## SOURCE CONNECTION

Explicitly listed in the IBM question bank. :contentReference[oaicite:6]{index=6}

---

MAX DEPTH
│
├── STORY
│      └── Find longest root-to-leaf path
│
├── CORE QUESTION
│      │
│      └── How deep is
│          the current subtree?
│
├── RECURSION
│
│      leftDepth
│      rightDepth
│
├── ANSWER
│
│      1 + max(
│          leftDepth,
│          rightDepth
│        )
│
└── BASE CASE

root == nullptr
      ↓
depth = 0


# MENTAL MODEL

             10
            /  \
           5    15
          /
         3


Depth:

10
 ↓
5
 ↓
3


= 3


# CORE TEMPLATE

int maxDepth(TreeNode* root)
{
    if(root == nullptr)
        return 0;

    int left = maxDepth(root->left);
    int right = maxDepth(root->right);

    return 1 + max(left, right);
}


# CONNECTION

MAX DEPTH
    ↓
RECURSION
    ↓
SOLVE LEFT
    +
SOLVE RIGHT
    ↓
COMBINE


This is the basic tree-recursion pattern.

Remember:

TREE PROBLEM
    ↓
ASK:
"What does my recursive function return for a subtree?"


# 70. VALIDATE BINARY SEARCH TREE

## SOURCE CONNECTION

Explicitly listed in the IBM question bank. :contentReference[oaicite:7]{index=7}

---

BST
│
├── LEFT SUBTREE
│      ↓
│    values < node
│
├── NODE
│
└── RIGHT SUBTREE
       ↓
     values > node


Example:

             8
            / \
           3   10
          / \
         1   6


Valid BST.


# IMPORTANT TRAP

Do NOT only compare:

root->left < root
root->right > root


Why?

Consider:

             8
            / \
           3   10
          / \
         1   9


9 is:

< 8

but it is inside the LEFT subtree.

Therefore invalid.


The rule is:

EVERY NODE
inside left subtree
must be < root.

EVERY NODE
inside right subtree
must be > root.


# PATTERN

VALIDATE BST
│
├── Current node
│
├── Allowed range
│
│      min < node < max
│
├── LEFT
│      ↓
│   min → node
│
└── RIGHT
       ↓
    node → max


# MENTAL MODEL

At root:

8

Allowed:

(-∞, +∞)


Move left to 3:

allowed:

(-∞, 8)


Move right from 3 to 6:

allowed:

(3, 8)


Therefore:

The valid range travels down the tree.


# CORE TEMPLATE

bool validate(TreeNode* root,
              long long low,
              long long high)
{
    if(root == nullptr)
        return true;

    if(root->val <= low ||
       root->val >= high)
        return false;

    return validate(root->left,
                    low,
                    root->val)
        &&
           validate(root->right,
                    root->val,
                    high);
}


# CONNECTION

BST
 ↓
ORDERING CONSTRAINT
 ↓
PASS RANGE DOWN


Alternative:

BST
 ↓
INORDER
 ↓
MUST BE STRICTLY SORTED


Both are important mental approaches.


# 71. LOWEST COMMON ANCESTOR

## SOURCE CONNECTION

Lowest Common Ancestor is explicitly listed in the IBM Trees & Graphs question bank. :contentReference[oaicite:8]{index=8}

---

LCA
│
├── INPUT
│      │
│      ├── node p
│      └── node q
│
├── OUTPUT
│      │
│      └── Lowest node that
│          is ancestor of both
│
└── IMPORTANT
       Exact approach depends on
       whether it is a BST or
       general binary tree.


# BST VERSION

If:

p < root
AND
q < root

both are left.

Move left.


If:

p > root
AND
q > root

both are right.

Move right.


Otherwise:

root is LCA.


# VISUAL

             8
            / \
           3   10
          / \
         1   6
            / \
           4   7


LCA(4,7)

Both lie inside:

6's subtree.

Therefore:

6


# MENTAL MODEL

BST LCA
│
├── Both smaller
│      ↓
│    LEFT
│
├── Both larger
│      ↓
│    RIGHT
│
└── Split
       ↓
     CURRENT NODE
     = LCA


# CONNECTION

BST property
 ↓
direction becomes obvious


This is much easier than general binary-tree LCA.


# GENERAL BINARY TREE LCA

For a general binary tree:

No ordering property exists.

Therefore:

Need to search both subtrees.


Mental structure:

LCA(root,p,q)
│
├── root == null
│      ↓
│    null
│
├── root == p/q
│      ↓
│    root
│
├── search left
│
├── search right
│
└── if both return non-null
       ↓
     root is LCA


# IMPORTANT

Do not confuse:

LCA of BST
with
LCA of arbitrary binary tree.


The IBM source names LCA but does not specify which exact variant. Therefore both conceptual variants are worth knowing, but we should not claim one specific variant was the IBM question. :contentReference[oaicite:9]{index=9}


# 72. LEVEL ORDER TRAVERSAL

## SOURCE CONNECTION

Explicitly listed in the IBM question bank. :contentReference[oaicite:10]{index=10}

---

LEVEL ORDER
│
├── STORY
│      └── Visit tree level by level
│
├── PATTERN
│      └── BFS
│
├── DATA STRUCTURE
│      └── QUEUE
│
├── PROCESS
│
│      root
│       ↓
│      queue
│       ↓
│      process front
│       ↓
│      push children
│
└── RESULT

Example:

             1
            / \
           2   3
          / \
         4   5


Output:

1
2 3
4 5


# MENTAL MODEL

TREE
 ↓
RIPPLE


Start at:

1

Then:

2 3

Then:

4 5


Exactly like a wave spreading outward.


# CORE TEMPLATE

queue<TreeNode*> q;

q.push(root);

while(!q.empty())
{
    TreeNode* curr = q.front();
    q.pop();

    // process curr

    if(curr->left)
        q.push(curr->left);

    if(curr->right)
        q.push(curr->right);
}


# LEVEL-BY-LEVEL VARIANT

If the question requires each level separately:

while(!q.empty())
{
    int size = q.size();

    for(int i = 0; i < size; i++)
    {
        TreeNode* curr = q.front();
        q.pop();

        // process current level

        if(curr->left)
            q.push(curr->left);

        if(curr->right)
            q.push(curr->right);
    }
}


# CONNECTION

TREE LEVEL ORDER
 ↓
BFS
 ↓
QUEUE


GRAPH SHORTEST PATH
 ↓
BFS
 ↓
QUEUE


Same fundamental pattern.


# 73. BINARY TREE FROM PREORDER + INORDER

## SOURCE CONNECTION

Explicitly listed in the IBM question bank. :contentReference[oaicite:11]{index=11}

---

CONSTRUCT TREE
│
├── INPUT
│      ├── preorder
│      └── inorder
│
├── PREORDER
│      │
│      └── ROOT comes first
│
├── INORDER
│      │
│      ├── LEFT
│      ├── ROOT
│      └── RIGHT
│
├── KEY
│      │
│      └── Preorder tells us
│          the root.
│
├── THEN
│      │
│      └── Find root in inorder.
│
├── LEFT SIDE
│      ↓
│   left subtree
│
└── RIGHT SIDE
       ↓
    right subtree


# EXAMPLE

Preorder:

[3, 9, 20, 15, 7]


Inorder:

[9, 3, 15, 20, 7]


Preorder first:

3

Therefore:

ROOT = 3


In inorder:

9 | 3 | 15 20 7

Therefore:

LEFT SUBTREE:

9


RIGHT SUBTREE:

15 20 7


Now recursively construct each side.


# MENTAL MODEL

PREORDER
 ↓
"WHO IS ROOT?"


INORDER
 ↓
"WHAT IS LEFT AND RIGHT?"


Together:

PREORDER
+
INORDER
=
TREE


# OPTIMIZATION

Use:

value → inorder index

HashMap


Then finding the root position becomes O(1).


# CONNECTION

TREE TRAVERSALS
│
├── PREORDER
│      ↓
│    ROOT first
│
├── INORDER
│      ↓
│    LEFT ROOT RIGHT
│
└── POSTORDER
       ↓
     ROOT last


Important:

Traversal problems are often about understanding what information each traversal gives you.


# 74. NUMBER OF ISLANDS

## SOURCE CONNECTION

Explicitly listed in the IBM question bank. :contentReference[oaicite:12]{index=12}

The DSA Geetha specifically recommends Number of Islands as the entry point for Graphs and says to solve it until you can write it in 5 minutes. :contentReference[oaicite:13]{index=13}

---

NUMBER OF ISLANDS
│
├── INPUT
│      └── GRID
│
├── LAND
│      └── '1'
│
├── WATER
│      └── '0'
│
├── ISLAND
│      └── connected land cells
│
├── CORE PATTERN
│      └── DFS / BFS
│
├── VISITED
│      └── essential
│
└── COUNT
       │
       └── Every time we discover
           a new unvisited land cell,
           start traversal and count +1.


# VISUAL

1 1 0 0
1 0 0 1
0 0 1 1


Start:

1 1
1

This is one island.

Later:

1
1

another island.


# MENTAL MODEL

GRID
 ↓
Every cell is a node.


Adjacent land cells
 ↓
Edges


Therefore:

GRID
 ↓
GRAPH


This is the key transition.


# CORE PROCESS

for every cell:

if cell is land
AND
not visited:

    count++

    DFS/BFS from cell

    mark all connected land


# DFS MENTAL MODEL

DFS(row,col)
│
├── out of bounds?
│      ↓
│    return
│
├── water?
│      ↓
│    return
│
├── already visited?
│      ↓
│    return
│
├── mark visited
│
└── visit 4 directions


Directions:

UP
DOWN
LEFT
RIGHT


# IMPORTANT

Without visited marking:

DFS may repeatedly revisit cells.

The Geetha explicitly identifies forgetting `visited` as a common graph-interview trap. :contentReference[oaicite:14]{index=14}


# CONNECTION

GRID
 ↓
GRAPH


NUMBER OF ISLANDS
 ↓
CONNECTED COMPONENTS


Therefore:

COUNT COMPONENTS
 ↓
DFS/BFS + VISITED


# 75. GRAPH REPRESENTATION

Before Course Schedule and Clone Graph, understand:

ADJACENCY LIST.


Suppose:

0 — 1
|   |
2 — 3


Adjacency list:

0 → 1,2
1 → 0,3
2 → 0,3
3 → 1,2


# C++ STRUCTURE

vector<vector<int>> adj(n);


For edge:

u → v

add:

adj[u].push_back(v);


For an undirected edge:

u — v

add both:

adj[u].push_back(v);
adj[v].push_back(u);


# MENTAL MODEL

GRAPH
 ↓
WHO IS CONNECTED TO WHOM?


ADJACENCY LIST
 ↓
For every node,
store its neighbors.


# IMPORTANT

The Geetha specifically recommends:

Build adjacency list first.

Then check:

1. Directed or undirected?
2. Weighted or unweighted?

Then choose traversal/algorithm. :contentReference[oaicite:15]{index=15}


# 76. GRAPH DFS

DFS
│
├── Start node
│
├── Mark visited
│
├── Explore neighbor
│
├── Continue deeply
│
└── Backtrack


# VISUAL

      1
     / \
    2   3
   /
  4


DFS from 1:

1
 ↓
2
 ↓
4
 ↓
back
 ↓
3


# CORE TEMPLATE

void dfs(int node,
         vector<vector<int>>& adj,
         vector<int>& visited)
{
    visited[node] = 1;

    for(int next : adj[node])
    {
        if(!visited[next])
        {
            dfs(next, adj, visited);
        }
    }
}


# CONNECTION

TREE DFS
 ↓
recursive left/right


GRAPH DFS
 ↓
recursive neighbors


Difference:

TREE
usually has structured parent-child relationships.

GRAPH
may contain cycles and arbitrary connections.

Therefore:

GRAPH
requires
VISITED.


# 77. GRAPH BFS

BFS
│
├── Queue
├── Start node
├── Mark visited
├── Push neighbors
└── Process level by level


# VISUAL

       1
      / \
     2   3
    / \
   4   5


BFS:

1
↓
2 3
↓
4 5


# CORE TEMPLATE

queue<int> q;

q.push(start);
visited[start] = true;

while(!q.empty())
{
    int node = q.front();
    q.pop();

    for(int next : adj[node])
    {
        if(!visited[next])
        {
            visited[next] = true;
            q.push(next);
        }
    }
}


# IMPORTANT RULE

For unweighted shortest path:

BFS.


The Geetha explicitly states:

Shortest path unweighted
        ↓
BFS. :contentReference[oaicite:16]{index=16}


# DFS vs BFS

DFS
│
├── recursion / stack
├── goes deep
├── connectivity
└── existence/search


BFS
│
├── queue
├── spreads level by level
└── shortest path in unweighted graph


# MEMORY TRICK

DFS
=
GO DEEP


BFS
=
SPREAD


# 78. COURSE SCHEDULE

## SOURCE CONNECTION

Course Schedule (topological sort) is explicitly listed in the IBM question bank. :contentReference[oaicite:17]{index=17}

The Geetha identifies dependencies/ordering as a topological-sort trigger and says Course Schedule introduces cycle detection. :contentReference[oaicite:18]{index=18}

---

COURSE SCHEDULE
│
├── STORY
│      └── Courses have prerequisites
│
├── EXAMPLE
│
│      To take:
│      B
│
│      first need:
│      A
│
│      A → B
│
├── GRAPH
│      └── DIRECTED
│
├── QUESTION
│      │
│      └── Is there a valid ordering?
│
├── KEY ISSUE
│      │
│      └── DIRECTED CYCLE
│
└── PATTERN
       TOPOLOGICAL SORT


# CYCLE EXAMPLE

A → B
↑   ↓
└── C


A requires C

C requires B

B requires A


Impossible.

Therefore:

cycle exists
 ↓
cannot finish all courses.


# TOPOLOGICAL ORDER

A → B → C


A must come before B.

B must come before C.


Therefore:

A B C


# KAHN'S ALGORITHM

TOPO SORT
│
├── Calculate indegree
│
├── Find nodes with
│   indegree = 0
│
├── Push them into queue
│
├── Remove/process node
│
├── Decrease neighbors' indegree
│
├── New zero-indegree nodes
│   enter queue
│
└── Count processed nodes


# MENTAL MODEL

INDEGREE
=
How many prerequisites
are still blocking this node?


If:

indegree = 0

nothing is blocking it.

Therefore:

READY TO TAKE.


# COURSE SCHEDULE CONNECTION

COURSE
 ↓
DEPENDENCY
 ↓
DIRECTED GRAPH
 ↓
TOPOLOGICAL SORT
 ↓
CYCLE DETECTION


# IMPORTANT CYCLE RULE

If:

processed nodes < total nodes

then:

cycle exists.


Therefore:

cannot produce valid ordering.


# 79. CLONE GRAPH

## SOURCE CONNECTION

Clone Graph is explicitly listed in the IBM question bank. :contentReference[oaicite:19]{index=19}

---

CLONE GRAPH
│
├── STORY
│      └── Create deep copy
│          of graph
│
├── PROBLEM
│      │
│      └── Graph may contain
│          cycles
│
├── THEREFORE
│      │
│      └── Cannot blindly recurse
│
├── KEY DATA STRUCTURE
│      └── HASHMAP
│
├── MAPPING
│
│      original node
│             ↓
│      cloned node
│
├── PROCESS
│      │
│      ├── If already cloned
│      │      ↓
│      │    return clone
│      │
│      ├── Create clone
│      │
│      ├── Store mapping
│      │
│      └── Clone neighbors
│
└── PATTERN
       GRAPH DFS/BFS
       +
       HASHMAP


# CONNECTION TO SET 3

Copy Random Pointer:

original → copy


Clone Graph:

original → copy


Same fundamental idea:

OBJECT MAPPING.


# WHY MAP BEFORE NEIGHBORS?

Suppose:

A ↔ B


Clone A.

Create:

A'


Store:

A → A'


Then clone B.

B' points to A'.

If A is encountered again:

map[A]

already exists.

Therefore:

return A'.


This prevents infinite recursion.


# 80. GRAPH VALID TREE

## SOURCE CONNECTION

Graph Valid Tree is explicitly listed in the IBM question bank. :contentReference[oaicite:20]{index=20}

---

GRAPH VALID TREE
│
├── A TREE MUST BE
│      │
│      ├── CONNECTED
│      └── ACYCLIC
│
├── THEREFORE
│      │
│      ├── no cycle
│      └── all nodes reachable
│
├── APPROACH
│      │
│      ├── DFS/BFS
│      └── cycle detection
│
└── ALTERNATIVE
       UNION-FIND


# IMPORTANT PROPERTY

For n nodes:

A tree has exactly:

n - 1 edges.


This is a useful necessary condition.

But depending on the exact problem, still verify connectivity/cycle conditions appropriately.


# MENTAL MODEL

VALID TREE
│
├── Connected?
│      │
│      └── YES
│
└── Cycle?
       │
       └── NO


Both required.


# CONNECTION

NUMBER OF ISLANDS
 ↓
CONNECTED COMPONENTS


GRAPH VALID TREE
 ↓
CONNECTED
+
NO CYCLE


# 81. WORD LADDER

## SOURCE CONNECTION

Word Ladder is explicitly listed in the IBM Trees & Graphs question bank. :contentReference[oaicite:21]{index=21}

---

WORD LADDER
│
├── STORY
│      └── Transform one word
│          into another
│
├── ONE MOVE
│      │
│      └── Change one character
│
├── GRAPH MODEL
│      │
│      ├── Each word = node
│      └── One-character transformation
│          = edge
│
├── QUESTION
│      └── Shortest transformation
│          sequence?
│
└── PATTERN
       BFS


# WHY BFS?

Each transformation:

cost = 1


Therefore:

unweighted graph.


Shortest path
 ↓
BFS.


# MENTAL MODEL

hit

↓

hot

↓

dot

↓

dog

↓

cog


Each word:

NODE


Each valid transformation:

EDGE


Therefore:

WORD PROBLEM
 ↓
GRAPH PROBLEM


# CONNECTION

NUMBER OF ISLANDS
 ↓
GRID → GRAPH


WORD LADDER
 ↓
WORDS → GRAPH


Same transformation:

REAL-WORLD OBJECTS
 ↓
NODES

RELATIONSHIP
 ↓
EDGE


# 82. ALIEN DICTIONARY

## SOURCE CONNECTION

Alien Dictionary is explicitly listed in the IBM Trees & Graphs question bank. :contentReference[oaicite:22]{index=22}

---

ALIEN DICTIONARY
│
├── STORY
│      └── Words are sorted according
│          to an unknown alphabet
│
├── GIVEN
│      └── Ordered dictionary
│
├── OBSERVATION
│      │
│      └── Compare adjacent words
│
├── FIRST DIFFERENT CHARACTER
│      │
│      └── gives ordering relation
│
├── EXAMPLE
│
│      "abc"
│      "abd"
│
│      first difference:
│
│      c < d
│
│      therefore:
│
│      c → d
│
├── GRAPH
│      └── directed
│
├── QUESTION
│      └── Find valid character order
│
└── PATTERN
       TOPOLOGICAL SORT


# MENTAL MODEL

WORD ORDER
 ↓
DEPENDENCY RELATION
 ↓
DIRECTED GRAPH
 ↓
TOPOLOGICAL SORT


# CONNECTION

COURSE SCHEDULE
 ↓
prerequisite dependency


ALIEN DICTIONARY
 ↓
character dependency


Both:

DEPENDENCIES
 ↓
TOPOLOGICAL SORT


# IMPORTANT

If a cycle appears:

no valid ordering.


Therefore:

cycle detection remains important.


# SET 6 — MASTER TREE MAP

TREE
│
├── TRAVERSAL
│      │
│      ├── PREORDER
│      │      ↓
│      │    ROOT LEFT RIGHT
│      │
│      ├── INORDER
│      │      ↓
│      │    LEFT ROOT RIGHT
│      │
│      └── POSTORDER
│             ↓
│           LEFT RIGHT ROOT
│
├── DFS
│      ↓
│    RECURSION
│
├── BFS
│      ↓
│    QUEUE
│
├── BST
│      │
│      ├── ordering
│      ├── inorder = sorted
│      └── range validation
│
├── DEPTH
│      ↓
│    max(left,right)+1
│
├── LCA
│      ↓
│    common ancestor
│
└── CONSTRUCTION
       ↓
    preorder + inorder


# SET 6 — MASTER GRAPH MAP

GRAPH
│
├── REPRESENTATION
│      ↓
│   adjacency list
│
├── TRAVERSAL
│      │
│      ├── DFS
│      │      ↓
│      │    recursion / stack
│      │
│      └── BFS
│             ↓
│           queue
│
├── VISITED
│      ↓
│   prevent revisiting
│
├── CONNECTIVITY
│      ↓
│   DFS / BFS
│
├── SHORTEST UNWEIGHTED
│      ↓
│   BFS
│
├── CYCLE
│      ↓
│   DFS / BFS / indegree
│
├── DEPENDENCIES
│      ↓
│   TOPOLOGICAL SORT
│
├── DYNAMIC CONNECTIVITY
│      ↓
│   UNION-FIND
│
└── WEIGHTED SHORTEST PATH
       ↓
    DIJKSTRA


# SET 6 — DFS vs BFS

DFS
│
├── Goes deep
├── Recursion / stack
├── Connectivity
├── Existence
├── Explore component
└── Cycle detection


BFS
│
├── Queue
├── Level by level
├── Shortest unweighted path
└── Minimum number of edges


# MEMORY TRICK

DFS
=
CONNECTED / EXISTS


BFS
=
SHORTEST PATH


TOPO
=
DEPENDENCIES


UNION-FIND
=
DYNAMIC CONNECTIVITY


This exact mapping is given in the DSA Geetha. :contentReference[oaicite:23]{index=23}


# SET 6 — VISITED ARRAY

GRAPH
│
├── Node may have
│   multiple neighbors
│
├── Graph may contain
│   cycles
│
└── Therefore:
       visited


Example:

A → B
↑   ↓
└── C


Without visited:

A
 ↓
B
 ↓
C
 ↓
A
 ↓
B
 ↓
C
...


Infinite traversal.


Therefore:

visited[node] = true

before exploring its neighbors.


# IMPORTANT TRAP

Marking visited too late can also cause duplicate processing.

For BFS:

Usually mark visited when adding the node to the queue.


For DFS:

Mark visited when entering the node.


# SET 6 — DIRECTED vs UNDIRECTED

UNDIRECTED

A — B

means:

A connected to B

AND

B connected to A.


Adjacency list:

A → B
B → A


DIRECTED

A → B


means:

A can go to B.

It does NOT automatically mean:

B → A.


# WHY THIS MATTERS

CYCLE DETECTION
│
├── Undirected
│      ↓
│    parent tracking
│
└── Directed
       ↓
    recursion state /
    indegree


Do not blindly use the same cycle logic for both.


# SET 6 — TOPOLOGICAL SORT

TOPOLOGICAL SORT
│
├── Only meaningful for
│   directed acyclic graph
│
├── DAG
│      ↓
│   Directed Acyclic Graph
│
├── Kahn
│      ↓
│   BFS + indegree
│
└── DFS VERSION
       ↓
    recursion + state/stack


# KAHN'S ALGORITHM

GRAPH
 ↓
INDEGREE
 ↓
ZERO INDEGREE
 ↓
QUEUE
 ↓
PROCESS
 ↓
REDUCE NEIGHBOR INDEGREE
 ↓
NEW ZERO INDEGREE
 ↓
QUEUE


# CYCLE DETECTION USING KAHN

If:

processed != n

then:

cycle exists.


Therefore:

NO COMPLETE TOPOLOGICAL ORDER.


# CONNECTION

COURSE SCHEDULE
 ↓
TOPOLOGICAL SORT


ALIEN DICTIONARY
 ↓
TOPOLOGICAL SORT


Same pattern.


# SET 6 — UNION-FIND

The DSA Geetha identifies Union-Find as the pattern for dynamic connectivity. :contentReference[oaicite:24]{index=24}

UNION-FIND
│
├── Each node belongs to
│   a component
│
├── FIND
│      ↓
│   identify component
│
├── UNION
│      ↓
│   merge components
│
└── USEFUL FOR
       │
       ├── connectivity
       ├── cycle detection
       └── dynamic connectivity


# GRAPH VALID TREE CONNECTION

Graph Valid Tree
      ↓
Need:
connected
+
acyclic


Union-Find can help detect whether adding an edge joins nodes already in the same component.

If yes:

cycle.


If no:

union them.


# SET 6 — GRID AS GRAPH

This is extremely important.

GRID

[ ][ ][ ]
[ ][ ][ ]
[ ][ ][ ]


Each cell:

NODE


Neighboring cells:

EDGES


Therefore:

GRID
 ↓
GRAPH


Examples:

NUMBER OF ISLANDS
 ↓
DFS/BFS


FLOOD FILL
 ↓
DFS/BFS


ROTTING ORANGES
 ↓
BFS


WORD LADDER
 ↓
WORDS become nodes


# SET 6 — PATTERN CONNECTIONS

## CONNECTION 1

TREE DFS

node
 ↓
left
 ↓
right


GRAPH DFS

node
 ↓
neighbors


Same concept:

DFS explores recursively.


---

## CONNECTION 2

TREE BFS

queue
 ↓
levels


GRAPH BFS

queue
 ↓
distance levels


Same data structure:

QUEUE.


---

## CONNECTION 3

NUMBER OF ISLANDS

GRID
 ↓
DFS/BFS
+
visited


CONNECTED COMPONENTS

GRAPH
 ↓
DFS/BFS
+
visited


Same fundamental problem.


---

## CONNECTION 4

COURSE SCHEDULE

prerequisites
 ↓
directed edges
 ↓
topological sort


ALIEN DICTIONARY

character order
 ↓
directed edges
 ↓
topological sort


Same pattern.


---

## CONNECTION 5

CLONE GRAPH

original node
 ↓
copy node


COPY RANDOM POINTER

original node
 ↓
copy node


Same:

HASHMAP MAPPING.


# SET 6 — STORY DECODING CHEAT SHEET

STORY
│
├── "Visit tree in left-root-right"
│      ↓
│    INORDER
│
├── "Maximum depth"
│      ↓
│    RECURSION
│
├── "Is this a BST?"
│      ↓
│    RANGE / INORDER
│
├── "Lowest common ancestor"
│      ↓
│    TREE RELATIONSHIP
│
├── "Level by level"
│      ↓
│    BFS + QUEUE
│
├── "Build tree from traversals"
│      ↓
│    PREORDER + INORDER
│
├── "Number of islands"
│      ↓
│    GRID + DFS/BFS + VISITED
│
├── "Reachable?"
│      ↓
│    DFS/BFS
│
├── "Shortest unweighted path"
│      ↓
│    BFS
│
├── "Course prerequisites"
│      ↓
│    TOPOLOGICAL SORT
│
├── "Clone graph"
│      ↓
│    DFS/BFS + HASHMAP
│
├── "Word transformation shortest"
│      ↓
│    BFS
│
├── "Valid tree"
│      ↓
│    CONNECTIVITY + CYCLE
│
└── "Unknown alphabet order"
       ↓
    TOPOLOGICAL SORT


# SET 6 — PRIORITY

## TIER 1 — MUST MASTER

The Geetha specifically recommends Number of Islands as the graph entry point and Course Schedule immediately after it. :contentReference[oaicite:25]{index=25}

├── [ ] 67. Tree Node
├── [ ] 68. Inorder Traversal
├── [ ] 69. Maximum Depth
├── [ ] 70. Validate BST
├── [ ] 71. Level Order Traversal
├── [ ] 72. Number of Islands
├── [ ] 73. Graph DFS
├── [ ] 74. Graph BFS
└── [ ] 75. Course Schedule


# TIER 2 — HIGH VALUE

├── [ ] 76. Lowest Common Ancestor
├── [ ] 77. Binary Tree from Preorder + Inorder
├── [ ] 78. Clone Graph
├── [ ] 79. Graph Valid Tree
└── [ ] 80. Word Ladder


# TIER 3 — ADVANCED

├── [ ] 81. Alien Dictionary
└── [ ] 82. Union-Find


# IMPORTANT SOURCE DISTINCTION

The IBM PYQ resource names the above questions but does not assign frequencies to each individual Trees & Graphs question in the retrieved source.

Therefore:

TIER 1 / 2 / 3 above is our preparation ordering based on prerequisite relationships and the Geetha's recommended progression, NOT a claim that IBM asks Tier 1 more frequently than Tier 2.

The source itself supports the list of IBM question types. :contentReference[oaicite:26]{index=26}


# SET 6 — CHECKLIST

SET 6 — TREES + GRAPHS
│
├── TREE FUNDAMENTALS
│      ├── [ ] Tree Node
│      ├── [ ] Recursion on tree
│      ├── [ ] Preorder
│      ├── [ ] Inorder
│      └── [ ] Postorder
│
├── TREE PROBLEMS
│      ├── [ ] Maximum Depth
│      ├── [ ] Validate BST
│      ├── [ ] Lowest Common Ancestor
│      ├── [ ] Level Order
│      └── [ ] Build from Preorder/Inorder
│
├── GRAPH FUNDAMENTALS
│      ├── [ ] Adjacency List
│      ├── [ ] Directed vs Undirected
│      ├── [ ] Visited
│      ├── [ ] DFS
│      └── [ ] BFS
│
├── GRAPH PROBLEMS
│      ├── [ ] Number of Islands
│      ├── [ ] Course Schedule
│      ├── [ ] Clone Graph
│      ├── [ ] Word Ladder
│      └── [ ] Graph Valid Tree
│
└── ADVANCED
       ├── [ ] Topological Sort
       ├── [ ] Union-Find
       └── [ ] Alien Dictionary


# SET 6 — COMPLEXITY CHEAT SHEET

TREE TRAVERSAL
    ↓
O(n)


MAX DEPTH
    ↓
O(n)


VALIDATE BST
    ↓
O(n)


LEVEL ORDER
    ↓
O(n)


BUILD TREE
    ↓
O(n)
with hashmap optimization


GRAPH DFS
    ↓
O(V + E)


GRAPH BFS
    ↓
O(V + E)


NUMBER OF ISLANDS
    ↓
O(rows × cols)


TOPOLOGICAL SORT
    ↓
O(V + E)


CLONE GRAPH
    ↓
O(V + E)


WORD LADDER
    ↓
depends on word-generation approach;
BFS is the core pattern.


UNION-FIND
    ↓
near-constant amortized
per operation with
path compression + union by rank/size.


# SET 6 — COMMON TRAPS

## TREE

├── [ ] Forgetting null base case
├── [ ] Mixing traversal orders
├── [ ] Incorrect BST validation
└── [ ] Confusing BST LCA with general-tree LCA


## GRAPH

├── [ ] Forgetting visited
├── [ ] Using DFS when shortest unweighted path needs BFS
├── [ ] Treating directed graph as undirected
├── [ ] Treating undirected graph as directed
├── [ ] Wrong cycle-detection method
└── [ ] Forgetting disconnected components


The Geetha explicitly identifies these as common graph-interview traps. :contentReference[oaicite:27]{index=27}


# SET 6 — EDGE CASES

GRAPH

├── [ ] Single node
├── [ ] No edges
├── [ ] Disconnected graph
├── [ ] Cycle
├── [ ] Fully connected graph
└── [ ] One central hub


TREE

├── [ ] Empty tree
├── [ ] One node
├── [ ] Only left children
├── [ ] Only right children
├── [ ] Balanced tree
└── [ ] Highly skewed tree


The Geetha explicitly lists disconnected graphs, single-node graphs, no-edge graphs, cyclic graphs, and highly centralized graphs among graph edge cases. :contentReference[oaicite:28]{index=28}


# SET 6 — CORE TEMPLATES

## TREE DFS

```cpp
void dfs(TreeNode* root)
{
    if(root == nullptr)
        return;

    dfs(root->left);

    // process root
    dfs(root->right);
}




























GRAPH DFS
void dfs(int node,
         vector<vector<int>>& adj,
         vector<int>& visited)
{
    visited[node] = 1;

    for(int next : adj[node])
    {
        if(!visited[next])
        {
            dfs(next, adj, visited);
        }
    }
}
GRAPH BFS
queue<int> q;

q.push(start);
visited[start] = 1;

while(!q.empty())
{
    int node = q.front();
    q.pop();

    for(int next : adj[node])
    {
        if(!visited[next])
        {
            visited[next] = 1;
            q.push(next);
        }
    }
}
TOPOLOGICAL SORT — KAHN
queue<int> q;

for(int i = 0; i < n; i++)
{
    if(indegree[i] == 0)
        q.push(i);
}

int count = 0;

while(!q.empty())
{
    int node = q.front();
    q.pop();

    count++;

    for(int next : adj[node])
    {
        indegree[next]--;

        if(indegree[next] == 0)
            q.push(next);
    }
}

if(count != n)
{
    // cycle exists
}
SET 6 — MASTER MEMORY TREE

TREES
│
├── DFS
│ ↓
│ RECURSION
│
├── INORDER
│ ↓
│ LEFT ROOT RIGHT
│
├── BST
│ ↓
│ ORDERING
│
├── BFS
│ ↓
│ QUEUE
│
└── CONSTRUCTION
↓
PREORDER + INORDER

GRAPHS
│
├── REPRESENT
│ ↓
│ ADJACENCY LIST
│
├── DFS
│ ↓
│ CONNECTIVITY / EXISTS
│
├── BFS
│ ↓
│ SHORTEST UNWEIGHTED
│
├── VISITED
│ ↓
│ PREVENT REVISIT
│
├── CYCLE
│ ↓
│ DETECT INVALID LOOP
│
├── TOPO
│ ↓
│ DEPENDENCIES
│
├── UNION-FIND
│ ↓
│ COMPONENTS / CONNECTIVITY
│
└── DIJKSTRA
↓
WEIGHTED SHORTEST PATH

SET 6 — FINAL RECOGNITION RULES
Tree traversal → think DFS/recursion.
Inorder → LEFT → ROOT → RIGHT.
BST inorder → sorted order.
Maximum tree depth → 1 + max(left,right).
Validate BST → global range, not just parent comparison.
Level order → BFS + queue.
Build tree from preorder/inorder → preorder gives root; inorder splits left/right.
Grid problems can be graph problems.
Number of Islands → DFS/BFS + visited.
Graph traversal → adjacency list + visited.
DFS → connectivity / existence.
BFS → shortest path in unweighted graph.
Course prerequisites → directed graph + topological sort.
Topological ordering exists only when dependency graph has no cycle.
Clone graph → original-to-copy mapping.
Word Ladder → words as nodes + BFS for shortest transformation.
Graph Valid Tree → connected + acyclic.
Alien Dictionary → character dependencies + topological sort.
Union-Find → dynamic connectivity.
Always determine directed vs undirected before choosing the cycle algorithm.
For graph problems, mark visited deliberately.
If the problem asks for shortest unweighted path, think BFS before DFS.
If the problem asks for dependency/order, think Topological Sort.
If the problem asks about connected components, think DFS/BFS or Union-Find.
If the graph is weighted and asks for shortest path, the Geetha points to Dijkstra.
SET 6 — COMPLETE STORY

TREE
↓
DFS / BFS
↓
TRAVERSAL
↓
BST
↓
ORDERING

GRID
↓
GRAPH
↓
DFS / BFS
↓
VISITED
↓
COMPONENTS

DEPENDENCIES
↓
DIRECTED GRAPH
↓
TOPOLOGICAL SORT
↓
CYCLE DETECTION

SHORTEST UNWEIGHTED
↓
BFS

SHORTEST WEIGHTED
↓
DIJKSTRA

DYNAMIC CONNECTIVITY
↓
UNION-FIND

SET 6 — THE MOST IMPORTANT CONNECTION

All of these look like different problems:

Number of Islands
Course Schedule
Word Ladder
Clone Graph
Graph Valid Tree
Alien Dictionary

But mentally:

NUMBER OF ISLANDS
↓
CONNECTED COMPONENT

COURSE SCHEDULE
↓
DEPENDENCY GRAPH

WORD LADDER
↓
SHORTEST PATH

CLONE GRAPH
↓
GRAPH TRAVERSAL + MAPPING

GRAPH VALID TREE
↓
CONNECTIVITY + CYCLE

ALIEN DICTIONARY
↓
DEPENDENCY + TOPOLOGICAL SORT

So don't memorize six independent solutions.

Learn:

GRAPH
│
├── DFS
├── BFS
├── VISITED
├── CYCLE
├── TOPO
└── CONNECTIVITY

Then map the story to the pattern.

SET 6 — COMPLETION TARGET

Before moving to Set 7, you should be able to immediately decode:

"Visit left, root, right"
↓
INORDER

"Maximum depth"
↓
TREE RECURSION

"Is this a valid BST?"
↓
RANGE / INORDER

"Level by level"
↓
BFS + QUEUE

"Count islands"
↓
GRID + DFS/BFS + VISITED

"Can all courses be completed?"
↓
DIRECTED GRAPH + TOPOLOGICAL SORT

"Shortest word transformation"
↓
GRAPH + BFS

"Clone graph"
↓
DFS/BFS + HASHMAP

"Is graph a tree?"
↓
CONNECTED + ACYCLIC

"Find alien character order"
↓
DEPENDENCY GRAPH + TOPO

"Dynamic connectivity"
↓
UNION-FIND

    dfs(root->right);
}
