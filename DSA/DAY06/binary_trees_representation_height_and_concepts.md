
# Binary Trees – Representation, Height and Concepts

**Suggested filename:** `02_binary_trees_representation_height_and_concepts.md`

## 1. Introduction to Binary Trees

A **Binary Tree** is a non-linear hierarchical data structure in which each node can have a maximum of two children.

These children are called:

1. Left Child
2. Right Child

A node can have:
- Zero children.
- One child.
- Two children.

### Example

```text
             10
            /  \
           20   30
          / \
         40  50
```

Here:
- 10 is the root.
- 20 is the left child of 10.
- 30 is the right child of 10.
- 40 and 50 are children of 20.

**Important:** A Binary Tree does not automatically follow the Binary Search Tree ordering rule. It only restricts each node to at most two children.

---

## 2. Structure of a Binary Tree Node

A binary tree node typically contains three parts:

1. Data
2. Reference to the left child
3. Reference to the right child

### Node Structure

```text
        +---------+
        |  Data   |
        +---------+
        |  Left   |
        +---------+
        |  Right  |
        +---------+
```

Example:

```text
          +---------+
          |   10    |
          +---------+
          |  Left   | ----> Node 20
          +---------+
          |  Right  | ----> Node 30
          +---------+
```

The left and right references point to other nodes.

If a child does not exist, its reference is `None` in Python.

---

## 3. Binary Tree Representation

There are two common ways to represent a binary tree:

1. Linked Representation
2. Array Representation

### 3.1 Linked Representation

In linked representation, each node stores data and references to its left and right children.

Example:

```text
             10
            /  \
           20   30
          / \
         40  50
```

Conceptually:

```text
Node 10
  Left  ---> Node 20
  Right ---> Node 30

Node 20
  Left  ---> Node 40
  Right ---> Node 50

Node 30
  Left  ---> None
  Right ---> None
```

Python implementation:

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None
```

Creating a binary tree:

```python
root = Node(10)

root.left = Node(20)
root.right = Node(30)

root.left.left = Node(40)
root.left.right = Node(50)
```

Print the values:

```python
print(root.data)
print(root.left.data)
print(root.right.data)
print(root.left.left.data)
print(root.left.right.data)
```

Output:

```text
10
20
30
40
50
```

**Advantages:**
- Flexible structure.
- Memory is allocated when nodes are created.
- Suitable for sparse and irregular trees.

**Disadvantages:**
- Additional memory is required for child references.
- Accessing a particular node requires following references from other nodes.

### 3.2 Array Representation

A binary tree can also be stored using an array.

Consider this tree:

```text
             10
            /  \
           20   30
          / \   / \
         40 50 60 70
```

Array representation:

```text
Index:    0   1   2   3   4   5   6
Value:   10  20  30  40  50  60  70
```

For a binary tree stored using zero-based indexing:

| Node position | Array index formula |
|---|---|
| Parent | `(i - 1) // 2` |
| Left child | `2 * i + 1` |
| Right child | `2 * i + 2` |

Here, `i` represents the current node's array index.

Example:

For node `20`:

```text
Index = 1

Left child index  = 2 * 1 + 1 = 3
Right child index = 2 * 1 + 2 = 4
```

Therefore:
- Left child = 40
- Right child = 50

Python example:

```python
tree = [10, 20, 30, 40, 50, 60, 70]

i = 1

left_index = 2 * i + 1
right_index = 2 * i + 2

print(tree[left_index])
print(tree[right_index])
```

Output:

```text
40
50
```

**Advantages:**
- Simple representation.
- No explicit child references are needed.
- Efficient for complete or nearly complete binary trees.

**Disadvantages:**
- Can waste memory for sparse trees.
- Inserting nodes into arbitrary positions can be inconvenient.

**Important:** Array representation is particularly useful for heaps, which are usually represented using arrays.

---

## 4. Types of Binary Trees

