
# Graph Terminology – Directed, Undirected, Weighted and Unweighted

## 1. Introduction to Graphs

A Graph is a non-linear data structure consisting of:

1. Vertices (Nodes)
2. Edges (Connections)

A graph represents relationships or connections between different objects.

### Real-world example

Consider a social networking application.

- Each person represents a Vertex.
- A friendship between two people represents an Edge.

```text
       A -------- B
       |          |
       |          |
       C -------- D
```

Here:

- A, B, C and D are vertices.
- The connecting lines are edges.

### Graph representation

A graph is commonly represented as:

G = (V, E)

Where:

- G = Graph
- V = Set of Vertices
- E = Set of Edges

Example:

```python
V = ["A", "B", "C", "D"]

E = [
    ("A", "B"),
    ("A", "C"),
    ("B", "D"),
    ("C", "D")
]
```

The graph contains:

- 4 vertices
- 4 edges

---

## 2. Basic Graph Terminology

Before understanding graph types, learn these important terms.

### 2.1 Vertex (Node)

A Vertex is an individual element in a graph.

Example:

```text
A -------- B
```

A and B are vertices.

### 2.2 Edge

An Edge represents a connection between two vertices.

Example:

```text
A -------- B
```

The connection between A and B is an edge.

### 2.3 Adjacent Vertices

Two vertices are adjacent if an edge directly connects them.

Example:

```text
A -------- B -------- C
```

- A and B are adjacent.
- B and C are adjacent.
- A and C are not adjacent.

### 2.4 Degree of a Vertex

Degree represents the number of edges connected to a vertex in an undirected graph.

Example:

```text
          B
          |
      C---A---D
          |
          E
```

Degree of A = 4

Because four edges are connected to A.

Degree of B = 1

Because only one edge is connected to B.

**Important:** In a directed graph, we use two different terms:

- In-degree: Number of incoming edges.
- Out-degree: Number of outgoing edges.

### 2.5 Path

A Path is a sequence of vertices connected through edges.

Example:

```text
A -------- B -------- C -------- D
```

One possible path:

A → B → C → D

### 2.6 Cycle

A Cycle is a path that starts and ends at the same vertex, following at least one edge.

Example:

```text
       A -------- B
       |          |
       |          |
       D -------- C
```

Cycle:

A → B → C → D → A

### 2.7 Connected Graph

An undirected graph is connected if every vertex can be reached from every other vertex.

Example:

```text
A -------- B -------- C
           |
           D
```

All vertices are connected through some path.

### 2.8 Disconnected Graph

A graph is disconnected if at least one vertex cannot be reached from another vertex.

Example:

```text
A -------- B       C -------- D
```

There are two separate connected components.

### 2.9 Self-loop

A Self-loop is an edge that connects a vertex to itself.

Example:

```text
       ↻
       A
```

### 2.10 Parallel Edges

Parallel edges are two or more edges connecting the same pair of vertices.

Example:

```text
     Edge 1
A ========== B
A ---------- B
     Edge 2
```

Some graph models allow parallel edges, while simple graphs do not.

---

## 3. Types of Graphs

Graphs can be classified based on the direction and weight of their edges.

The four important types are:

1. Directed Graph
2. Undirected Graph
3. Weighted Graph
4. Unweighted Graph

---

## 4. Directed Graph

A Directed Graph is a graph in which edges have a specific direction.

It is also called a Digraph.

An edge from A to B does not automatically mean there is an edge from B to A.

### Example

```text
A --------> B
^           |
|           |
|           v
D <-------- C
```

Here:

- A → B
- B → C
- C → D
- D → A

The arrows indicate the direction of movement.

### Real-world example

Social media following system:

- A follows B.
- B does not necessarily follow A.

```text
Alice --------> Bob
```

This represents a one-way relationship.

### Python representation

```python
graph = {
    "A": ["B"],
    "B": ["C"],
    "C": ["D"],
    "D": ["A"]
}

print(graph["A"])
```

