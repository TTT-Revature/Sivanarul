
# BFS – Implementation and Problem Solving

## 1. Introduction to BFS

Breadth-First Search (BFS) is a graph traversal algorithm that explores a graph level by level.

It visits all immediate neighbors of a vertex before moving to the next level.

### Real-world analogy

Imagine searching for a person in a social network.

- First, check your direct friends.
- Next, check your friends' friends.
- Then, check the next level of connections.

This is the basic idea behind BFS.

## 2. How BFS Works

Consider this graph:

        A
       / \
      B   C
     / \   \
    D   E   F

Starting vertex: A

BFS traversal:

1. Visit A.
2. Visit A's neighbors: B and C.
3. Visit B's unvisited neighbor: D.
4. Visit B's next unvisited neighbor: E.
5. Visit C's unvisited neighbor: F.

BFS order:

A → B → C → D → E → F

Notice that BFS visits nodes level by level.

### Level representation

Level 0: A

Level 1: B, C

Level 2: D, E, F

## 3. Why Does BFS Use a Queue?

BFS uses a Queue data structure.

A queue follows FIFO:

First In, First Out.

The vertex added first is processed first.

Two important queue operations:

- enqueue: add an element to the queue.
- dequeue: remove the first element from the queue.

Python provides `deque` in the `collections` module.

```python
from collections import deque

queue = deque()

queue.append("A")  # Enqueue
queue.popleft()    # Dequeue
```

Why not use a stack?

A stack follows LIFO (Last In, First Out), which produces a different traversal behavior.

## 4. BFS Algorithm – Step by Step

The BFS algorithm follows these steps:

1. Select a starting vertex.
2. Create an empty queue.
3. Mark the starting vertex as visited.
4. Insert the starting vertex into the queue.
5. Repeat while the queue is not empty:
   - Remove the front vertex.
   - Process that vertex.
   - Visit all its unvisited neighbors.
   - Mark each neighbor as visited.
   - Add each neighbor to the queue.

### Pseudocode

```text
BFS(graph, start):

    create an empty queue
    create an empty visited set

    add start to visited
    add start to queue

    while queue is not empty:

        current = remove from queue

        print current

        for each neighbor of current:

            if neighbor is not visited:

                mark neighbor as visited
                add neighbor to queue
```

## 5. BFS Implementation Using Python

Let's represent a graph using an adjacency list.

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

Each key represents a vertex.

Each value contains its neighboring vertices.

### Complete BFS code

```python
from collections import deque

def bfs(graph, start):

    visited = set()

    queue = deque([start])

    visited.add(start)

    while queue:

        current = queue.popleft()

        print(current, end=" ")

        for neighbor in graph[current]:

            if neighbor not in visited:

                visited.add(neighbor)

                queue.append(neighbor)


graph = {
    "A": ["B", "C"],
    "B": ["A", "D", "E"],
    "C": ["A", "F"],
    "D": ["B"],
    "E": ["B"],
    "F": ["C"]
}

bfs(graph, "A")
```

### Output

```text
A B C D E F
```

## 6. Understanding the Code

Let's understand each important statement.

### Step 1: Import deque

```python
from collections import deque
```

Imports the queue implementation.

### Step 2: Create a visited set

```python
visited = set()
```

Stores vertices that have already been discovered.

Why is it needed?

Graphs can contain cycles.

For example:

A → B → C → A

Without tracking visited vertices, BFS might repeatedly visit the same vertices.

### Step 3: Initialize the queue

```python
queue = deque([start])
```

Adds the starting vertex to the queue.

### Step 4: Mark the starting vertex

```python
visited.add(start)
```

Marks the starting vertex as visited when it is enqueued.

This prevents it from being added again through another edge.

### Step 5: Process the queue

```python
while queue:
```

Continues until there are no more vertices to process.

### Step 6: Remove the front vertex

```python
current = queue.popleft()
```

Removes the first vertex from the queue.

### Step 7: Explore neighbors

```python
for neighbor in graph[current]:
```

Checks every neighboring vertex.

### Step 8: Check visited status

```python
if neighbor not in visited:
```

Only processes vertices that have not already been discovered.

### Step 9: Mark and enqueue

```python
visited.add(neighbor)
queue.append(neighbor)
```

Marks the neighbor as visited and adds it to the queue.

Important: Mark a vertex as visited when it is enqueued, not when it is dequeued. This prevents duplicate queue entries.

## 7. BFS Dry Run – Queue Visualization

Consider the same graph:

        A
       / \
      B   C
     / \   \
    D   E   F

Starting vertex: A

