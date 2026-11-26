
# Shortest Path – Dijkstra's Algorithm

## 1. Introduction to Dijkstra's Algorithm

Dijkstra's Algorithm is a shortest-path algorithm used to find the minimum distance from one starting vertex to other vertices in a weighted graph.

It is commonly used in:

- GPS navigation
- Network routing
- Delivery route optimization
- Communication networks
- AI pathfinding

### Real-world analogy

Imagine travelling from Chennai to different cities.

You have multiple routes, and each route has a different distance.

Your objective is to find the shortest distance from Chennai to every other city.

Dijkstra's Algorithm helps calculate these shortest distances.

## 2. Understanding Weighted Graphs

A weighted graph contains edges with numerical values.

These values can represent:

- Distance
- Travel time
- Cost
- Network latency

Example:

```text
        4
   A -------- B
   |          |
  2|          |5
   |          |
   C -------- D
        1
```

Edges:

```text
A → B = 4
A → C = 2
C → D = 1
B → D = 5
```

Suppose we want to find the shortest distance from A to D.

Possible paths:

Path 1:

```text
A → B → D

Distance = 4 + 5 = 9
```

Path 2:

```text
A → C → D

Distance = 2 + 1 = 3
```

Shortest path:

```text
A → C → D

Minimum distance = 3
```

Dijkstra's Algorithm helps find this minimum distance systematically.

## 3. Important Concepts Before Dijkstra

### 1. Source Vertex

The starting vertex from which we calculate shortest distances.

Example:

```text
Source = A
```

### 2. Distance

The total weight of the edges along a path.

Example:

```text
A → C → D

Distance = 2 + 1 = 3
```

### 3. Relaxation

Relaxation means checking whether a newly discovered path provides a shorter distance to a vertex.

Formula:

```text
new_distance = distance[current] + edge_weight
```

If:

```text
new_distance < distance[neighbor]
```

Update:

```text
distance[neighbor] = new_distance
```

Example:

Current known distance to D = 9.

New path through C:

```text
Distance to C = 2
Edge C → D = 1

New distance = 2 + 1 = 3
```

Since 3 is smaller than 9, update D's distance to 3.

This process is called relaxation.

## 4. How Dijkstra's Algorithm Works

Dijkstra follows a greedy approach.

At each step, it selects the unprocessed vertex with the smallest known distance.

### Main steps

1. Select a source vertex.
2. Initialize the distance of the source to 0.
3. Initialize all other vertex distances to infinity.
4. Select the unprocessed vertex with the smallest distance.
5. Examine its neighboring vertices.
6. Calculate the new distance through the current vertex.
7. If the new distance is smaller, update the neighbor's distance.
8. Repeat until all reachable vertices have been processed.

### Initial distance table

Suppose the source is A.

| Vertex | Initial Distance |
|---|---:|
| A | 0 |
| B | ∞ |
| C | ∞ |
| D | ∞ |

Why infinity?

We have not discovered any path from A to those vertices yet.

## 5. Dijkstra's Algorithm – Visual Dry Run

Consider this weighted undirected graph:

```text
        4
   A -------- B
   |          |
  2|          |5
   |          |
   C -------- D
        1
```

Edges:

```text
A - B = 4
A - C = 2
B - D = 5
C - D = 1
```

Source vertex:

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

Current vertex: A

### Step 2: Process A

A's neighbors:

- B = 4
- C = 2

Update distances:

| Vertex | Distance |
|---|---:|
| A | 0 |
| B | 4 |
| C | 2 |
| D | ∞ |

Now select the unprocessed vertex with the smallest distance.

C = 2

### Step 3: Process C

C's neighbor:

- D = 1

New distance to D:

```text
Distance to C + Weight(C, D)

2 + 1 = 3
```

Update D:

| Vertex | Distance |
|---|---:|
| A | 0 |
| B | 4 |
| C | 2 |
| D | 3 |

Next smallest unprocessed vertex:

D = 3

### Step 4: Process D

D's neighbor:

- B = 5

Calculate the new distance to B:

```text
Distance to D + Weight(D, B)

3 + 5 = 8
```

But the current distance to B is 4.

Since 8 is greater than 4, do not update B.

Next smallest unprocessed vertex:

B = 4

### Step 5: Process B

B has no shorter route to update.

The algorithm finishes.

### Final shortest distances