Output:

```text
['B']
```

This means A has an outgoing edge to B.

### Important points

- Every edge has a direction.
- Direction matters when traversing the graph.
- An edge A → B does not imply B → A.
- Directed graphs are useful for representing one-way relationships.

---

## 5. Undirected Graph

An Undirected Graph is a graph in which edges do not have a direction.

If A is connected to B, B is also connected to A.

### Example

```text
A -------- B
|          |
|          |
C -------- D
```

Here:

- A is connected to B.
- B is connected to A.
- A is connected to C.
- C is connected to A.

The relationship works in both directions.

### Real-world example

Friendship system:

If Alice and Bob are friends, the relationship is generally mutual.

```text
Alice -------- Bob
```

### Python representation

```python
graph = {
    "A": ["B", "C"],
    "B": ["A", "D"],
    "C": ["A", "D"],
    "D": ["B", "C"]
}

print(graph["A"])
```

Output:

```text
['B', 'C']
```

To represent an undirected edge in an adjacency list, both directions are stored.

For example:

```python
"A": ["B"]
"B": ["A"]
```

### Important points

- Edges have no direction.
- Connections work in both directions.
- Both vertices are considered adjacent.
- Useful for representing mutual relationships.

---

## 6. Directed Graph vs Undirected Graph

| Feature | Directed Graph | Undirected Graph |
|---|---|---|
| Edge direction | Has direction | No direction |
| Representation | A → B | A — B |
| Relationship | One-way possible | Mutual connection |
| Traversal | Must follow edge direction | Can travel either way |
| Example | Following system | Friendship system |

### Visual comparison

Directed:

```text
A --------> B
```

Undirected:

```text
A ---------- B
```

---

## 7. Weighted Graph

A Weighted Graph is a graph in which every edge has an associated numerical value called a Weight.

The weight may represent:

- Distance
- Cost
- Time
- Price
- Network latency

### Example

```text
       10
   A -------- B
    \        /
   20\      /15
      \    /
        C
```

Here:

- A to B = 10
- A to C = 20
- B to C = 15

These numbers represent edge weights.

### Real-world example

Google Maps or navigation systems:

- Cities represent vertices.
- Roads represent edges.
- Distance or travel time represents edge weights.

### Python representation

```python
graph = {
    "A": {"B": 10, "C": 20},
    "B": {"A": 10, "C": 15},
    "C": {"A": 20, "B": 15}
}

print(graph["A"]["B"])
```

Output:

```text
10
```

This means the weight of the edge between A and B is 10.

### Important points

- Every edge has an associated weight.
- Weights can represent cost, distance or time.
- The shortest or cheapest route can be calculated using suitable algorithms.
- Dijkstra's algorithm is commonly used for shortest paths with non-negative edge weights.

---

## 8. Unweighted Graph

An Unweighted Graph is a graph in which edges do not have associated numerical weights.

All edges are treated equally in terms of edge cost.

### Example

```text
A -------- B
|          |
|          |
C -------- D
```

There are no numerical values associated with the connections.

### Real-world example

A basic friendship network:

- A is connected to B.
- B is connected to C.
- C is connected to D.

The graph only represents relationships, not the cost or distance between people.

### Python representation

```python
graph = {
    "A": ["B", "C"],
    "B": ["A", "D"],
    "C": ["A", "D"],
    "D": ["B", "C"]
}

print(graph["A"])
```

Output:

```text
['B', 'C']
```

### Important points

- Edges do not have numerical weights.
- Every edge is treated equally.
- BFS can find the shortest path in terms of number of edges in an unweighted graph.

---

## 9. Weighted Graph vs Unweighted Graph

| Feature | Weighted Graph | Unweighted Graph |
|---|---|---|
| Edge values | Has weights | No weights |
| Edge cost | Can differ | Treated equally |
| Example | Road distances | Basic friendship network |
| Shortest path | Depends on edge weights | Minimum number of edges |
| Common algorithm | Dijkstra's algorithm | BFS |

