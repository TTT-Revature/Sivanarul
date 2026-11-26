
# Tree Traversals – Inorder, Preorder, Postorder, Level-order

**Suggested filename:** `03_tree_traversals_inorder_preorder_postorder_level_order.md`

## 1. Introduction to Tree Traversal

**Tree Traversal** is the process of visiting every node in a tree systematically.

Unlike arrays and linked lists, trees are hierarchical. Therefore, we need specific techniques to visit their nodes.

There are four fundamental tree traversal techniques:

1. Inorder Traversal
2. Preorder Traversal
3. Postorder Traversal
4. Level-order Traversal

Consider this binary tree throughout the chapter:

```text
              1
            /   \
           2     3
          / \   / \
         4   5 6   7
```

Our objective is to visit every node exactly once and produce a particular sequence.

---

## 2. Depth-First Search (DFS)

In Depth-First Search, we explore one branch of the tree as far as possible before moving to another branch.

The following three traversals belong to DFS:

- Inorder
- Preorder
- Postorder

DFS commonly uses recursion or an explicit stack.

### Understanding DFS Visually

```text
              1
            /   \
           2     3
          / \   / \
         4   5 6   7
```

DFS explores deeper nodes before moving to another branch.

The order in which a node is visited depends on the traversal technique.

---

## 3. Inorder Traversal (Left → Root → Right)

Inorder traversal follows this order:

1. Visit the Left Subtree.
2. Visit the Root Node.
3. Visit the Right Subtree.

**Formula:**

```text
Left → Root → Right
```

### Example

```text
              1
            /   \
           2     3
          / \   / \
         4   5 6   7
```

Follow the steps:

**Step 1:** Move to the left subtree of 1.

**Step 2:** Move to the left subtree of 2.

**Step 3:** Visit 4.

**Step 4:** Visit 2.

**Step 5:** Visit 5.

**Step 6:** Visit 1.

**Step 7:** Visit the right subtree of 1.

**Step 8:** Visit 6, then 3, then 7.

Final traversal:

```text
4 → 2 → 5 → 1 → 6 → 3 → 7
```

<details>
<summary>Python implementation</summary>

```python
def inorder(root):

    if root is None:
        return

    inorder(root.left)

    print(root.data, end=" ")

    inorder(root.right)
```

</details>

### Explanation

```python
inorder(root.left)
```

First, recursively visit the left subtree.

```python
print(root.data)
```

Then visit the current node.

```python
inorder(root.right)
```

Finally, recursively visit the right subtree.

### Important Point

Inorder traversal of a Binary Search Tree produces values in ascending order when the BST uses the usual ordering rule and its duplicate-handling policy is consistent.

---

## 4. Preorder Traversal (Root → Left → Right)

Preorder traversal follows this order:

1. Visit the Root Node.
2. Visit the Left Subtree.
3. Visit the Right Subtree.

**Formula:**

```text
Root → Left → Right
```

### Example

```text
              1
            /   \
           2     3
          / \   / \
         4   5 6   7
```

Follow the steps:

**Step 1:** Visit root 1.

**Step 2:** Move to the left subtree and visit 2.

**Step 3:** Visit 4.

**Step 4:** Visit 5.

**Step 5:** Move to the right subtree and visit 3.

**Step 6:** Visit 6.

**Step 7:** Visit 7.

Final traversal:

```text
1 → 2 → 4 → 5 → 3 → 6 → 7
```

<details>
<summary>Python implementation</summary>

```python
def preorder(root):

    if root is None:
        return

    print(root.data, end=" ")

    preorder(root.left)

    preorder(root.right)
```

</details>

### Explanation

```python
print(root.data)
```

Visit the current node first.

```python
preorder(root.left)
```

Then visit the left subtree.

```python
preorder(root.right)
```

Finally, visit the right subtree.

### Important Point

Preorder traversal is useful when creating a copy of a tree or serializing a tree structure, provided the representation also preserves enough information about missing children.

---

## 5. Postorder Traversal (Left → Right → Root)

