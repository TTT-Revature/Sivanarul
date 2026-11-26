
# Union-Find / Disjoint Set (DSU)

## 1. Introduction

Union-Find, also called **Disjoint Set Union (DSU)**, is a data structure used to manage multiple separate groups of elements.

It helps us answer two important questions:

1. Are two elements part of the same group?
2. Can we combine two different groups into one?

### Real-world example

Imagine a social network with six users:

A, B, C, D, E, F

Initially, every user belongs to a separate group.

After some connections:

- A connects with B.
- B connects with C.
- D connects with E.

The groups become:

```text
Group 1: A --- B --- C

Group 2: D --- E

Group 3: F
```

Now we can quickly check:

- Are A and C in the same group? YES.
- Are A and E in the same group? NO.
- What happens if C connects with D? Both groups merge.

This is exactly what Union-Find does.

---

## 2. What Is a Disjoint Set?

A disjoint set is a collection of sets where no element belongs to more than one set.

Example:

```text
Set 1 = {A, B, C}
Set 2 = {D, E}
Set 3 = {F}
```

These sets are disjoint because they have no common elements.

Initially, every element is placed in its own set.

```text
{A}  {B}  {C}  {D}  {E}  {F}
```

Union-Find manages these sets efficiently.

---

## 3. Two Main Operations

Union-Find mainly supports two operations.

### A. Find

The Find operation identifies which group an element belongs to.

It returns the representative (root or leader) of that group.

Example:

```text
A --- B --- C
```

If A is the representative:

```text
Find(A) = A
Find(B) = A
Find(C) = A
```

All three elements belong to the same group.

### B. Union

The Union operation combines two different groups into one.

Before Union:

```text
Group 1       Group 2

A --- B       C --- D
```

Operation:

```python
union(A, C)
```

After Union:

```text
A --- B
|
C --- D
```

Now all four elements belong to the same group.

**Important:** Union combines groups, not just two individual values.

---

## 4. How Does Union-Find Work Internally?

A common implementation uses an array called `parent`.

Each element stores the parent of that element.

Initially, every element is its own parent.

```python
parent = [0, 1, 2, 3, 4]
```

This means:

```text
0 is its own parent
1 is its own parent
2 is its own parent
3 is its own parent
4 is its own parent
```

Visual representation:

```text
0    1    2    3    4
```

Each element is initially a separate group.

After some Union operations, the parent array may look like:

```python
parent = [0, 0, 0, 3, 3]
```

The groups are:

```text
       0             3
      / \            |
     1   2            4
```

Here:

- 0 is the representative of group 1.
- 3 is the representative of group 2.

The parent array represents a collection of trees.

Each tree represents one disjoint set.

---

## 5. Basic Find Operation

The Find operation follows parent references until it reaches the root.

A root is an element whose parent is itself.

### Python implementation

```python
def find(parent, x):

    if parent[x] == x:
        return x

    return find(parent, parent[x])
```

### Example

```python
parent = [0, 0, 1, 3, 3]

print(find(parent, 2))
```

Output:

```text
0
```

Explanation:

For element 2:

```text
2 → 1 → 0
```

Since 0 is its own parent, it is the representative.

Therefore:

```text
Find(2) = 0
```

---

## 6. Basic Union Operation

Union combines two groups.

The process:

1. Find the representative of the first element.
2. Find the representative of the second element.
3. If both representatives are the same, they are already connected.
4. Otherwise, make one representative the parent of the other.

### Python implementation

```python
def union(parent, x, y):

    root_x = find(parent, x)
    root_y = find(parent, y)

    if root_x != root_y:
        parent[root_y] = root_x
```

### Example

```python
parent = [0, 1, 2, 3, 4]

union(parent, 0, 1)
union(parent, 2, 3)

print(parent)
```

Possible output:

```text
[0, 0, 2, 2, 4]
```

Explanation:

After `union(0, 1)`:

```text
0
|
1
```

After `union(2, 3)`:

```text
0       2
|       |
1       3

4
```

Three groups remain:

```text
{0, 1}
{2, 3}
{4}
```

The exact representative depends on the implementation.

---

## 7. Checking Whether Two Elements Are Connected

We can use Find to determine whether two elements belong to the same group.

```python
def connected(parent, x, y):

    return find(parent, x) == find(parent, y)
```

Example:

```python
parent = [0, 0, 2, 2, 4]

print(connected(parent, 0, 1))
print(connected(parent, 0, 3))
```

Output:

```text
True
False
```

Explanation:

- 0 and 1 have the same representative.
- 0 and 3 have different representatives.

---

## 8. Problem With Basic Union-Find

The basic implementation can create a long chain.

Example:

```text
0
|
1
|
2
|
3
|
4
```

To find the representative of 4, we must travel through several parent references.

For a badly shaped tree, Find can take O(n) time.

We can improve this using two important techniques:

1. Path Compression
2. Union by Rank or Union by Size

---

## 9. Path Compression

Path Compression optimizes the Find operation.