---

## 10. Graph Classification – Important Concept

Direction and weight are two independent properties.

A graph can be:

1. Directed and Weighted
2. Directed and Unweighted
3. Undirected and Weighted
4. Undirected and Unweighted

### 10.1 Directed and Weighted

```text
A ----10----> B
```

The edge has both direction and weight.

Example: One-way road with a distance or travel cost.

### 10.2 Directed and Unweighted

```text
A --------> B
```

The edge has direction but no numerical weight.

Example: A follows B on social media.

### 10.3 Undirected and Weighted

```text
A ----10---- B
```

The edge has a weight but no direction.

Example: A two-way road with a distance of 10 km.

### 10.4 Undirected and Unweighted

```text
A -------- B
```

The edge has neither direction nor weight.

Example: Mutual friendship.

---

## 11. Important Graph Terminology

### In-degree

The number of incoming edges to a vertex.

Example:

```text
A ------> C
B ------> C
D ------> C
```

In-degree of C = 3.

### Out-degree

The number of outgoing edges from a vertex.

Example:

```text
C ------> A
C ------> B
C ------> D
```

Out-degree of C = 3.

### Source Vertex

A vertex with in-degree 0.

It has no incoming edges.

### Sink Vertex

A vertex with out-degree 0.

It has no outgoing edges.

### Simple Graph

A graph with:

- No self-loops.
- No parallel edges.

### Complete Graph

A simple undirected graph in which every pair of distinct vertices has an edge connecting them.

For n vertices, the number of edges is:

n(n - 1) / 2

Example:

```text
       A
      / \
     /   \
    B-----C
```

This is a complete graph with 3 vertices and 3 edges.

---

## 12. Graph Representation

There are two common ways to represent graphs in programming.

1. Adjacency Matrix
2. Adjacency List

### 12.1 Adjacency Matrix

An Adjacency Matrix is a two-dimensional array used to represent connections between vertices.

Example graph:

```text
A -------- B
|          
|
C
```

Vertices:

A, B, C

Matrix:

```text
    A  B  C

A   0  1  1
B   1  0  0
C   1  0  0
```

Explanation:

- 1 means an edge exists.
- 0 means no edge exists.

Python implementation:

```python
vertices = ["A", "B", "C"]

matrix = [
    [0, 1, 1],
    [1, 0, 0],
    [1, 0, 0]
]

print(matrix[0][1])
```

Output:

```text
1
```

This means A is connected to B.

For a weighted graph, matrix entries can store weights instead of 1.

### 12.2 Adjacency List

An Adjacency List stores each vertex along with its neighboring vertices.

Example:

```text
A -------- B
|
|
C
```

Python representation:

```python
graph = {
    "A": ["B", "C"],
    "B": ["A"],
    "C": ["A"]
}

print(graph["A"])
```

Output:

```text
['B', 'C']
```

This means A is connected to B and C.

### Adjacency Matrix vs Adjacency List

| Feature | Adjacency Matrix | Adjacency List |
|---|---|---|
| Storage | 2D array | Dictionary or list |
| Space | O(V²) | O(V + E) |
| Check edge | O(1) | O(degree of vertex) |
| Best suited for | Dense graphs | Sparse graphs |
| Neighbor traversal | O(V) | O(degree of vertex) |

Where:

- V = Number of vertices.
- E = Number of edges.

---

## 13. Real-World Applications of Graphs

### 1. Social Networking

- Users represent vertices.
- Friendships or follows represent edges.

### 2. Google Maps

- Locations represent vertices.
- Roads represent edges.
- Distance or travel time represents weights.

### 3. Computer Networks

- Computers and routers represent vertices.
- Network connections represent edges.
- Latency or bandwidth can be represented using weights.

### 4. Recommendation Systems

- Users and products can be represented as vertices.
- Interactions represent edges.

### 5. Web Search Engines

- Web pages represent vertices.
- Hyperlinks represent directed edges.