| Vertex | Shortest Distance from A |
|---|---:|
| A | 0 |
| B | 4 |
| C | 2 |
| D | 3 |

Shortest path from A to D:

```text
A → C → D

Total distance = 3
```

## 6. Dijkstra's Algorithm Using Python

We can represent a weighted graph using an adjacency list.

Each vertex stores its neighbors and corresponding weights.

### Graph representation

```python
graph = {
    "A": {"B": 4, "C": 2},
    "B": {"A": 4, "D": 5},
    "C": {"A": 2, "D": 1},
    "D": {"B": 5, "C": 1}
}
```

For example:

```python
"A": {"B": 4, "C": 2}
```

This means:

- A connects to B with weight 4.
- A connects to C with weight 2.

### Complete implementation

We use Python's `heapq` module to implement a min-priority queue.

```python
import heapq

def dijkstra(graph, start):

    distances = {
        vertex: float("inf")
        for vertex in graph
    }

    distances[start] = 0

    priority_queue = [(0, start)]

    while priority_queue:

        current_distance, current = heapq.heappop(
            priority_queue
        )

        if current_distance > distances[current]:
            continue

        for neighbor, weight in graph[current].items():

            new_distance = current_distance + weight

            if new_distance < distances[neighbor]:

                distances[neighbor] = new_distance

                heapq.heappush(
                    priority_queue,
                    (new_distance, neighbor)
                )

    return distances


graph = {
    "A": {"B": 4, "C": 2},
    "B": {"A": 4, "D": 5},
    "C": {"A": 2, "D": 1},
    "D": {"B": 5, "C": 1}
}

result = dijkstra(graph, "A")

print(result)
```

### Output

```text
{'A': 0, 'B': 4, 'C': 2, 'D': 3}
```

## 7. Understanding the Python Code

Let's understand the important statements.

### Step 1: Import heapq

```python
import heapq
```

Python's `heapq` module provides a min-heap implementation.

It helps retrieve the vertex with the smallest known distance efficiently.

### Step 2: Initialize distances

```python
distances = {
    vertex: float("inf")
    for vertex in graph
}
```

Initially, every vertex has an infinite distance.

### Step 3: Set source distance to zero

```python
distances[start] = 0
```

The distance from the source to itself is zero.

### Step 4: Initialize the priority queue

```python
priority_queue = [(0, start)]
```

Each entry contains:

```text
(distance, vertex)
```

Initially:

```text
[(0, A)]
```

### Step 5: Extract the smallest distance

```python
current_distance, current = heapq.heappop(
    priority_queue
)
```

Removes the entry with the smallest distance.

### Step 6: Skip outdated entries

```python
if current_distance > distances[current]:
    continue
```

The same vertex may enter the priority queue multiple times when a shorter route is discovered.

An older entry may therefore contain an outdated distance.

This condition skips it.

### Step 7: Explore neighbors

```python
for neighbor, weight in graph[current].items():
```

Checks every neighboring vertex and its edge weight.

### Step 8: Calculate the new distance

```python
new_distance = current_distance + weight
```

Adds the distance to the current vertex and the edge weight.

### Step 9: Relaxation

```python
if new_distance < distances[neighbor]:
```

Checks whether the new route is shorter than the previously known route.

### Step 10: Update and push

```python
distances[neighbor] = new_distance

heapq.heappush(
    priority_queue,
    (new_distance, neighbor)
)
```

Updates the shortest known distance and inserts the new candidate into the priority queue.

## 8. Why Does Dijkstra Use a Min-Heap?

Imagine there are 100 vertices.

At every step, Dijkstra needs to select the unprocessed vertex with the smallest known distance.

Without a priority queue, we may scan all vertices to find the minimum.

That can be expensive.

A min-heap helps retrieve the smallest distance efficiently.

Important operations:

| Operation | Min-Heap Complexity |
|---|---|
| Insert | O(log V) |
| Remove minimum | O(log V) |
| Peek minimum | O(1) |

This improves the overall performance of Dijkstra's Algorithm.

## 9. Finding the Actual Shortest Path

The previous implementation returns the shortest distances.

But sometimes we need the actual path, not just the distance.

For example:

```text
Source = A
Destination = D
```

Expected result:

```text
A → C → D
```

To reconstruct the path, maintain a parent dictionary.

### Python implementation