Instead of keeping every element connected through a long chain, it directly connects visited elements to the root.

### Before Find

```text
0
|
1
|
2
|
3
|
4
```

Operation:

```python
find(4)
```

### After Find with Path Compression

```text
    0
  / | | \
 1  2 3  4
```

Now every visited element points directly to the representative.

### Python implementation

```python
def find(parent, x):

    if parent[x] != x:
        parent[x] = find(parent, parent[x])

    return parent[x]
```

Important line:

```python
parent[x] = find(parent, parent[x])
```

It updates the parent of the current element to the root.

This makes future Find operations faster.

---

## 10. Union by Rank

Union by Rank prevents unnecessarily tall trees.

Rank is an estimate of a tree's height.

Initially, every element has rank 0.

```python
rank = [0, 0, 0, 0, 0]
```

When combining two trees:

- Attach the smaller-rank tree below the larger-rank tree.
- If both ranks are equal, choose one as the parent and increase its rank by 1.

### Python implementation

```python
def union(parent, rank, x, y):

    root_x = find(parent, x)
    root_y = find(parent, y)

    if root_x == root_y:
        return

    if rank[root_x] < rank[root_y]:

        parent[root_x] = root_y

    elif rank[root_x] > rank[root_y]:

        parent[root_y] = root_x

    else:

        parent[root_y] = root_x
        rank[root_x] += 1
```

### Example

Suppose:

```text
Tree A: rank 1
Tree B: rank 2
```

Union will attach Tree A below Tree B.

```text
Before:

   A             B
  /             / \
 A1            B1  B2

After:

       B
      /|\
     B1 B2 A
            |
            A1
```

The lower-rank tree is attached below the higher-rank tree.

**Note:** Rank is not always the exact current height after path compression. It is an upper-bound-style balancing measure maintained by the algorithm.

---

## 11. Union by Size

Another optimization is Union by Size.

Instead of comparing ranks, we compare the number of elements in each set.

Initially:

```python
size = [1, 1, 1, 1, 1]
```

When combining two sets:

- Attach the smaller set below the larger set.
- Update the size of the new representative.
- The size of a non-representative is no longer maintained as an authoritative set size.

### Python implementation

```python
def union(parent, size, x, y):

    root_x = find(parent, x)
    root_y = find(parent, y)

    if root_x == root_y:
        return

    if size[root_x] < size[root_y]:

        parent[root_x] = root_y
        size[root_y] += size[root_x]

    else:

        parent[root_y] = root_x
        size[root_x] += size[root_y]
```

Union by Rank and Union by Size are alternative balancing strategies.

Both can be combined with Path Compression.

---

## 12. Complete Optimized Union-Find Implementation

The following implementation uses:

- Path Compression
- Union by Rank
- Find
- Union
- Connected

```python
class DisjointSet:

    def __init__(self, n):

        self.parent = list(range(n))
        self.rank = [0] * n

    def find(self, x):

        if self.parent[x] != x:

            self.parent[x] = self.find(self.parent[x])

        return self.parent[x]

    def union(self, x, y):

        root_x = self.find(x)
        root_y = self.find(y)

        if root_x == root_y:
            return False

        if self.rank[root_x] < self.rank[root_y]:

            self.parent[root_x] = root_y

        elif self.rank[root_x] > self.rank[root_y]:

            self.parent[root_y] = root_x

        else:

            self.parent[root_y] = root_x
            self.rank[root_x] += 1

        return True

    def connected(self, x, y):

        return self.find(x) == self.find(y)


ds = DisjointSet(5)

ds.union(0, 1)
ds.union(1, 2)
ds.union(3, 4)

print(ds.connected(0, 2))
print(ds.connected(0, 4))
print(ds.connected(3, 4))
```

Output:

```text
True
False
True
```

Explanation:

```text
Group 1: {0, 1, 2}

Group 2: {3, 4}
```

- 0 and 2 belong to the same group.
- 0 and 4 belong to different groups.
- 3 and 4 belong to the same group.

---

## 13. Time Complexity

Let:

- n = number of elements.
- α(n) = inverse Ackermann function.

| Operation | Basic Implementation | Optimized DSU |
|---|---:|---:|
| Initialization | O(n) | O(n) |
| Find | O(n) worst case | O(α(n)) amortized |
| Union | O(n) worst case | O(α(n)) amortized |
| Connected | O(n) worst case | O(α(n)) amortized |

With both Path Compression and Union by Rank (or Size), a sequence of operations takes nearly linear total time.

The inverse Ackermann function grows extremely slowly. For all practical input sizes, its value is very small.

Space Complexity:

```text
O(n)
```

Because we maintain parent and rank (or size) arrays.

---

## 14. Union-Find vs Graph Traversal

Both Union-Find and graph traversal can help determine connectivity, but they solve the problem differently.