### 6. AI and Workflow Automation

- Tasks represent vertices.
- Dependencies represent directed edges.

Example:

```text
Collect Data
     |
     v
Clean Data
     |
     v
Generate Embeddings
     |
     v
Create Vector Index
     |
     v
Run RAG Query
```

This represents a workflow where one task depends on another.

---

## 14. Graphs in Forward-Deployed Engineering

Graphs are especially useful when building systems that involve relationships and dependencies.

### Example: AI Document Processing Workflow

Imagine an AI application that processes documents.

```text
Upload Document
       |
       v
Extract Text
       |
       v
Validate Content
       |
       v
Generate Embeddings
       |
       v
Store in Vector Database
       |
       v
Answer User Query
```

Each step represents a vertex.

The dependency between steps represents a directed edge.

If the system allows multiple independent processing tasks, the graph can branch:

```text
             Upload
                |
                v
          Extract Text
                |
          -------------
          |           |
          v           v
       Validate    Detect Type
          |           |
          -------------
                |
                v
          Generate Output
```

Understanding graphs helps when designing:

- Workflow orchestration systems.
- Task dependency management.
- AI pipelines.
- Service dependency maps.
- Distributed systems.

---

## 15. Common Mistakes

1. Confusing vertices with edges.
2. Assuming directed edges work in both directions.
3. Assuming every graph must have weights.
4. Confusing degree with in-degree and out-degree.
5. Assuming every graph is connected.
6. Confusing a path with a cycle.
7. Assuming a weighted graph must always be directed.
8. Assuming a graph must be a tree.

Important:

A tree is a special type of connected, acyclic, undirected graph.

But not every graph is a tree.

---

## 16. Practice Exercises

### Beginner Level

1. What is a Graph?
2. Define Vertex and Edge.
3. What is the difference between directed and undirected graphs?
4. What is a weighted graph?
5. What is the degree of a vertex?
6. What is a self-loop?

### Intermediate Level

7. Differentiate between in-degree and out-degree.
8. What is the difference between a connected and disconnected graph?
9. Explain the difference between a path and a cycle.
10. Represent a directed graph using a Python dictionary.
11. Represent an undirected graph using an adjacency list.
12. Explain adjacency matrix and adjacency list.

### Advanced Level

13. Why is an adjacency list more space-efficient for sparse graphs?
14. Can a graph be both directed and weighted? Explain with an example.
15. How many edges exist in a complete undirected graph with 5 vertices?
16. Explain how graphs represent AI workflow dependencies.
17. What is the difference between a tree and a general graph?

---

## 17. Quick Revision

| Term | Meaning |
|---|---|
| Graph | Collection of vertices and edges |
| Vertex | Individual node |
| Edge | Connection between vertices |
| Directed Graph | Edges have direction |
| Undirected Graph | Edges have no direction |
| Weighted Graph | Edges have numerical weights |
| Unweighted Graph | Edges have no numerical weights |
| Degree | Number of connected edges in an undirected graph |
| In-degree | Number of incoming edges |
| Out-degree | Number of outgoing edges |
| Path | Sequence of connected vertices |
| Cycle | Path that returns to its starting vertex |
| Connected Graph | Every vertex is reachable from every other vertex |
| Self-loop | Edge connecting a vertex to itself |
| Adjacency Matrix | Graph represented using a 2D array |
| Adjacency List | Graph represented using neighboring vertices |

---

## 18. Learning Outcome

After completing this chapter, you should be able to:

- Explain graph data structures.
- Understand vertices and edges.
- Differentiate directed and undirected graphs.
- Differentiate weighted and unweighted graphs.
- Understand degree, in-degree and out-degree.
- Identify paths and cycles.
- Understand connected and disconnected graphs.
- Represent graphs using adjacency matrices and adjacency lists.
- Identify real-world graph applications.

## Next Recommended Topic

**Graph Representation – Adjacency Matrix and Adjacency List in Python**