Understanding the different types of binary trees is important before learning traversal and search operations.

### 4.1 Full Binary Tree

A **Full Binary Tree** is a binary tree in which every node has either zero or exactly two children.

Example:

```text
             10
            /  \
           20   30
          / \
         40  50
```

Here:
- Node 10 has two children.
- Node 20 has two children.
- Nodes 30, 40 and 50 have zero children.

This is a Full Binary Tree.

A node with exactly one child would violate the full binary tree property.

### 4.2 Complete Binary Tree

A **Complete Binary Tree** is a binary tree in which:

- Every level is completely filled except possibly the last level.
- The last level is filled from left to right without gaps.

Example:

```text
             10
            /  \
           20   30
          / \  /
         40 50 60
```

This is a Complete Binary Tree.

Example of an incomplete tree:

```text
             10
            /  \
           20   30
            \   /
             50 60
```

This is not complete because there is a gap before a node on the last level.

### 4.3 Perfect Binary Tree

A **Perfect Binary Tree** is a binary tree in which:

- Every internal node has exactly two children.
- All leaf nodes are at the same level.

Example:

```text
             10
            /  \
           20   30
          / \   / \
         40 50 60 70
```

Every level is completely filled.

### 4.4 Balanced Binary Tree

A **Balanced Binary Tree** generally means that the heights of the left and right subtrees of every node differ by at most one.

For this chapter, use the common height-balanced definition:

```text
abs(left_subtree_height - right_subtree_height) <= 1
```

Example:

```text
             10
            /  \
           20   30
          /
         40
```

The height difference at each node is at most one, so this tree is height-balanced.

A highly skewed tree is not balanced:

```text
             10
            /
           20
          /
         30
        /
       40
```

Note: Different data structures and textbooks may use different balancing rules.

### 4.5 Degenerate or Skewed Binary Tree

A **Degenerate Binary Tree** is a tree in which every parent has only one child.

Example:

```text
             10
            /
           20
            \
             30
              \
               40
```

Types:

Left-skewed:

```text
        10
       /
      20
     /
    30
   /
  40
```

Right-skewed:

```text
10
  \
   20
     \
      30
        \
         40
```

A skewed binary tree behaves similarly to a linked list in terms of its shape.

---

## 5. Height of a Binary Tree

**Height of a Binary Tree** is the number of edges in the longest path from the root to a leaf.

Consider:

```text
             10
            /  \
           20   30
          / \
         40  50
```

The longest root-to-leaf paths are:

```text
10 → 20 → 40
10 → 20 → 50
```

Each path contains two edges.

Therefore:

```text
Height of tree = 2
```

### Important Height Rules

Using the edge-counting convention:

- Height of an empty tree = -1.
- Height of a leaf node = 0.
- Height of a tree with one node = 0.

### Height Formula

```text
Height(node) = 1 + max(
    Height(left child),
    Height(right child)
)
```

For an empty node, height is -1.

For a leaf node:

```text
Height = 1 + max(-1, -1)
       = 0
```

For the previous tree:

```text
Height(40) = 0
Height(50) = 0
Height(30) = 0

Height(20) = 1 + max(0, 0)
           = 1

Height(10) = 1 + max(1, 0)
           = 2
```

---

## 6. Calculating Binary Tree Height Using Python

We can calculate tree height using recursion.

### Code

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None


def height(root):

    if root is None:
        return -1

    left_height = height(root.left)
    right_height = height(root.right)

    return 1 + max(left_height, right_height)


root = Node(10)

root.left = Node(20)
root.right = Node(30)

root.left.left = Node(40)
root.left.right = Node(50)