| Step | Current | Queue after processing | Visited |
|---|---|---|---|
| Initial | - | A | A |
| 1 | A | B, C | A, B, C |
| 2 | B | C, D, E | A, B, C, D, E |
| 3 | C | D, E, F | A, B, C, D, E, F |
| 4 | D | E, F | A, B, C, D, E, F |
| 5 | E | F | A, B, C, D, E, F |
| 6 | F | Empty | A, B, C, D, E, F |

Final traversal:

```text
A B C D E F
```

Note: The traversal order depends on the order in which neighbors are stored in the adjacency list.

## 8. Problem Solving Using BFS

### Problem 1: Find the Shortest Path in an Unweighted Graph

BFS can find the shortest path in terms of the number of edges in an unweighted graph.

Consider:

    A --- B --- D
    |           |
    C --------- E

Suppose we want to find the shortest path from A to E.

Possible paths:

- A → B → D → E (3 edges)
- A → C → E (2 edges)

BFS finds the shortest path:

A → C → E

Why?

Because BFS explores vertices level by level. It reaches a destination using the minimum number of edges before exploring deeper levels.

### Python implementation – Shortest path

```python
from collections import deque

def shortest_path(graph, start, target):

    queue = deque([start])

    visited = {start}

    parent = {start: None}

    while queue:

        current = queue.popleft()

        if current == target:
            break

        for neighbor in graph[current]:

            if neighbor not in visited:

                visited.add(neighbor)

                parent[neighbor] = current

                queue.append(neighbor)

    if target not in parent:
        return None

    path = []

    current = target

    while current is not None:

        path.append(current)

        current = parent[current]

    path.reverse()

    return path


graph = {
    "A": ["B", "C"],
    "B": ["A", "D"],
    "C": ["A", "E"],
    "D": ["B", "E"],
    "E": ["C", "D"]
}

result = shortest_path(graph, "A", "E")

print(result)
```

### Output

```text
['A', 'C', 'E']
```

### Understanding the parent dictionary

```python
parent = {start: None}
```

Stores the previous vertex used to reach each discovered vertex.

For the shortest path:

```text
A → C → E
```

The parent dictionary becomes:

```python
{
    "A": None,
    "B": "A",
    "C": "A",
    "D": "B",
    "E": "C"
}
```

To reconstruct the path:

1. Start from E.
2. Find its parent C.
3. Find C's parent A.
4. Stop when the parent is None.
5. Reverse the collected path.

This gives:

A → C → E

## 9. Problem 2: Count Reachable Vertices

Suppose we want to find how many vertices can be reached from a given starting vertex.

BFS can solve this problem.

```python
from collections import deque

def count_reachable(graph, start):

    visited = {start}

    queue = deque([start])

    while queue:

        current = queue.popleft()

        for neighbor in graph[current]:

            if neighbor not in visited:

                visited.add(neighbor)

                queue.append(neighbor)

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

Starting from A, the reachable vertices are:

A, B, C, D

Vertices E and F belong to another disconnected component.

## 10. BFS for Disconnected Graphs

A graph may contain multiple disconnected components.

Example:

    A --- B       D --- E
          |
          C

Starting BFS from A only visits:

A, B, C

It cannot reach D and E.

To traverse every component, start BFS from each unvisited vertex.

```python
from collections import deque

def bfs_all(graph):

    visited = set()

    for vertex in graph:

        if vertex not in visited:

            queue = deque([vertex])

            visited.add(vertex)

            while queue:

                current = queue.popleft()

                print(current, end=" ")

                for neighbor in graph[current]:

                    if neighbor not in visited:

                        visited.add(neighbor)

                        queue.append(neighbor)


graph = {
    "A": ["B"],
    "B": ["A", "C"],
    "C": ["B"],
    "D": ["E"],
    "E": ["D"]
}

bfs_all(graph)
```

### Output

```text
A B C D E
```

This approach visits every vertex, including vertices in disconnected components.

## 11. BFS Time and Space Complexity

Let:

- V = Number of vertices
- E = Number of edges

For an adjacency list:

| Operation | Complexity |
|---|---|
| Visit each vertex | O(V) |
| Examine all edges | O(E) |
| Total BFS time | O(V + E) |
| Visited set | O(V) |
| Queue | O(V) |
| Total auxiliary space | O(V) |

### Why O(V + E)?

BFS processes each vertex once.

It also examines each adjacency-list entry.

For an undirected graph, each edge normally appears twice in the adjacency lists, but this is still O(E).

Therefore:

Time Complexity = O(V + E)

Space Complexity = O(V)

For an adjacency matrix, BFS takes O(V²) time because it scans an entire row to find the neighbors of each vertex.

## 12. BFS vs DFS

| Feature | BFS | DFS |
|---|---|---|
| Full form | Breadth-First Search | Depth-First Search |
| Approach | Level by level | Explore deeper first |
| Data structure | Queue | Stack / Recursion |
| Shortest path in unweighted graph | Yes | Not guaranteed |
| Time with adjacency list | O(V + E) | O(V + E) |
| Auxiliary space | O(V) | O(V) |

### Visual difference

BFS:

```text
Visit by levels:

A
B C
D E F
```

DFS (one possible order):

```text
A → B → D → E → C → F
```

The exact DFS order depends on the neighbor ordering and implementation.

## 13. Real-World Applications of BFS

1. Social networks
   - Find people within two or three connection levels.

2. GPS and navigation
   - Find minimum-edge paths when every connection has equal cost.

3. Web crawling
   - Explore pages level by level from a starting URL.

4. Network broadcasting
   - Explore devices reachable through network connections.

5. AI systems
   - Explore possible states in an unweighted state-space graph.

6. Workflow systems
   - Identify all tasks reachable from a particular workflow step.

### FDE Connection

Imagine an AI document-processing workflow:

```text
Upload Document
       |
       v
Extract Text
       |
       v
Validate Data
      / \
     v   v
  Store  Review
     |
     v
  Generate Report
```

BFS can help explore which workflow steps are reachable from a starting step.

For real workflow execution, dependencies, conditions, and task states must also be considered. BFS is a traversal technique, not a complete workflow engine.

## 14. Common Mistakes

### Mistake 1: Not using a visited set

This can cause repeated processing or an infinite loop when cycles exist.

### Mistake 2: Marking visited too late

Marking a vertex only when dequeued can allow it to enter the queue multiple times.

Mark it when enqueued.

### Mistake 3: Using pop(0) with a Python list

```python
queue = []
queue.pop(0)
```

Removing the first element from a Python list takes O(n) time.

Prefer:

```python
from collections import deque

queue = deque()
queue.popleft()
```

### Mistake 4: Assuming BFS always finds the cheapest path

BFS finds a minimum-edge path in an unweighted graph.

It does not generally find the minimum-cost path when edges have different weights.

For weighted graphs with non-negative edge weights, Dijkstra's algorithm is a suitable choice.

### Mistake 5: Assuming every vertex is visited

A BFS starting from one vertex only visits vertices reachable from that vertex.

Use an outer loop to cover disconnected components.

## 15. Practice Exercises

### Beginner

1. Implement BFS for a graph containing five vertices.
2. Find the BFS traversal starting from vertex A.
3. Explain why BFS uses a queue.
4. What happens if the visited set is removed?
5. What is the difference between enqueue and dequeue?

### Intermediate

6. Find the shortest path between two vertices using BFS.
7. Count the number of vertices reachable from a given vertex.
8. Implement BFS for a disconnected graph.
9. Find the minimum number of edges between two vertices.
10. Modify BFS to return the traversal as a Python list instead of printing it.

### Interview-Level Thinking

11. Why must a vertex be marked visited when it is enqueued?
12. Can BFS find the shortest path in a weighted graph?
13. What is the time complexity of BFS using an adjacency matrix?
14. Can two different BFS traversals exist for the same graph?
15. How would you use BFS to find all vertices within distance K from a starting vertex?

## 16. Quick Revision

| Concept | Remember |
|---|---|
| BFS | Breadth-First Search |
| Traversal | Level by level |
| Data structure | Queue |
| Queue operation | FIFO |
| Python queue | `collections.deque` |
| Add element | `append()` |
| Remove front | `popleft()` |
| Visited tracking | Set |
| Shortest path | Minimum edges in unweighted graphs |
| Time complexity | O(V + E), adjacency list |
| Space complexity | O(V) |

## 17. Self-Assessment

You should be able to answer these questions before moving forward:

- What is BFS?
- Why does BFS use a queue?
- How does a visited set prevent repeated traversal?
- How do you implement BFS in Python?
- How can BFS find the shortest path in an unweighted graph?
- How do you traverse disconnected graphs?
- What are the time and space complexities?
- When should you use BFS instead of DFS?

## 18. Learning Outcome

After completing this topic, you should be able to:

1. Explain Breadth-First Search.
2. Understand the role of a queue.
3. Implement BFS using Python.
4. Trace BFS execution manually.
5. Find shortest paths in unweighted graphs.
6. Count reachable vertices.
7. Traverse disconnected graphs.
8. Analyze BFS time and space complexity.

**Next recommended topic:** DFS – Implementation and Problem Solving.
