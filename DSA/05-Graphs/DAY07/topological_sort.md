
# Topological Sort

## 1. Introduction to Topological Sort

Topological Sorting is a linear ordering of vertices in a Directed Acyclic Graph (DAG).

A DAG is a Directed Graph that does not contain any cycles.

In topological ordering, if there is an edge:

```text
A → B
```

Then A must appear before B in the ordering.

### Real-world analogy

Imagine preparing for a software development project.

Before deploying an application:

1. Write the code.
2. Test the application.
3. Build the application.
4. Deploy the application.

You cannot deploy the application before building and testing it.

These relationships are called dependencies.

Topological Sort helps arrange tasks in a valid execution order.

## 2. Understanding DAG

DAG stands for:

- Directed: Edges have a direction.
- Acyclic: The graph does not contain a cycle.
- Graph: A collection of vertices and edges.

Example:

```text
A → B → D
|
v
C → D
```

Possible topological ordering:

```text
A → B → C → D
```

Another valid ordering:

```text
A → C → B → D
```

Both are correct.

Why?

- A comes before B.
- A comes before C.
- B comes before D.
- C comes before D.

Topological sorting does not always produce one unique answer.

## 3. Important Conditions

Topological Sort is possible only for a Directed Acyclic Graph (DAG).

### Condition 1: Directed Graph

Every edge must have a direction.

```text
A → B
```

### Condition 2: No Cycles

Consider:

```text
A → B → C → A
```

This graph contains a cycle.

A must come before B.

B must come before C.

C must come before A.

These dependencies create a contradiction.

Therefore, a valid topological ordering does not exist.

### Remember

| Graph Type | Topological Sort |
|---|---|
| Directed Acyclic Graph | Possible |
| Directed Cyclic Graph | Not possible |
| Undirected Graph | Not defined as standard topological sorting |

## 4. Understanding In-Degree

Before learning the algorithm, understand in-degree.

In-degree means the number of incoming edges to a vertex.

Example:

```text
A → C
B → C
C → D
```

In-degree:

| Vertex | In-Degree |
|---|---:|
| A | 0 |
| B | 0 |
| C | 2 |
| D | 1 |

Explanation:

- A has no incoming edges.
- B has no incoming edges.
- C has incoming edges from A and B.
- D has an incoming edge from C.

### Important concept

A vertex with in-degree 0 has no remaining prerequisites.

It can be processed first.

This is the main idea behind Kahn's Algorithm.

## 5. Topological Sort Using Kahn's Algorithm (BFS Approach)

Kahn's Algorithm uses:

- In-degree
- Queue
- BFS-style processing

### Algorithm steps

1. Calculate the in-degree of every vertex.
2. Find all vertices with in-degree 0.
3. Add them to a queue.
4. Remove a vertex from the queue.
5. Add that vertex to the topological ordering.
6. For each outgoing neighbor:
   - Decrease its in-degree by 1.
   - If its in-degree becomes 0, add it to the queue.
7. Repeat until the queue becomes empty.
8. If the number of processed vertices is less than the total number of vertices, the graph contains a cycle.

## 6. Kahn's Algorithm – Visual Dry Run

Consider:

```text
A → C → D
B → C
B → E
```

### Step 1: Calculate in-degree

| Vertex | In-Degree |
|---|---:|
| A | 0 |
| B | 0 |
| C | 2 |
| D | 1 |
| E | 1 |

Initial queue:

```text
[A, B]
```

### Step 2: Process A

Remove A from the queue.

Add A to the result.

A → C

Decrease C's in-degree:

```text
C: 2 → 1
```

Queue:

```text
[B]
```

Result:

```text
[A]
```

### Step 3: Process B

Remove B.

Add B to the result.

B → C

Decrease C's in-degree:

```text
C: 1 → 0
```

C is now ready, so add it to the queue.

B → E

Decrease E's in-degree:

```text
E: 1 → 0
```

Add E to the queue.

Queue:

```text
[C, E]
```

Result:

```text
[A, B]
```

### Step 4: Process C

Remove C.

Add C to the result.

C → D

Decrease D's in-degree:

```text
D: 1 → 0
```

Add D to the queue.

Queue:

```text
[E, D]
```

Result:

```text
[A, B, C]
```

### Step 5: Process E

Remove E.