print("Tree Height:", height(root))
```

Output:

```text
Tree Height: 2
```

### Understanding the Logic

Step 1: If the node is `None`, return -1.

Step 2: Calculate the height of the left subtree.

Step 3: Calculate the height of the right subtree.

Step 4: Select the greater height.

Step 5: Add 1 for the current node's edge to its child.

This process continues until the entire tree is evaluated.

**Time Complexity:** O(n), because every node is visited once.

**Auxiliary Space Complexity:** O(h), due to the recursive call stack, where `h` is the tree height.

---

## 7. Maximum Number of Nodes in a Binary Tree

A binary tree can contain at most two children per node.

For a tree with levels numbered from 0, the maximum number of nodes at each level is:

| Level | Maximum nodes |
|---|---:|
| 0 | 1 |
| 1 | 2 |
| 2 | 4 |
| 3 | 8 |
| 4 | 16 |

The maximum number of nodes at level `L` is:

```text
2^L
```

The maximum number of nodes in a binary tree of height `h` is:

```text
2^(h + 1) - 1
```

Example:

For height 2:

```text
Maximum nodes = 2^(2 + 1) - 1
              = 8 - 1
              = 7
```

A perfect binary tree of height 2 contains exactly 7 nodes.

---

## 8. Minimum Height of a Binary Tree

If a binary tree contains `n` nodes, its minimum possible height occurs when its nodes are arranged as compactly as possible.

Using the edge-counting convention:

```text
Minimum height = ceil(log2(n + 1)) - 1
```

Example:

For 7 nodes:

```text
Minimum height = ceil(log2(8)) - 1
               = 3 - 1
               = 2
```

A perfect binary tree containing 7 nodes has height 2.

A tree with the same number of nodes can have a much greater height if it is skewed.

---

## 9. Number of Leaf Nodes and Internal Nodes

For a Full Binary Tree:

Let:
- `I` = Number of internal nodes.
- `L` = Number of leaf nodes.
- `N` = Total number of nodes.

The relationship is:

```text
L = I + 1
```

Example:

```text
             10
            /  \
           20   30
          / \
         40  50
```

Internal nodes = 2

Leaf nodes = 3

```text
L = I + 1
  = 2 + 1
  = 3
```

This relationship applies to Full Binary Trees, not every arbitrary binary tree.

---

## 10. Binary Tree vs Binary Search Tree

These two concepts are related, but they are not the same.

| Binary Tree | Binary Search Tree |
|---|---|
| Each node has at most two children. | Each node has at most two children. |
| No ordering rule is required. | Follows a search ordering rule. |
| Values can appear in any position. | Values are arranged according to comparison rules. |
| Searching may require visiting every node. | Searching can be efficient when balanced. |

Binary Tree:

```text
             10
            /  \
           50   20
```

This is a valid Binary Tree.

But it does not follow the usual BST ordering rule.

Binary Search Tree:

```text
             50
            /  \
           30   70
          / \
         20  40
```

The left subtree contains smaller values and the right subtree contains larger values.

Note: The exact handling of duplicate values depends on the BST implementation.

---

## 11. Time Complexity and Height

Tree height affects the efficiency of many tree operations.

Consider two trees containing the same number of nodes.

Balanced tree:

```text
             10
            /  \
           20   30
          / \   / \
         40 50 60 70
```

Skewed tree:

```text
10
 \
  20
    \
     30
       \
        40
          \
           50
```

The balanced tree has a smaller height.

The skewed tree has a larger height.

For a balanced BST, searching is typically O(log n).

For a skewed BST, searching can become O(n).

Important: A general binary tree does not automatically provide O(log n) searching. That efficiency depends on its ordering and balance properties.

---

## 12. Practical Applications of Binary Trees

| Application | Purpose |
|---|---|
| Binary Search Trees | Searching and organizing data |
| Heaps | Priority queues |
| Expression Trees | Representing mathematical expressions |
| Decision Trees | Making decisions in machine learning |
| Huffman Trees | Data compression |
| Syntax Trees | Representing programming language structures |

### FDE Connection

As a Forward-Deployed Engineer, understanding binary trees is useful when:

- Processing hierarchical application data.
- Working with JSON and nested API responses.
- Understanding database indexing concepts.
- Integrating AI systems that use decision trees.
- Debugging recursive data structures.
- Understanding how priority queues and search structures work.

For example, a decision tree used by an AI system can represent a sequence of decisions:

```text
              Is age > 18?
               /       \
             Yes        No
             /           \
       Eligible       Not Eligible