```python
import heapq

def dijkstra_path(graph, start, target):

    distances = {
        vertex: float("inf")
        for vertex in graph
    }

    parent = {
        vertex: None
        for vertex in graph
    }

    distances[start] = 0

    priority_queue = [(0, start)]

    while priority_queue:

        current_distance, current = heapq.heappop(
            priority_queue
        )

        if current_distance > distances[current]:
            continue

        if current == target:
            break

        for neighbor, weight in graph[current].items():

            new_distance = current_distance + weight

            if new_distance < distances[neighbor]:

                distances[neighbor] = new_distance

                parent[neighbor] = current

                heapq.heappush(
                    priority_queue,
                    (new_distance, neighbor)
                )

    if distances[target] == float("inf"):
        return None, float("inf")

    path = []

    current = target

    while current is not None:

        path.append(current)

        current = parent[current]

    path.reverse()

    return path, distances[target]


graph = {
    "A": {"B": 4, "C": 2},
    "B": {"A": 4, "D": 5},
    "C": {"A": 2, "D": 1},
    "D": {"B": 5, "C": 1}
}

path, distance = dijkstra_path(graph, "A", "D")

print("Shortest path:", path)
print("Shortest distance:", distance)
```

### Output

```text
Shortest path: ['A', 'C', 'D']
Shortest distance: 3
```

### Understanding the parent dictionary

```python
parent[neighbor] = current
```

Stores the previous vertex on the currently best-known path.

Example:

```python
{
    "A": None,
    "B": "A",
    "C": "A",
    "D": "C"
}
```

To reconstruct the path:

1. Start from D.
2. Find its parent C.
3. Find C's parent A.
4. Stop at None.
5. Reverse the collected path.

Final path:

```text
A → C → D
```

## 10. Important Limitation – Negative Edge Weights

Dijkstra's Algorithm does not work correctly for graphs containing negative edge weights in general.

Example:

```text
A → B = 2
A → C = 5
C → B = -10
```

Possible paths from A to B:

Direct path:

```text
A → B = 2
```

Alternative path:

```text
A → C → B

5 + (-10) = -5
```

The actual shortest path is -5.

However, Dijkstra may process B with distance 2 before discovering the better route through C.

Its greedy assumption is no longer valid.

### Which algorithm should we use?

| Algorithm | Use |
|---|---|
| BFS | Unweighted graphs or equal edge costs |
| Dijkstra | Weighted graphs with non-negative edge weights |
| Bellman-Ford | Graphs that may contain negative edge weights |
| Floyd-Warshall | All-pairs shortest paths |

Important: Bellman-Ford can also detect reachable negative-weight cycles. If a relevant negative cycle exists, a finite shortest path may not exist.

## 11. Dijkstra vs BFS

| Feature | BFS | Dijkstra |
|---|---|---|
| Graph | Unweighted | Weighted |
| Main data structure | Queue | Min-priority queue |
| Selection | First discovered level | Smallest known distance |
| Edge weights | Equal cost | Non-negative weights |
| Shortest path | Minimum number of edges | Minimum total weight |
| Typical time | O(V + E) | O((V + E) log V) with a binary heap and adjacency list |

### Example

Suppose:

```text
A → B = 10
A → C = 2
C → B = 1
```

BFS considers the direct route A → B because it uses one edge.

Dijkstra considers the total weights:

Direct route:

```text
A → B = 10
```

Alternative route:

```text
A → C → B = 2 + 1 = 3
```

Dijkstra finds:

```text
A → C → B = 3
```

BFS does not optimize total edge weight when weights differ.

## 12. Time and Space Complexity

Let:

- V = Number of vertices.
- E = Number of edges.

Using an adjacency list and a binary min-heap:

| Operation | Complexity |
|---|---|
| Initialize distances | O(V) |
| Heap insertion | O(log V) |
| Heap extraction | O(log V) |
| Relax edges | O(E) |
| Overall time | O((V + E) log V) |
| Auxiliary space | O(V + E) |

The common overall time complexity is:

```text
O((V + E) log V)
```

For a connected graph, this is often written as:

```text
O(E log V)
```

The priority queue may contain multiple entries for a vertex, so its size can grow to O(E).

The distance dictionary, parent dictionary, and visited-related state require O(V) space.

The graph itself requires O(V + E) storage and is not counted as auxiliary space.