Postorder traversal follows this order:

1. Visit the Left Subtree.
2. Visit the Right Subtree.
3. Visit the Root Node.

**Formula:**

```text
Left → Right → Root
```

### Example

```text
              1
            /   \
           2     3
          / \   / \
         4   5 6   7
```

Follow the steps:

**Step 1:** Move to the left subtree of 1.

**Step 2:** Visit 4.

**Step 3:** Visit 5.

**Step 4:** Visit 2.

**Step 5:** Move to the right subtree of 1.

**Step 6:** Visit 6.

**Step 7:** Visit 7.

**Step 8:** Visit 3.

**Step 9:** Finally, visit 1.

Final traversal:

```text
4 → 5 → 2 → 6 → 7 → 3 → 1
```

<details>
<summary>Python implementation</summary>

```python
def postorder(root):

    if root is None:
        return

    postorder(root.left)

    postorder(root.right)

    print(root.data, end=" ")
```

</details>

### Explanation

```python
postorder(root.left)
```

First visit the left subtree.

```python
postorder(root.right)
```

Then visit the right subtree.

```python
print(root.data)
```

Finally visit the current node.

### Important Point

Postorder traversal is useful when deleting a tree because child nodes are processed before their parent.

It is also useful when evaluating expression trees.

---

## 6. Comparing DFS Traversals

All three DFS techniques visit the same nodes, but the position of the root changes.

Consider:

```text
              1
            /   \
           2     3
          / \   / \
         4   5 6   7
```

| Traversal | Order | Output |
|---|---|---|
| Inorder | Left → Root → Right | 4, 2, 5, 1, 6, 3, 7 |
| Preorder | Root → Left → Right | 1, 2, 4, 5, 3, 6, 7 |
| Postorder | Left → Right → Root | 4, 5, 2, 6, 7, 3, 1 |

### Easy Memory Trick

- Inorder: Root comes in the middle.
- Preorder: Root comes first.
- Postorder: Root comes last.

Remember:

```text
INORDER    = L → ROOT → R
PREORDER   = ROOT → L → R
POSTORDER  = L → R → ROOT
```

---

## 7. Breadth-First Search (BFS)

Breadth-First Search visits nodes level by level.

Instead of exploring one branch deeply, it visits all nodes at the current level before moving to the next level.

For binary trees, this is called **Level-order Traversal**.

### Example

```text
              1            Level 0
            /   \
           2     3         Level 1
          / \   / \
         4   5 6   7       Level 2
```

Visit nodes in this order:

```text
Level 0: 1
Level 1: 2, 3
Level 2: 4, 5, 6, 7
```

Final output:

```text
1 → 2 → 3 → 4 → 5 → 6 → 7
```

---

## 8. Level-order Traversal Using a Queue

Level-order traversal uses a **Queue** data structure.

A queue follows FIFO:

**First In, First Out**

The first element inserted is the first element removed.

### Understanding the Queue

```text
Insert: 1 → 2 → 3

Queue:
+---+---+---+
| 1 | 2 | 3 |
+---+---+---+
  ↑       ↑
Front    Rear

Remove: 1
```

### Level-order Algorithm

1. Insert the root into the queue.
2. Remove the front node from the queue.
3. Visit that node.
4. Insert its left child if it exists.
5. Insert its right child if it exists.
6. Repeat until the queue is empty.

### Step-by-Step Example

Initial tree:

```text
              1
            /   \
           2     3
          / \   / \
         4   5 6   7
```

| Step | Removed | Added to Queue | Queue after operation |
|---|---|---|---|
| 1 | 1 | 2, 3 | 2, 3 |
| 2 | 2 | 4, 5 | 3, 4, 5 |
| 3 | 3 | 6, 7 | 4, 5, 6, 7 |
| 4 | 4 | None | 5, 6, 7 |
| 5 | 5 | None | 6, 7 |
| 6 | 6 | None | 7 |
| 7 | 7 | None | Empty |

Final output:

```text
1 → 2 → 3 → 4 → 5 → 6 → 7
```