```

Each decision is represented as a node, and its outcomes lead to child nodes.

---

## 13. Practice Exercises

### Exercise 1: Identify the Binary Tree Type

Identify whether each tree is Full, Complete, Perfect, or Skewed.

A:

```text
             10
            /  \
           20   30
          / \
         40  50
```

B:

```text
             10
            /  \
           20   30
          / \  /
         40 50 60
```

C:

```text
             10
            /  \
           20   30
          / \   / \
         40 50 60 70
```

D:

```text
             10
               \
                20
                  \
                   30
```

### Exercise 2: Calculate Height

Consider:

```text
             10
            /  \
           20   30
          /
         40
        /
       50
```

Find:
1. Height of node 50.
2. Height of node 40.
3. Height of node 20.
4. Height of the entire tree.

Use the edge-counting convention.

### Exercise 3: Array Representation

Given:

```python
tree = [10, 20, 30, 40, 50, 60, 70]
```

Find:
1. Left child of index 0.
2. Right child of index 0.
3. Left child of index 1.
4. Right child of index 1.
5. Parent of index 4.

### Exercise 4: Python Coding

Create a binary tree using the following structure:

```text
             100
            /   \
           50    150
          / \      \
         25  75    200
```

Tasks:
1. Create a `Node` class.
2. Build the tree.
3. Write a recursive function to calculate its height.
4. Print the height.

### Exercise 5: Conceptual Questions

1. What is the maximum number of children in a binary tree node?
2. What is the difference between a Full and Complete Binary Tree?
3. What is the difference between a Complete and Perfect Binary Tree?
4. Why can a skewed tree become inefficient?
5. Does every Binary Tree follow BST ordering rules?
6. What is the time complexity of calculating tree height?

---

## 14. Quick Revision

| Concept | Key Point |
|---|---|
| Binary Tree | Each node has at most two children |
| Left Child | First child reference |
| Right Child | Second child reference |
| Linked Representation | Nodes connected through references |
| Array Representation | Nodes stored using array indexes |
| Full Binary Tree | Every node has 0 or 2 children |
| Complete Binary Tree | Last level filled from left to right |
| Perfect Binary Tree | All levels completely filled |
| Balanced Binary Tree | Left and right subtree heights differ by at most 1 at every node |
| Skewed Tree | Each parent has only one child |
| Height | Longest downward path measured in edges |
| Leaf Height | Always 0 |
| Empty Tree Height | -1 under the edge-counting convention |

### Important Formulas

```text
Maximum nodes at level L = 2^L

Maximum nodes at height h = 2^(h + 1) - 1

Minimum height for n nodes =
ceil(log2(n + 1)) - 1

Left child index = 2 * i + 1

Right child index = 2 * i + 2

Parent index = (i - 1) // 2

Full Binary Tree:
Leaf nodes = Internal nodes + 1
```

## 15. Self-Assessment

- [ ] Explain the structure of a binary tree.
- [ ] Understand linked representation.
- [ ] Understand array representation.
- [ ] Identify different types of binary trees.
- [ ] Calculate the height of a binary tree.
- [ ] Understand the relationship between height and number of nodes.
- [ ] Implement a binary tree using Python.
- [ ] Write a recursive height calculation function.
- [ ] Understand why tree balance matters.

## 16. Learning Outcome

You should now be able to explain binary tree structures, represent them using Python and arrays, identify their common types, and calculate their height using recursion.

**Next recommended topic:** Binary Tree Traversals – Inorder, Preorder and Postorder.