Add E to the result.

E has no outgoing edges.

Queue:

```text
[D]
```

Result:

```text
[A, B, C, E]
```

### Step 6: Process D

Remove D.

Add D to the result.

Queue:

```text
Empty
```

Final result:

```text
A → B → C → E → D
```

This is one valid topological ordering.

## 7. Kahn's Algorithm – Python Implementation

### Complete code

```python
from collections import deque

def topological_sort(graph):

    indegree = {vertex: 0 for vertex in graph}

    # Calculate in-degree
    for vertex in graph:

        for neighbor in graph[vertex]:

            indegree[neighbor] += 1

    # Add vertices with in-degree 0
    queue = deque()

    for vertex in indegree:

        if indegree[vertex] == 0:

            queue.append(vertex)

    result = []

    # Process vertices
    while queue:

        current = queue.popleft()

        result.append(current)

        for neighbor in graph[current]:

            indegree[neighbor] -= 1

            if indegree[neighbor] == 0:

                queue.append(neighbor)

    # Cycle detection
    if len(result) != len(graph):

        return None

    return result


graph = {
    "A": ["C"],
    "B": ["C", "E"],
    "C": ["D"],
    "D": [],
    "E": []
}

result = topological_sort(graph)

print(result)
```

### Output

```text
['A', 'B', 'C', 'E', 'D']
```

Note: This output depends on the order in which vertices and neighbors are processed. Other valid topological orders may exist.

## 8. Understanding the Python Code

### Step 1: Initialize in-degree

```python
indegree = {vertex: 0 for vertex in graph}
```

Creates a dictionary where every vertex starts with an in-degree of zero.

Example:

```python
{
    "A": 0,
    "B": 0,
    "C": 0,
    "D": 0,
    "E": 0
}
```

### Step 2: Calculate incoming edges

```python
for vertex in graph:

    for neighbor in graph[vertex]:

        indegree[neighbor] += 1
```

Every outgoing edge from a vertex increases the in-degree of its destination.

For example:

```text
A → C
B → C
```

C receives two incoming edges.

Therefore:

```python
indegree["C"] = 2
```

### Step 3: Initialize the queue

```python
queue = deque()
```

Creates an empty queue.

### Step 4: Add zero in-degree vertices

```python
if indegree[vertex] == 0:

    queue.append(vertex)
```

These vertices have no prerequisites remaining.

### Step 5: Process the queue

```python
current = queue.popleft()
```

Removes the next available vertex.

### Step 6: Reduce in-degree

```python
indegree[neighbor] -= 1
```

One prerequisite has now been processed.

Therefore, the neighbor's in-degree decreases by one.

### Step 7: Add newly available vertices

```python
if indegree[neighbor] == 0:

    queue.append(neighbor)
```

If no prerequisites remain, the vertex is ready to be processed.

### Step 8: Detect cycles

```python
if len(result) != len(graph):

    return None
```

If some vertices were not processed, the graph contains a cycle.

Why?

A cycle prevents its vertices from becoming available through the zero-in-degree process.

## 9. Topological Sort Using DFS

Topological sorting can also be implemented using Depth-First Search.

The main idea:

1. Start DFS from an unvisited vertex.
2. Explore all its unvisited neighbors.
3. After exploring all neighbors, add the current vertex to a stack.
4. Repeat for all unvisited vertices.
5. Reverse the stack to obtain the topological ordering.

### Why add a vertex after exploring its neighbors?

Suppose:

```text
A → B → C
```

DFS explores:

A → B → C

C has no outgoing neighbors.

So push C first.

Then push B.

Then push A.

Stack insertion order:

```text
C, B, A
```

After reversing:

```text
A, B, C
```

This respects the dependency order.

## 10. DFS-Based Topological Sort – Python Implementation

```python
def topological_sort_dfs(graph):

    visited = set()

    visiting = set()

    stack = []

    def dfs(current):

        if current in visiting:

            raise ValueError("Cycle detected")

        if current in visited:

            return

        visiting.add(current)

        for neighbor in graph[current]:

            dfs(neighbor)

        visiting.remove(current)

        visited.add(current)

        stack.append(current)

    for vertex in graph:

        if vertex not in visited:

            dfs(vertex)

    return stack[::-1]


graph = {
    "A": ["C"],
    "B": ["C", "E"],
    "C": ["D"],
    "D": [],
    "E": []
}

result = topological_sort_dfs(graph)

print(result)
```