### Python Implementation

Use `deque` from the `collections` module because removing from the front of a list using `pop(0)` is inefficient.

```python
from collections import deque


def level_order(root):

    if root is None:
        return

    queue = deque()

    queue.append(root)

    while queue:

        current = queue.popleft()

        print(current.data, end=" ")

        if current.left:
            queue.append(current.left)

        if current.right:
            queue.append(current.right)
```

### Explanation

```python
queue = deque()
```

Creates an empty queue.

```python
queue.append(root)
```

Inserts the root node.

```python
current = queue.popleft()
```

Removes and returns the front node.

```python
if current.left:
    queue.append(current.left)
```

Adds the left child if it exists.

```python
if current.right:
    queue.append(current.right)
```

Adds the right child if it exists.

The loop continues until the queue becomes empty.

---

## 9. Complete Python Implementation of All Four Traversals

Now let's implement all four traversal techniques using a single binary tree.

### Step 1: Create the Node Class

```python
class Node:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None
```

### Step 2: Create the Binary Tree

```python
root = Node(1)

root.left = Node(2)
root.right = Node(3)

root.left.left = Node(4)
root.left.right = Node(5)

root.right.left = Node(6)
root.right.right = Node(7)
```

Tree structure:

```text
              1
            /   \
           2     3
          / \   / \
         4   5 6   7
```

### Step 3: Implement Inorder

```python
def inorder(root):

    if root is None:
        return

    inorder(root.left)

    print(root.data, end=" ")

    inorder(root.right)
```

### Step 4: Implement Preorder

```python
def preorder(root):

    if root is None:
        return

    print(root.data, end=" ")

    preorder(root.left)

    preorder(root.right)
```

### Step 5: Implement Postorder

```python
def postorder(root):

    if root is None:
        return

    postorder(root.left)

    postorder(root.right)

    print(root.data, end=" ")
```

### Step 6: Implement Level-order

```python
from collections import deque


def level_order(root):

    if root is None:
        return

    queue = deque([root])

    while queue:

        current = queue.popleft()

        print(current.data, end=" ")

        if current.left:
            queue.append(current.left)

        if current.right:
            queue.append(current.right)
```

### Step 7: Execute All Traversals

```python
print("Inorder:")
inorder(root)

print("\nPreorder:")
preorder(root)

print("\nPostorder:")
postorder(root)

print("\nLevel-order:")
level_order(root)
```

### Expected Output

```text
Inorder:
4 2 5 1 6 3 7

Preorder:
1 2 4 5 3 6 7

Postorder:
4 5 2 6 7 3 1

Level-order:
1 2 3 4 5 6 7
```

---

## 10. Time and Space Complexity

Let `n` represent the number of nodes and `h` represent the height of the tree.

| Traversal | Time Complexity | Auxiliary Space |
|---|---|---|
| Inorder | O(n) | O(h) |
| Preorder | O(n) | O(h) |
| Postorder | O(n) | O(h) |
| Level-order | O(n) | O(w) |

Where:

- `n` = Total number of nodes.
- `h` = Height of the tree.
- `w` = Maximum width of the tree.

### Why is Time Complexity O(n)?

Every traversal visits each node exactly once.

If a tree contains 7 nodes, the algorithm visits all 7 nodes.

Therefore:

```text
Time Complexity = O(n)
```

### Why Does Recursive DFS Use O(h) Space?

Each recursive call uses the function call stack.

For a balanced tree, the recursion depth is relatively small.

For a skewed tree, the recursion depth can become as large as the number of nodes.

### Why Does Level-order Use O(w) Space?

The queue may need to hold all the nodes at the widest level.

For a complete binary tree, the maximum width can be approximately half the total number of nodes.

---

## 11. Practical Applications

| Traversal | Application |
|---|---|
| Inorder | Retrieve BST values in sorted order |
| Preorder | Copy or serialize tree structures |
| Postorder | Delete trees and evaluate expression trees |
| Level-order | Process data level by level and find shortest-depth nodes |

