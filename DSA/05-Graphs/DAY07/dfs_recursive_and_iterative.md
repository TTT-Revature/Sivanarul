
# DFS – Recursive and Iterative

## 1. Introduction to DFS

Depth-First Search (DFS) is a graph traversal algorithm that explores as far as possible along one path before backtracking.

Unlike BFS, which explores level by level, DFS explores depth first.

### Real-world analogy

Imagine exploring a maze.

1. Start at the entrance.
2. Choose one available path.
3. Continue moving forward.
4. If you reach a dead end, go back.
5. Explore another available path.

This is the basic idea behind DFS.

## 2. How DFS Works

Consider this graph:

        A
       / \
      B   C
     / \   \
    D   E   F

Starting vertex: A

Assume we visit neighbors from left to right.

DFS traversal:

A → B → D → E → C → F

Explanation:

1. Start at A.
2. Move to B.
3. Move deeper to D.
4. D has no unvisited neighbors, so backtrack to B.
5. Visit E.
6. Backtrack to A.
7. Visit C.
8. Visit F.

The traversal order depends on the order in which neighbors are stored.

## 3. Why Does DFS Use a Stack?

DFS uses a Stack data structure.

A stack follows LIFO:

Last In, First Out.

The most recently added element is removed first.

Two important stack operations:

- push: add an element.
- pop: remove the top element.

DFS can be implemented in two ways:

1. Recursive DFS – uses the function call stack automatically.
2. Iterative DFS – uses an explicit stack created by the programmer.

## 4. Recursive DFS

Recursion means a function calls itself.

In recursive DFS, the function visits a vertex and calls itself for every unvisited neighbor.

### Algorithm

1. Select a starting vertex.
2. Mark it as visited.
3. Process the current vertex.
4. Check all its neighbors.
5. If a neighbor is unvisited, recursively call DFS for that neighbor.
6. Continue until no unvisited neighbors remain.

### Pseudocode

```text
DFS(graph, current):

    mark current as visited

    process current

    for each neighbor of current:

        if neighbor is not visited:

            DFS(graph, neighbor)
```

## 5. Recursive DFS Implementation Using Python

Let's represent the graph using an adjacency list.

```python
graph = {
    "A": ["B", "C"],
    "B": ["A", "D", "E"],
    "C": ["A", "F"],
    "D": ["B"],
    "E": ["B"],
    "F": ["C"]
}
```

### Complete code

```python
def dfs_recursive(graph, current, visited):

    visited.add(current)

    print(current, end=" ")

    for neighbor in graph[current]:

        if neighbor not in visited:

            dfs_recursive(graph, neighbor, visited)


graph = {
    "A": ["B", "C"],
    "B": ["A", "D", "E"],
    "C": ["A", "F"],
    "D": ["B"],
    "E": ["B"],
    "F": ["C"]
}

visited = set()

dfs_recursive(graph, "A", visited)
```

### Output

```text
A B D E C F
```

## 6. Understanding Recursive DFS

Let's understand the important statements.

### Step 1: Define the function

```python
def dfs_recursive(graph, current, visited):
```

Parameters:

- graph: stores vertices and their neighbors.
- current: vertex currently being processed.
- visited: tracks already visited vertices.

### Step 2: Mark the current vertex

```python
visited.add(current)
```

Prevents the same vertex from being processed repeatedly.

### Step 3: Process the vertex

```python
print(current, end=" ")
```

Displays the current vertex.

### Step 4: Explore neighbors

```python
for neighbor in graph[current]:
```

Checks every neighbor of the current vertex.

### Step 5: Check whether it is visited

```python
if neighbor not in visited:
```

Only unvisited neighbors should be explored.

### Step 6: Recursive call

```python
dfs_recursive(graph, neighbor, visited)
```

The function calls itself to explore the next vertex.

This continues until there are no unvisited neighbors.

## 7. Understanding Recursion and Backtracking

Consider:

        A
       / \
      B   C
     / \
    D   E

Starting from A:

```text
DFS(A)
  |
  v
DFS(B)
  |
  v
DFS(D)
  |
  v
No unvisited neighbor
  |
  v
Return to B
  |
  v
DFS(E)
  |
  v
Return to B
  |
  v
Return to A
  |
  v
DFS(C)
```

Traversal:

```text
A B D E C
```

### Important concept: Call Stack

When a recursive function calls another function, Python keeps track of the current function call.

For example:

```text
DFS(A)
  DFS(B)
    DFS(D)
```

The function calls are stored in the call stack.

When DFS(D) finishes, execution returns to DFS(B).

This process is called backtracking.

## 8. Iterative DFS

Recursive DFS uses Python's internal function call stack.

Iterative DFS uses an explicit stack.

Instead of calling the function recursively, we manually push and pop vertices.

### Algorithm

1. Create an empty visited set.
2. Create a stack.
3. Push the starting vertex.
4. While the stack is not empty:
   - Pop the top vertex.
   - If it is not visited:
     - Mark it as visited.
     - Process it.
     - Push its unvisited neighbors.

### Pseudocode

```text
DFS_ITERATIVE(graph, start):

    create empty stack
    create empty visited set

    push start into stack

    while stack is not empty:

        current = pop from stack

        if current is not visited:

            mark current as visited

            process current

            for each neighbor of current:

                if neighbor is not visited:

                    push neighbor into stack
```

## 9. Iterative DFS Implementation Using Python

```python
def dfs_iterative(graph, start):

    visited = set()

    stack = [start]

    while stack:

        current = stack.pop()

        if current not in visited:

            visited.add(current)

            print(current, end=" ")

            for neighbor in reversed(graph[current]):

                if neighbor not in visited:

                    stack.append(neighbor)


graph = {
    "A": ["B", "C"],
    "B": ["A", "D", "E"],
    "C": ["A", "F"],
    "D": ["B"],
    "E": ["B"],
    "F": ["C"]
}

dfs_iterative(graph, "A")
```

### Output

```text
A B D E C F
```

### Why use reversed()?

A stack follows LIFO.

Suppose the neighbors are:

```python
["B", "C"]
```

If we push B first and then C:

```text
Stack: B, C
```

C will be popped first.

To visit B first, we push neighbors in reverse order:

```python
for neighbor in reversed(graph[current]):
```

This makes the iterative traversal match the recursive left-to-right traversal for this graph.

Important: Reversing neighbors is not mandatory. It only controls traversal order.

## 10. Recursive DFS vs Iterative DFS

| Feature | Recursive DFS | Iterative DFS |
|---|---|---|
| Technique | Function calls itself | Uses explicit stack |
| Stack | Python call stack | List or stack |
| Implementation | Shorter | More manual control |
| Backtracking | Automatic | Managed manually |
| Deep graphs | Can hit recursion limit | Avoids Python recursion limit |
| Time complexity | O(V + E) | O(V + E) |
| Auxiliary space | O(V) worst case | O(V) worst case |

### When should you use each?

Recursive DFS:

- When the graph or tree depth is manageable.
- When you want simpler code.
- When recursion makes the problem easier to understand.

Iterative DFS:

- When graphs may be very deep.
- When you want to avoid Python recursion limits.
- When you need explicit control over the stack.

## 11. Problem Solving Using DFS

### Problem 1: Count Reachable Vertices

Suppose we want to find how many vertices are reachable from a starting vertex.

DFS can solve this problem.

```python
def count_reachable(graph, start):

    visited = set()

    def dfs(current):

        visited.add(current)

        for neighbor in graph[current]:

            if neighbor not in visited:

                dfs(neighbor)

    dfs(start)

    return len(visited)


graph = {
    "A": ["B", "C"],
    "B": ["A", "D"],
    "C": ["A"],
    "D": ["B"],
    "E": ["F"],
    "F": ["E"]
}

print(count_reachable(graph, "A"))
```

### Output

```text
4
```

Explanation:

Starting from A, DFS can reach:

A, B, C, D

Vertices E and F belong to a disconnected component.

## 12. Problem 2: Detect a Cycle in an Undirected Graph

DFS can help detect cycles in an undirected graph.

Consider:

```text
A ----- B
|       |
|       |
D ----- C
```

There is a cycle:

A → B → C → D → A

### Important concept: Parent vertex

In an undirected graph, every edge appears in both directions.

For example:

```python
"A": ["B"]
"B": ["A"]
```

When DFS moves from A to B, it sees A again as B's neighbor.

That is not a cycle. It is simply the edge we just used.

Therefore, we track the parent vertex.

A cycle exists if we find an already visited neighbor that is not the current vertex's parent.

### Python implementation

```python
def has_cycle(graph):

    visited = set()

    def dfs(current, parent):

        visited.add(current)

        for neighbor in graph[current]:

            if neighbor not in visited:

                if dfs(neighbor, current):
                    return True

            elif neighbor != parent:

                return True

        return False

    for vertex in graph:

        if vertex not in visited:

            if dfs(vertex, None):
                return True

    return False


graph = {
    "A": ["B", "D"],
    "B": ["A", "C"],
    "C": ["B", "D"],
    "D": ["A", "C"]
}

print(has_cycle(graph))
```

### Output

```text
True
```

The graph contains a cycle.

Note: This implementation assumes a simple undirected graph without self-loops or parallel edges. Directed graph cycle detection requires a different approach.

## 13. Problem 3: Traverse Every Connected Component

A graph may contain multiple disconnected components.

Example:

```text
A --- B --- C

D --- E

F
```

Starting DFS from A only visits A, B, and C.

To visit every vertex, run DFS from each unvisited vertex.

### Python implementation

```python
def dfs_all(graph):

    visited = set()

    def dfs(current):

        visited.add(current)

        print(current, end=" ")

        for neighbor in graph[current]:

            if neighbor not in visited:

                dfs(neighbor)

    for vertex in graph:

        if vertex not in visited:

            dfs(vertex)


graph = {
    "A": ["B"],
    "B": ["A", "C"],
    "C": ["B"],
    "D": ["E"],
    "E": ["D"],
    "F": []
}

dfs_all(graph)
```

### Output

```text
A B C D E F
```

This approach visits every vertex, including isolated vertices.

## 14. DFS Time and Space Complexity

Let:

- V = Number of vertices.
- E = Number of edges.

For an adjacency list:

| Operation | Complexity |
|---|---|
| Visit each vertex | O(V) |
| Examine all edges | O(E) |
| Total DFS time | O(V + E) |
| Visited set | O(V) |
| Stack / recursion calls | O(V) worst case |
| Total auxiliary space | O(V) |

### Why O(V + E)?

DFS visits every vertex at most once.

It examines every adjacency-list entry.

For an undirected graph, each edge generally appears twice in the adjacency lists.

Therefore:

Time Complexity = O(V + E)

Space Complexity = O(V)

For an adjacency matrix, DFS takes O(V²) time because it scans an entire row to identify neighbors.

## 15. BFS vs DFS

| Feature | BFS | DFS |
|---|---|---|
| Full form | Breadth-First Search | Depth-First Search |
| Exploration | Level by level | Depth first |
| Data structure | Queue | Stack |
| Recursive implementation | Possible | Common |
| Iterative implementation | Possible | Common |
| Shortest path in unweighted graph | Guaranteed | Not guaranteed |
| Cycle detection | Possible | Possible |
| Time complexity | O(V + E) | O(V + E) |
| Auxiliary space | O(V) | O(V) |

### Visual comparison

Graph:

```text
        A
       / \
      B   C
     / \   \
    D   E   F
```

BFS traversal:

```text
A → B → C → D → E → F
```

DFS traversal:

```text
A → B → D → E → C → F
```

Both algorithms visit all reachable vertices, but their exploration order differs.

## 16. Real-World Applications of DFS

1. Maze solving
   - Explore a path until a dead end, then backtrack.