## 13. Real-World Applications

1. GPS navigation
   - Find the shortest or lowest-cost route between locations.

2. Network routing
   - Find efficient paths between network devices.

3. Delivery optimization
   - Calculate minimum-distance routes.

4. Communication networks
   - Find routes with minimum network cost.

5. Robotics
   - Find low-cost paths through a map represented as a graph.

6. Cloud infrastructure
   - Model network connections and calculate least-cost routes.

### FDE Connection

Imagine an AI-powered delivery management system.

A delivery network contains multiple locations and roads.

Each road has a travel cost.

```text
Warehouse
   /   \
  4     2
 /       \
A         B
 \       /
  3     1
   \   /
  Customer
```

Dijkstra can calculate the minimum total edge cost from the warehouse to each reachable location.

In a real delivery system, the edge weight might represent distance, estimated travel time, or monetary cost.

However, real-world traffic conditions may change, so the graph weights may need to be updated regularly.

## 14. Common Mistakes

### Mistake 1: Using Dijkstra with negative weights

Dijkstra requires non-negative edge weights.

Use Bellman-Ford when negative weights are allowed.

### Mistake 2: Confusing shortest distance with shortest number of edges

A path with fewer edges may have a higher total weight.

Dijkstra minimizes total weight, not the number of edges.

### Mistake 3: Forgetting relaxation

Always compare the newly calculated distance with the existing distance.

### Mistake 4: Not using a priority queue

A normal queue does not automatically select the smallest known distance.

Use a min-heap.

### Mistake 5: Forgetting infinity initialization

Initially, all vertices except the source should have an infinite distance.

### Mistake 6: Not handling unreachable vertices

If a vertex cannot be reached from the source, its distance remains infinity.

### Mistake 7: Not handling outdated heap entries

A vertex may have multiple entries in the priority queue.

Skip entries whose distance is greater than the currently recorded distance.

## 15. Practice Exercises

### Beginner

1. What is Dijkstra's Algorithm?
2. What is a weighted graph?
3. What is relaxation?
4. Why do we initialize distances with infinity?
5. Why does Dijkstra use a min-heap?

### Intermediate

6. Find the shortest distance from A to D:

```text
A → B = 4
A → C = 2
C → D = 1
B → D = 5
```

7. Implement Dijkstra using Python.
8. Modify the implementation to return the actual shortest path.
9. Find the shortest distances to all reachable vertices.
10. What happens when a vertex is unreachable?

### Interview-Level Thinking

11. Why does Dijkstra fail with negative edge weights?
12. What is the difference between BFS and Dijkstra?
13. Why is a min-heap preferred over a normal list?
14. What is the purpose of the parent dictionary?
15. When would you choose Bellman-Ford instead of Dijkstra?

## 16. Quick Revision

| Concept | Remember |
|---|---|
| Algorithm | Dijkstra |
| Purpose | Shortest paths from one source |
| Graph | Weighted graph |
| Edge weights | Non-negative |
| Approach | Greedy |
| Data structure | Min-priority queue |
| Python module | `heapq` |
| Distance initialization | Infinity |
| Source distance | 0 |
| Relaxation | Update if new distance is smaller |
| Path reconstruction | Parent dictionary |
| Time complexity | O((V + E) log V) |
| Auxiliary space | O(V + E) |
| Negative weights | Not supported |

## 17. Self-Assessment

You should be able to answer these questions before moving forward:

- What is Dijkstra's Algorithm?
- How does it find the shortest path?
- What is relaxation?
- Why does it use a min-heap?
- What is the purpose of infinity initialization?
- How do you reconstruct the actual shortest path?
- Why does Dijkstra fail with negative edge weights?
- What is the difference between BFS and Dijkstra?
- What are the time and space complexities?
- When should you use Bellman-Ford?

## 18. Learning Outcome

After completing this topic, you should be able to:

1. Understand weighted graphs.
2. Explain Dijkstra's Algorithm.
3. Understand greedy selection and relaxation.
4. Implement Dijkstra using Python.
5. Use `heapq` as a priority queue.
6. Find shortest distances from a source vertex.
7. Reconstruct the actual shortest path.
8. Understand the limitations of Dijkstra.
9. Analyze time and space complexity.

**Next recommended topic:** Bellman-Ford Algorithm – Shortest Path with Negative Edge Weights.