### FDE Connection

Tree traversal concepts are useful when working with:

**1. Nested JSON**

API responses often contain nested objects and arrays. Traversal-style logic helps process hierarchical information.

**2. File Systems**

A directory structure can be explored recursively or level by level.

**3. AI Decision Trees**

You can traverse decision paths to understand how a prediction was reached.

**4. Compilers**

Syntax trees are processed using different traversal strategies to generate or evaluate expressions.

---

## 12. Common Mistakes

1. Confusing Inorder with Preorder.
2. Forgetting that Postorder visits the root last.
3. Assuming Level-order uses recursion in the same way as DFS.
4. Forgetting the base condition `if root is None`.
5. Adding the right child before the left child in standard left-to-right level-order traversal.
6. Using `list.pop(0)` repeatedly for a large queue instead of `deque.popleft()`.
7. Assuming Inorder always produces sorted values. It does so for a correctly ordered BST, not every binary tree.

---

## 13. Practice Exercises

### Exercise 1: Find the Traversal Outputs

Consider this tree:

```text
              A
            /   \
           B     C
          / \     \
         D   E     F
```

Find:

1. Inorder traversal.
2. Preorder traversal.
3. Postorder traversal.
4. Level-order traversal.

### Exercise 2: Find the Traversal Outputs

Consider:

```text
              10
            /    \
           20     30
          /      /  \
         40     50   60
```

Write all four traversal sequences.

### Exercise 3: Python Coding

Create this binary tree:

```text
              100
             /   \
            50    150
           / \    / \
          25 75 125 175
```

Tasks:

1. Create the Node class.
2. Construct the tree.
3. Implement inorder traversal.
4. Implement preorder traversal.
5. Implement postorder traversal.
6. Implement level-order traversal.

### Exercise 4: Conceptual Questions

1. What is tree traversal?
2. Which three traversals belong to DFS?
3. Which traversal uses a queue?
4. Which data structure is used for iterative DFS?
5. Which traversal visits the root first?
6. Which traversal visits the root last?
7. What is the time complexity of tree traversal?
8. Why is `deque` preferred over `list.pop(0)` for level-order traversal?

### Exercise 5: FDE Scenario

You receive a hierarchical organization structure from an API.

You need to process each department and its employees.

Think about:

1. Which traversal would you choose to process departments before their children?
2. Which traversal would process child nodes before their parent?
3. Which traversal would process the organization level by level?

Explain your choices.

---

## 14. Quick Revision

| Traversal | Rule | Root Position | Data Structure |
|---|---|---|---|
| Inorder | Left → Root → Right | Middle | Recursion / Stack |
| Preorder | Root → Left → Right | First | Recursion / Stack |
| Postorder | Left → Right → Root | Last | Recursion / Stack |
| Level-order | Level by Level | Before its children | Queue |

### Remember These Four Rules

```text
INORDER:
Left → Root → Right

PREORDER:
Root → Left → Right

POSTORDER:
Left → Right → Root

LEVEL-ORDER:
Visit one level at a time
```

### Important Complexity

```text
DFS Traversals:
Time = O(n)
Auxiliary Space = O(h) for recursive implementations

Level-order:
Time = O(n)
Auxiliary Space = O(w)
```

---

## 15. Self-Assessment

- [ ] Explain what tree traversal means.
- [ ] Understand Depth-First Search.
- [ ] Perform Inorder traversal manually.
- [ ] Perform Preorder traversal manually.
- [ ] Perform Postorder traversal manually.
- [ ] Understand Breadth-First Search.
- [ ] Implement Level-order using a queue.
- [ ] Write all four traversal functions in Python.
- [ ] Understand time and space complexity.
- [ ] Identify practical applications of each traversal.

## 16. Learning Outcome

You should now be able to understand and implement the four fundamental binary tree traversal techniques.

You should also be able to trace traversal sequences manually, write recursive DFS algorithms, and implement BFS using a queue.

**Next recommended topic:** Binary Search Tree (BST) – Insertion, Searching and Deletion.