2. Cycle detection
   - Identify cycles in dependency graphs.

3. Dependency resolution
   - Explore relationships between tasks or packages.

4. Connected components
   - Find separate groups in a network.

5. Topological sorting
   - Process dependencies in a directed acyclic graph (DAG).

6. File system traversal
   - Explore nested folders and their contents.

### FDE Connection

Imagine an AI workflow with task dependencies:

```text
       Start
         |
         v
    Extract Data
       /    \
      v      v
  Validate  Clean
      \      /
       v    v
      Store
        |
        v
      Report
```

DFS can explore a dependency graph by following one branch deeply before exploring another.

This is useful when inspecting workflow dependencies, exploring connected systems, and detecting certain dependency cycles.

DFS alone does not guarantee that tasks execute in a valid dependency order. For that, a DAG and a topological ordering may be required.

## 17. Common Mistakes

### Mistake 1: Forgetting the visited set

Graphs can contain cycles.

Without visited tracking, DFS may repeatedly explore the same vertices.

### Mistake 2: Confusing recursion with iteration

Recursive DFS uses function calls.

Iterative DFS uses an explicit stack.

Both implement depth-first traversal.

### Mistake 3: Forgetting to backtrack

Recursive DFS automatically returns to the previous function call after exploring a branch.

This is how it explores alternative paths.

### Mistake 4: Assuming DFS finds the shortest path

DFS does not guarantee the shortest path.

BFS is generally the correct choice for shortest paths in unweighted graphs.

### Mistake 5: Ignoring recursion limits

A deeply nested graph can cause Python's recursion limit to be exceeded.

Use iterative DFS for very deep graphs when appropriate.

### Mistake 6: Assuming one DFS visits the entire graph

A DFS starting from one vertex only visits vertices reachable from that vertex.

Use an outer loop to cover disconnected components.

## 18. Practice Exercises

### Beginner

1. Implement recursive DFS for a graph containing five vertices.
2. Implement iterative DFS using a Python list as a stack.
3. Explain why DFS uses a stack.
4. What is the purpose of the visited set?
5. What is backtracking in DFS?

### Intermediate

6. Count reachable vertices using recursive DFS.
7. Traverse all connected components.
8. Detect a cycle in an undirected graph.
9. Find whether a path exists between two vertices.
10. Convert recursive DFS into iterative DFS.

### Interview-Level Thinking

11. What is the difference between the call stack and an explicit stack?
12. Why can recursive DFS cause a RecursionError?
13. Can DFS find the shortest path in an unweighted graph?
14. Can two DFS traversals of the same graph produce different orders?
15. How can DFS be used for topological sorting?

## 19. Quick Revision

| Concept | Remember |
|---|---|
| DFS | Depth-First Search |
| Traversal | Explore deeply, then backtrack |
| Recursive technique | Function calls itself |
| Iterative technique | Explicit stack |
| Stack principle | LIFO |
| Python stack | List |
| Add element | `append()` |
| Remove top | `pop()` |
| Visited tracking | Set |
| Time complexity | O(V + E), adjacency list |
| Space complexity | O(V) |
| Shortest path | Not guaranteed |

## 20. Self-Assessment

You should be able to answer these questions before moving forward:

- What is DFS?
- How does DFS differ from BFS?
- Why does DFS use a stack?
- How does recursive DFS work?
- How does iterative DFS work?
- What is backtracking?
- Why is a visited set necessary?
- How can DFS detect cycles in an undirected graph?
- What are the time and space complexities?
- When should you choose DFS over BFS?

## 21. Learning Outcome

After completing this topic, you should be able to:

1. Explain Depth-First Search.
2. Understand recursion and backtracking.
3. Implement recursive DFS.
4. Implement iterative DFS using a stack.
5. Count reachable vertices.
6. Detect cycles in an undirected graph.
7. Traverse disconnected graphs.
8. Analyze DFS time and space complexity.

**Next recommended topic:** Graph Cycle Detection – Directed and Undirected Graphs.
