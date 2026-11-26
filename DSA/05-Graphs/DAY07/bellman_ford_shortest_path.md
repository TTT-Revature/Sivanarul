
# Shortest Path – Bellman-Ford Algorithm

## 1. Introduction to Bellman-Ford

Bellman-Ford is a graph algorithm used to find the shortest paths from one starting vertex to all other vertices.

It supports:

- Directed weighted graphs.
- Undirected weighted graphs.
- Positive edge weights.
- Zero edge weights.
- Negative edge weights.

It can also detect negative-weight cycles that are reachable from the source.

### Real-world analogy

Imagine a financial transaction network.

Different transactions may have different costs or adjustments.

Some transactions may even provide discounts or credits, represented by negative values.

You need to calculate the minimum total cost from one starting point.

Bellman-Ford can handle negative edge weights while calculating shortest paths.

## 2. Understanding Negative Edge Weights

In a weighted graph, every edge has a numerical value.

Usually, these values are positive.

Example:

```text
A → B = 5
B → C = 3
```

But sometimes an edge can have a negative weight.

Example:

```text
A → B = 4
B → C = -6
A → C = 2
```

Let's calculate the possible paths from A to C.

Path 1:

```text
A → C

Distance = 2
```

Path 2:

```text
A → B → C

Distance = 4 + (-6)

Distance = -2
```

The shortest path is:

```text
A → B → C

Minimum distance = -2
```

Bellman-Ford can correctly calculate this shortest distance.

## 3. Why Do We Need Bellman-Ford?

Dijkstra's Algorithm uses a greedy approach.

It selects the vertex with the smallest known distance and considers it finalized.

This works when all edge weights are non-negative.

However, negative edge weights can create a shorter path later, even after a vertex has been processed.

Bellman-Ford takes a different approach.

Instead of selecting the closest vertex, it repeatedly checks every edge and updates distances whenever a shorter path is found.

This process is called **edge relaxation**.

## 4. Understanding Edge Relaxation

Relaxation means checking whether a new route provides a shorter distance.

Formula:

```text
new_distance = distance[u] + weight(u, v)
```

If:

```text
new_distance < distance[v]
```

Update:

```text
distance[v] = new_distance
```

Here:

- u = Starting vertex of an edge.
- v = Destination vertex.
- weight(u, v) = Weight of the edge.
- distance[u] = Current shortest known distance to u.

### Example

Suppose:

```text
A → B = 4
B → C = -3
```

Initially:

```text
Distance[A] = 0
Distance[B] = ∞
Distance[C] = ∞
```

Relax edge A → B:

```text
0 + 4 = 4
```

Update:

```text
Distance[B] = 4
```

Relax edge B → C:

```text
4 + (-3) = 1
```

Update:

```text
Distance[C] = 1
```

Final distances:

| Vertex | Distance from A |
|---|---:|
| A | 0 |
| B | 4 |
| C | 1 |

## 5. Why Does Bellman-Ford Repeat V - 1 Times?

This is the most important concept in Bellman-Ford.

Suppose a graph contains V vertices.

A shortest path without cycles can contain at most:

```text
V - 1 edges
```

Why?

A path containing V vertices can connect them using V - 1 edges.

For example:

```text
A → B → C → D
```

Number of vertices = 4

Number of edges = 3

Therefore:

```text
V - 1 = 4 - 1 = 3
```

If a shortest path contains a cycle with non-negative total weight, removing that cycle cannot make the path longer.

If a reachable negative-weight cycle exists, a finite shortest path may not exist.

Therefore, in a graph without reachable negative-weight cycles, V - 1 relaxation rounds are sufficient to find all shortest distances.

## 6. Bellman-Ford Algorithm – Step by Step

The algorithm follows these steps:

1. Select a source vertex.
2. Initialize all distances to infinity.
3. Set the source distance to zero.
4. Repeat the following process V - 1 times:
   - Visit every edge.
   - Calculate the new distance.
   - If the new distance is smaller, update it.
5. After V - 1 rounds, perform one additional pass over all edges.
6. If any distance can still be reduced, a reachable negative-weight cycle exists.

### Pseudocode

```text
BELLMAN_FORD(vertices, edges, source):

    initialize all distances to infinity

    distance[source] = 0

    repeat V - 1 times:

        for each edge (u, v, weight):

            if distance[u] is not infinity:

                new_distance = distance[u] + weight

                if new_distance < distance[v]:

                    distance[v] = new_distance

    check every edge again:

        if distance[u] + weight < distance[v]:

            negative cycle detected

    return distances
```

## 7. Bellman-Ford – Visual Dry Run

Consider this directed weighted graph:

```text
       4
  A ------> B
  |          |
  | 5        | -3
  |          |
  v          v
  C <------ D
       2
```

Edges:

```text
A → B = 4
A → C = 5
B → D = -3
D → C = 2
```