### Output

```text
['B', 'E', 'A', 'C', 'D']
```

This is another valid topological ordering.

### Understanding the important variables

```python
visited = set()
```

Tracks vertices whose DFS processing is complete.

```python
visiting = set()
```

Tracks vertices currently in the active recursion path.

Why do we need both?

If DFS reaches a vertex already in `visiting`, it has found a back edge to an ancestor in the current path.

That means a directed cycle exists.

```python
stack.append(current)
```

Adds a vertex only after all its outgoing neighbors have been processed.

```python
return stack[::-1]
```

Reverses the finishing order to obtain the topological ordering.

## 11. Kahn's Algorithm vs DFS-Based Topological Sort

| Feature | Kahn's Algorithm | DFS Approach |
|---|---|---|
| Main technique | BFS-style processing | Depth-First Search |
| Data structure | Queue | Recursion stack and result stack |
| Uses in-degree | Yes | No |
| Cycle detection | Processed count | Visiting set |
| Time complexity | O(V + E) | O(V + E) |
| Auxiliary space | O(V) | O(V) |
| Implementation | Iterative | Commonly recursive |

Both algorithms produce a valid topological ordering if the graph is a DAG.

## 12. Problem Solving Using Topological Sort

### Problem 1: Course Schedule

Suppose a student needs to complete these courses:

```text
Programming → Data Structures
Data Structures → Algorithms
Mathematics → Algorithms
```

Interpretation:

- Programming must be completed before Data Structures.
- Data Structures must be completed before Algorithms.
- Mathematics must be completed before Algorithms.

Question:

Can all courses be completed?

Yes, because the graph has no cycle.

One valid ordering:

```text
Programming
Mathematics
Data Structures
Algorithms
```

This is a common interview problem.

### Python implementation

```python
from collections import deque

def can_finish_courses(num_courses, prerequisites):

    graph = {
        course: [] for course in range(num_courses)
    }

    indegree = [0] * num_courses

    for course, prerequisite in prerequisites:

        graph[prerequisite].append(course)

        indegree[course] += 1

    queue = deque()

    for course in range(num_courses):

        if indegree[course] == 0:

            queue.append(course)

    completed = 0

    while queue:

        current = queue.popleft()

        completed += 1

        for neighbor in graph[current]:

            indegree[neighbor] -= 1

            if indegree[neighbor] == 0:

                queue.append(neighbor)

    return completed == num_courses


num_courses = 4

prerequisites = [
    [1, 0],
    [2, 1],
    [3, 2]
]

print(can_finish_courses(num_courses, prerequisites))
```

### Output

```text
True
```

Explanation:

The prerequisite pairs are:

```text
[1, 0] means course 0 before course 1
[2, 1] means course 1 before course 2
[3, 2] means course 2 before course 3
```

All four courses can be completed.

If a cycle exists, not all courses can be completed.

## 13. Problem 2: Detect a Cycle Using Kahn's Algorithm

Consider:

```text
A → B → C → A
```

In-degree:

| Vertex | In-Degree |
|---|---:|
| A | 1 |
| B | 1 |
| C | 1 |

There is no vertex with in-degree zero.

Therefore, the queue is empty from the beginning.

No vertex can be processed.

Result:

```text
Cycle detected
```

### Python example

```python
graph = {
    "A": ["B"],
    "B": ["C"],
    "C": ["A"]
}

result = topological_sort(graph)

if result is None:

    print("Cycle detected")

else:

    print(result)
```

### Output

```text
Cycle detected
```

## 14. Time and Space Complexity

Let:

- V = Number of vertices.
- E = Number of directed edges.

| Operation | Complexity |
|---|---|
| Initialize in-degree | O(V) |
| Calculate in-degree | O(E) |
| Queue processing | O(V) |
| Process outgoing edges | O(E) |
| Total time | O(V + E) |
| Auxiliary space | O(V) |

### Why O(V + E)?

Each vertex enters and leaves the queue at most once.

Each directed edge is examined once when processing its source vertex.

Therefore:

Time Complexity = O(V + E)

Space Complexity = O(V)

The DFS-based implementation also takes O(V + E) time and O(V) auxiliary space.