| Feature | Union-Find | BFS / DFS |
|---|---|---|
| Main purpose | Manage connected groups | Explore graph |
| Find connectivity | Very efficient for incremental connections | Traverse the graph |
| Add connections | Efficient Union operation | Graph structure must be updated |
| Shortest path | Not supported | BFS supports unweighted shortest paths |
| Store graph paths | No | Can store parents during traversal |
| Typical complexity | Nearly O(1) amortized per operation | O(V + E) traversal |

**Important:** Union-Find does not calculate shortest paths or tell us the actual sequence of edges connecting two vertices. It only tells us whether they belong to the same component.

---

## 15. Applications of Union-Find

### A. Detecting Cycles in an Undirected Graph

Consider:

```text
A ----- B
|       |
|       |
C ----- D
```

When processing an edge:

1. Find the representative of both endpoints.
2. If both endpoints already have the same representative, adding this edge creates a cycle.
3. Otherwise, perform Union.

This is a common application of DSU.

### B. Kruskal's Minimum Spanning Tree Algorithm

Kruskal's algorithm selects edges in increasing order of weight.

Union-Find checks whether an edge connects two different components.

- Different components: select the edge and perform Union.
- Same component: skip the edge because it would create a cycle.

### C. Social Networks

Manage groups of connected users.

Example:

```text
User A connects with User B.
User B connects with User C.
```

We can quickly determine whether A and C belong to the same connected group.

### D. Network Connectivity

Suppose computers are connected through network cables.

Union-Find helps determine whether two computers belong to the same connected component.

### E. Image Processing

Some image-processing algorithms use connected-component labeling to group neighboring pixels with similar properties. Disjoint-set structures can help merge provisional component labels.

---

## 16. Union-Find in an FDE Scenario

Imagine an enterprise system that manages connections between different services.

```text
Service A ---- Service B

Service C ---- Service D

Service E
```

You receive new connection events:

```text
Connect A with C
Connect B with E
```

The system must determine which services belong to the same connected group.

Union-Find can efficiently manage these groups.

Potential use cases:

- Network connectivity monitoring.
- Grouping connected entities.
- Dependency analysis in undirected relationships.
- Processing large connectivity datasets.

However, DSU is not a replacement for a complete workflow engine or dependency graph. It is designed specifically for disjoint-set connectivity management.

---

## 17. Common Mistakes

1. **Confusing Find and Union**
   - Find identifies the representative.
   - Union combines two sets.

2. **Using the element instead of its representative**
   - Always call Find before changing parent relationships in Union.

3. **Forgetting Path Compression**
   - Without it, Find may repeatedly traverse long chains.

4. **Forgetting Union by Rank or Size**
   - Trees may become unnecessarily tall.

5. **Assuming DSU gives the shortest path**
   - DSU only identifies whether two elements belong to the same set.

6. **Assuming Union always changes the structure**
   - If both elements already have the same representative, Union does nothing.

7. **Using ordinary DSU for arbitrary deletions**
   - Standard DSU handles additions and merges efficiently, but does not directly support splitting a set when an edge is removed.

---

## 18. Practice Exercises

### Beginner

1. What is a Disjoint Set?
2. What is the difference between Find and Union?
3. Initially, how many sets exist for 8 elements?
4. What does a representative element mean?
5. What is Path Compression?

### Intermediate

6. Given:

```python
ds = DisjointSet(6)

ds.union(0, 1)
ds.union(1, 2)
ds.union(3, 4)
```

Determine:

```python
ds.connected(0, 2)
ds.connected(0, 4)
ds.connected(3, 5)
```

7. Why do we use Union by Rank?
8. What happens when we Union two elements that already belong to the same set?
9. Why is the parent array represented as a collection of trees?

### Advanced

10. How can Union-Find detect a cycle in an undirected graph?
11. How does Kruskal's algorithm use Union-Find?
12. Why is Union-Find not suitable for shortest-path problems?
13. What is the difference between Union by Rank and Union by Size?
14. Why is the optimized operation complexity expressed using the inverse Ackermann function?

---

## 19. Quick Revision

| Concept | Meaning |
|---|---|
| Union-Find | Data structure for managing disjoint sets |
| DSU | Disjoint Set Union |
| Find | Returns the representative of a set |
| Union | Combines two sets |
| Parent | Stores parent references |
| Representative | Root of a set's tree |
| Path Compression | Connects visited nodes directly to the root |
| Union by Rank | Attaches the shorter-rank tree below the taller-rank tree |
| Union by Size | Attaches the smaller set below the larger set |
| Optimized Find | O(α(n)) amortized |
| Space Complexity | O(n) |

---

## 20. Learning Outcome

After completing this topic, you should be able to:

- Explain Disjoint Sets and their purpose.
- Implement Find and Union in Python.
- Understand parent arrays and representative elements.
- Apply Path Compression.
- Apply Union by Rank and Union by Size.
- Analyze optimized DSU complexity.
- Detect cycles in undirected graphs.
- Understand how Kruskal's algorithm uses DSU.

### Recommended Next Topic

**Minimum Spanning Tree (MST) – Prim's and Kruskal's Algorithms**

Union-Find is especially important for understanding Kruskal's algorithm.