Number of vertices:

```text
V = 4
```

Required relaxation rounds:

```text
V - 1 = 3
```

Source:

```text
A
```

### Step 1: Initialize distances

| Vertex | Distance |
|---|---:|
| A | 0 |
| B | ∞ |
| C | ∞ |
| D | ∞ |

### Step 2: First relaxation round

Process A → B:

```text
0 + 4 = 4
```

Update B = 4.

Process A → C:

```text
0 + 5 = 5
```

Update C = 5.

Process B → D:

```text
4 + (-3) = 1
```

Update D = 1.

Process D → C:

```text
1 + 2 = 3
```

Current distance to C = 5.

Since 3 is smaller, update C = 3.

After round 1:

| Vertex | Distance |
|---|---:|
| A | 0 |
| B | 4 |
| C | 3 |
| D | 1 |

### Step 3: Second relaxation round

Check every edge again.

A → B:

```text
0 + 4 = 4
```

No change.

A → C:

```text
0 + 5 = 5
```

No change.

B → D:

```text
4 + (-3) = 1
```

No change.

D → C:

```text
1 + 2 = 3
```

No change.

After round 2:

| Vertex | Distance |
|---|---:|
| A | 0 |
| B | 4 |
| C | 3 |
| D | 1 |

### Step 4: Third relaxation round

Check every edge again.

No distances change.

After round 3:

| Vertex | Distance |
|---|---:|
| A | 0 |
| B | 4 |
| C | 3 |
| D | 1 |

### Final shortest distances

| Vertex | Shortest Distance |
|---|---:|
| A | 0 |
| B | 4 |
| C | 3 |
| D | 1 |

Shortest path from A to C:

```text
A → B → D → C

Distance = 4 + (-3) + 2

Distance = 3
```

## 8. Bellman-Ford Implementation Using Python

We can represent a graph using an edge list.

Each edge contains:

```text
(source, destination, weight)
```

### Graph representation

```python
edges = [
    ("A", "B", 4),
    ("A", "C", 5),
    ("B", "D", -3),
    ("D", "C", 2)
]
```

### Complete implementation

```python
def bellman_ford(vertices, edges, start):

    distances = {
        vertex: float("inf")
        for vertex in vertices
    }

    distances[start] = 0

    # Relax all edges V - 1 times
    for _ in range(len(vertices) - 1):

        updated = False

        for u, v, weight in edges:

            if distances[u] == float("inf"):
                continue

            new_distance = distances[u] + weight

            if new_distance < distances[v]:

                distances[v] = new_distance

                updated = True

        # Early stopping
        if not updated:
            break

    # Negative cycle detection
    for u, v, weight in edges:

        if distances[u] == float("inf"):
            continue

        if distances[u] + weight < distances[v]:

            return None

    return distances


vertices = ["A", "B", "C", "D"]

edges = [
    ("A", "B", 4),
    ("A", "C", 5),
    ("B", "D", -3),
    ("D", "C", 2)
]

result = bellman_ford(vertices, edges, "A")

print(result)
```

### Output

```text
{'A': 0, 'B': 4, 'C': 3, 'D': 1}
```

Note: The `updated` variable is an optimization. If no distance changes during a round, further rounds are unnecessary.

## 9. Understanding the Python Code

### Step 1: Initialize distances

```python
distances = {
    vertex: float("inf")
    for vertex in vertices
}
```

Every vertex starts with infinity.

### Step 2: Set source distance

```python
distances[start] = 0
```

The distance from the source to itself is zero.

### Step 3: Repeat V - 1 times

```python
for _ in range(len(vertices) - 1):
```

Repeats the relaxation process V - 1 times.

The underscore means we do not need the loop counter.

### Step 4: Process every edge

```python
for u, v, weight in edges:
```

Extracts:

- u: Source vertex.
- v: Destination vertex.
- weight: Edge weight.

### Step 5: Check reachability

```python
if distances[u] == float("inf"):
    continue
```

If u is unreachable from the source, we cannot use it to improve v.

This also prevents calculations involving infinity from being treated as meaningful paths.

### Step 6: Calculate new distance

```python
new_distance = distances[u] + weight
```

Adds the current known distance and edge weight.

### Step 7: Update distance

```python
if new_distance < distances[v]:

    distances[v] = new_distance
```

Updates the destination if a shorter path is discovered.

### Step 8: Early stopping

```python
if not updated:
    break
```

If no distance changed in a complete round, the shortest distances have already been found.

### Step 9: Negative cycle detection

```python
if distances[u] + weight < distances[v]:
```

Checks whether any edge can still reduce a distance.

If it can, a negative-weight cycle reachable from the source exists.

## 10. Negative-Weight Cycle Detection

A negative-weight cycle is a cycle whose total edge weight is negative.

Example:

```text
A → B = 2
B → C = -5
C → A = 1
```

Total cycle weight:

```text
2 + (-5) + 1 = -2
```

The cycle has a negative total weight.

### Why is this a problem?

Imagine travelling around this cycle repeatedly.

Every time you complete the cycle, the total cost decreases by 2.

```text
First round  = -2
Second round = -4
Third round  = -6
Fourth round = -8
```

The distance can keep decreasing indefinitely.

Therefore, a finite shortest path does not exist for vertices that can be reached by repeatedly exploiting this cycle.

### Python example

```python
vertices = ["A", "B", "C"]

edges = [
    ("A", "B", 2),
    ("B", "C", -5),
    ("C", "A", 1)
]

result = bellman_ford(vertices, edges, "A")

if result is None:

    print("Negative-weight cycle detected")

else:

    print(result)
```

### Output

```text
Negative-weight cycle detected
```

Important:

Bellman-Ford detects negative-weight cycles reachable from the chosen source.

A negative cycle in a disconnected part of the graph will not be detected by a single-source run from an unrelated source.

## 11. Finding the Actual Shortest Path

The previous implementation returns distances.

Sometimes we also need the actual path.

For this, we maintain a parent dictionary.

### Python implementation

```python
def bellman_ford_path(vertices, edges, start, target):

    distances = {
        vertex: float("inf")
        for vertex in vertices
    }

    parent = {
        vertex: None
        for vertex in vertices
    }

    distances[start] = 0

    for _ in range(len(vertices) - 1):

        updated = False

        for u, v, weight in edges:

            if distances[u] == float("inf"):
                continue

            new_distance = distances[u] + weight

            if new_distance < distances[v]:

                distances[v] = new_distance

                parent[v] = u

                updated = True

        if not updated:
            break

    # Detect reachable negative cycle
    for u, v, weight in edges:

        if distances[u] == float("inf"):
            continue

        if distances[u] + weight < distances[v]:

            return None, None

    if distances[target] == float("inf"):

        return None, float("inf")

    path = []

    current = target

    while current is not None:

        path.append(current)

        current = parent[current]

    path.reverse()

    return path, distances[target]


vertices = ["A", "B", "C", "D"]

edges = [
    ("A", "B", 4),
    ("A", "C", 5),
    ("B", "D", -3),
    ("D", "C", 2)
]

path, distance = bellman_ford_path(
    vertices, edges, "A", "C"
)

print("Shortest path:", path)
print("Shortest distance:", distance)
```

### Output

```text
Shortest path: ['A', 'B', 'D', 'C']
Shortest distance: 3
```

### Understanding the parent dictionary

```python
parent[v] = u
```

Stores the previous vertex on the currently best-known path.

Example:

```python
{
    "A": None,
    "B": "A",
    "C": "D",
    "D": "B"
}
```

To reconstruct the path:

1. Start from C.
2. Find its parent D.
3. Find D's parent B.
4. Find B's parent A.
5. Stop at None.
6. Reverse the collected path.

Final path:

```text
A → B → D → C
```

## 12. Dijkstra vs Bellman-Ford

Both algorithms solve the single-source shortest-path problem, but they work differently.

| Feature | Dijkstra | Bellman-Ford |
|---|---|---|
| Approach | Greedy | Repeated edge relaxation |
| Graph | Weighted | Weighted |
| Negative weights | Not supported | Supported |
| Negative cycle detection | No | Yes |
| Main data structure | Min-heap | Edge list |
| Relaxation | As vertices are processed | Every edge, repeatedly |
| Time complexity | O((V + E) log V) with binary heap | O(V × E) |
| Typical performance | Faster | Slower |

### When should you use each?

Use Dijkstra when:

- All edge weights are non-negative.
- Performance is important.
- You need shortest paths from one source.

Use Bellman-Ford when:

- Negative edge weights are possible.
- You need to detect reachable negative-weight cycles.
- A slower algorithm is acceptable.

## 13. BFS vs Dijkstra vs Bellman-Ford

| Feature | BFS | Dijkstra | Bellman-Ford |
|---|---|---|---|
| Graph | Unweighted | Weighted | Weighted |
| Negative weights | Not applicable to ordinary unweighted edges | No | Yes |
| Shortest path | Minimum edges | Minimum total weight | Minimum total weight |
| Main technique | Level traversal | Greedy | Edge relaxation |
| Main data structure | Queue | Min-heap | Edge list |
| Negative cycle detection | No | No | Yes |
| Time complexity | O(V + E) | O((V + E) log V) | O(V × E) |

Remember:

- BFS: Best for unweighted shortest paths.
- Dijkstra: Best for non-negative weighted shortest paths.
- Bellman-Ford: Useful when negative weights are present.

## 14. Time and Space Complexity

Let:

- V = Number of vertices.
- E = Number of edges.