Its recursive call stack can grow to O(V) in the worst case.

## 15. Real-World Applications

1. Task scheduling
   - Execute tasks after their prerequisites.

2. Package management
   - Install required dependencies before installing a package.

3. Build systems
   - Compile source files in dependency order.

4. Course scheduling
   - Complete prerequisite courses first.

5. Workflow automation
   - Execute workflow stages in a valid order.

6. Data pipelines
   - Run data transformation steps after their required inputs are ready.

### FDE Connection

Imagine an AI document-processing pipeline:

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
  Clean  Review
     \   /
      v v
     Store
       |
       v
  Generate Report
```

Some tasks depend on other tasks.

For example:

- Text extraction depends on document upload.
- Validation depends on text extraction.
- Storage depends on the required cleaning and review tasks.
- Report generation depends on storage.

Topological Sort can determine a valid order for executing these dependent tasks.

In a real workflow engine, execution also needs to handle failures, retries, conditional branches, and task status.

## 16. Common Mistakes

### Mistake 1: Applying Topological Sort to a cyclic graph

Topological ordering is only possible for DAGs.

### Mistake 2: Confusing in-degree with out-degree

In-degree = Incoming edges.

Out-degree = Outgoing edges.

Kahn's Algorithm uses in-degree.

### Mistake 3: Assuming there is only one valid ordering

A DAG can have multiple valid topological orders.

### Mistake 4: Forgetting to update in-degree

Every time a vertex is processed, decrease the in-degree of each outgoing neighbor.

### Mistake 5: Confusing BFS with Topological Sort

Kahn's Algorithm uses a queue like BFS, but it is not ordinary BFS.

It processes vertices based on their remaining incoming dependencies.

### Mistake 6: Ignoring cycle detection

If the processed vertex count is smaller than the total vertex count, a cycle exists.

### Mistake 7: Confusing DFS visited and visiting

- visited: DFS processing is complete.
- visiting: Vertex is currently in the recursion path.

Both are useful for detecting directed cycles.

## 17. Practice Exercises

### Beginner

1. Define Topological Sort.
2. What is a DAG?
3. What is in-degree?
4. Why does Kahn's Algorithm use a queue?
5. Can an undirected graph have a standard topological ordering?

### Intermediate

6. Find a topological ordering for:

```text
A → C
B → C
C → D
D → E
```

7. Implement Kahn's Algorithm in Python.
8. Implement DFS-based Topological Sort.
9. Detect a cycle using Kahn's Algorithm.
10. Explain why a graph with a cycle cannot have a topological ordering.

### Interview-Level Thinking

11. Can a DAG have more than one topological ordering?
12. What happens if no vertex has in-degree zero?
13. What is the difference between BFS and Kahn's Algorithm?
14. How does DFS detect a cycle in a directed graph?
15. How would you schedule multiple independent tasks at the same time?

## 18. Quick Revision

| Concept | Remember |
|---|---|
| Topological Sort | Dependency-based ordering |
| Required graph | Directed Acyclic Graph |
| DAG | Directed graph without cycles |
| In-degree | Number of incoming edges |
| Kahn's Algorithm | Queue + In-degree |
| DFS approach | Recursion + Stack |
| Cycle detection | Processed count or visiting set |
| Time complexity | O(V + E) |
| Space complexity | O(V) |
| Applications | Scheduling, dependencies, build systems |

## 19. Self-Assessment

You should be able to answer these questions before moving forward:

- What is Topological Sort?
- Why must the graph be a DAG?
- What is in-degree?
- How does Kahn's Algorithm work?
- How does DFS-based Topological Sort work?
- What is the difference between the two approaches?
- How can we detect cycles?
- Can multiple valid topological orderings exist?
- What are the time and space complexities?
- How is Topological Sort useful in workflow automation?

## 20. Learning Outcome

After completing this topic, you should be able to:

1. Understand Directed Acyclic Graphs.
2. Understand in-degree and dependency relationships.
3. Implement Kahn's Algorithm.
4. Implement DFS-based Topological Sort.
5. Detect cycles in directed graphs.
6. Solve course scheduling problems.
7. Analyze time and space complexity.
8. Apply topological ordering to real-world workflows.

**Next recommended topic:** Dijkstra's Algorithm – Shortest Path in Weighted Graphs.