### Time complexity

Bellman-Ford performs V - 1 relaxation rounds.

Every round examines all E edges.

Therefore:

```text
O((V - 1) × E)
```

Simplified:

```text
O(V × E)
```

The additional negative-cycle detection pass takes O(E), which does not change the overall complexity.

### Space complexity

| Data Structure | Complexity |
|---|---|
| Distance dictionary | O(V) |
| Parent dictionary | O(V) |
| Edge list | O(E) |
| Auxiliary space | O(V) |

The edge list is the input graph representation, so auxiliary space excluding the input is O(V).

## 15. Real-World Applications

1. Network routing
   - Calculate least-cost routes when edge costs can be negative.

2. Financial systems
   - Model currency exchange rates using negative logarithmic edge weights to detect arbitrage opportunities.

3. Graph analysis
   - Detect negative-weight cycles.

4. Transportation systems
   - Model routes with discounts or credits represented by negative costs.

5. Optimization systems
   - Solve shortest-path problems involving negative edge costs.

### FDE Connection

Imagine an AI-powered financial analysis system.

Different conversion rates between currencies can be represented as weighted graph edges.

For example:

```text
USD → EUR
EUR → GBP
GBP → USD
```

A currency exchange system can transform exchange rates using negative logarithms and use Bellman-Ford-style negative-cycle detection to identify possible arbitrage opportunities.

This is a mathematical model; real-world trading must also account for transaction fees, exchange limits, and changing rates.

## 16. Common Mistakes

### Mistake 1: Repeating relaxation only V times

For shortest-path calculation, V - 1 rounds are sufficient when no reachable negative cycle exists.

The additional pass is used for negative-cycle detection.

### Mistake 2: Forgetting to initialize the source distance

The source distance must be zero.

### Mistake 3: Not checking infinity

Do not relax an edge from a vertex that is unreachable from the source.

### Mistake 4: Confusing negative edges with negative cycles

A negative edge is allowed.

A negative-weight cycle is the condition that can make a finite shortest path impossible for affected reachable vertices.

### Mistake 5: Assuming every negative cycle is detected

A single-source Bellman-Ford run detects only negative cycles reachable from its source.

### Mistake 6: Confusing edge relaxation with vertex selection

Dijkstra selects the closest known vertex using a priority queue.

Bellman-Ford repeatedly checks every edge.

## 17. Practice Exercises

### Beginner

1. What is Bellman-Ford?
2. What is a negative edge weight?
3. What is edge relaxation?
4. Why does Bellman-Ford repeat V - 1 times?
5. What is a negative-weight cycle?

### Intermediate

6. Find the shortest distances from A:

```text
A → B = 4
A → C = 5
B → D = -3
D → C = 2
```

7. Implement Bellman-Ford using Python.
8. Detect a negative-weight cycle.
9. Modify the algorithm to return the actual shortest path.
10. Explain why an unreachable vertex must not be used for relaxation.

### Interview-Level Thinking

11. Why can Bellman-Ford handle negative weights?
12. Why does Dijkstra fail with negative weights?
13. Why are V - 1 rounds sufficient?
14. Can Bellman-Ford detect a negative cycle in a disconnected component?
15. How can Bellman-Ford be used to detect currency arbitrage?

## 18. Quick Revision

| Concept | Remember |
|---|---|
| Algorithm | Bellman-Ford |
| Purpose | Single-source shortest paths |
| Graph | Weighted directed graph |
| Edge weights | Positive, zero or negative |
| Main technique | Repeated edge relaxation |
| Relaxation rounds | V - 1 |
| Cycle detection | One additional pass |
| Negative cycles | Can make finite shortest paths impossible |
| Python representation | Edge list |
| Time complexity | O(V × E) |
| Auxiliary space | O(V) |
| Dijkstra comparison | Bellman-Ford supports negative weights |

## 19. Self-Assessment

You should be able to answer these questions before moving forward:

- What is Bellman-Ford?
- How does edge relaxation work?
- Why are V - 1 rounds required?
- Why can Bellman-Ford handle negative edge weights?
- What is a negative-weight cycle?
- How does Bellman-Ford detect negative cycles?
- What is the difference between Dijkstra and Bellman-Ford?
- How can you reconstruct the shortest path?
- What are the time and space complexities?
- What are the real-world applications?

## 20. Learning Outcome

After completing this topic, you should be able to:

1. Understand weighted graphs with negative edges.
2. Explain Bellman-Ford.
3. Implement edge relaxation in Python.
4. Calculate shortest distances from a source.
5. Detect reachable negative-weight cycles.
6. Reconstruct the shortest path.
7. Compare BFS, Dijkstra, and Bellman-Ford.
8. Analyze time and space complexity.

**Next recommended topic:** Floyd-Warshall Algorithm – All-Pairs Shortest Paths.
