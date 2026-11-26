
# Tree Terminology and Basic Concepts

**Suggested filename:** `01_tree_terminology_and_basic_concepts.md`

## 1. Introduction to Trees

A **Tree** is a non-linear data structure used to organize data in a hierarchical relationship.

Unlike arrays and linked lists, where elements are generally arranged sequentially, a tree organizes elements in parent-child relationships.

### Real-world examples

- File systems: Folders contain files and subfolders.
- Organization charts: Managers have employees reporting to them.
- Family trees: Parents have children.
- HTML DOM: Elements contain other elements.
- Database indexes: Trees help organize and search data efficiently.

### Simple Tree Diagram

Consider the following organization:

```text
             CEO
              |
       +------+------+
       |             |
    Manager A     Manager B
       |             |
    +--+--+       +--+--+
    |     |       |     |
  Dev1  Dev2    Dev3  Dev4
```

This is a hierarchical structure.

---

## 2. What is a Node?

A **Node** is an individual element in a tree that stores data.

For example:

```text
       10
      /  \
     20   30
```

Here:
- 10 is a node.
- 20 is a node.
- 30 is a node.

Every value represented in the tree is stored inside a node.

---

## 3. What is the Root Node?

The **Root Node** is the topmost node of a tree.

It is the starting point of the tree.

```text
         10  <-- Root
        /  \
       20   30
      / \
     40  50
```

Here, `10` is the root node.

Important:
- A tree has exactly one root node if it is non-empty.
- The root node does not have a parent.
- All other nodes descend from the root.

---

## 4. Parent and Child Nodes

A **Parent Node** is a node that has one or more nodes directly below it.

A **Child Node** is a node directly connected below another node.

```text
          10
         /  \
        20   30
       / \
      40  50
```

In this example:

- 10 is the parent of 20 and 30.
- 20 is the parent of 40 and 50.
- 20 and 30 are children of 10.
- 40 and 50 are children of 20.

Remember: Parent-child relationships are direct relationships.

---

## 5. Sibling Nodes

Nodes that share the same parent are called **Siblings**.

```text
          10
         /  \
        20   30
       / \
      40  50
```

Examples:
- 20 and 30 are siblings because they share parent 10.
- 40 and 50 are siblings because they share parent 20.

But 20 and 40 are not siblings.

---

## 6. Leaf Node (External Node)

A **Leaf Node** is a node that does not have any children.

```text
          10
         /  \
        20   30
       / \
      40  50
```

Leaf nodes:
- 30
- 40
- 50

Important:
- A leaf node has zero children.
- Leaf nodes are also called terminal nodes or external nodes in many contexts.

---

## 7. Internal Node

An **Internal Node** is a node that has at least one child.

```text
          10
         /  \
        20   30
       / \
      40  50
```

Internal nodes:
- 10
- 20

Leaf nodes:
- 30
- 40
- 50

Note: The root can also be an internal node if it has children.

---

## 8. Edge

An **Edge** is the connection between two nodes.

```text
          10
         /  \
        20   30
       /
      40
```

Edges:
- 10 → 20
- 10 → 30
- 20 → 40

A tree containing `N` nodes has exactly `N - 1` edges.

Example:

If a tree contains 5 nodes:

```text
Number of edges = 5 - 1
                = 4
```

This property applies to a non-empty tree.

---

## 9. Path

A **Path** is a sequence of nodes connected through edges.

```text
          10
         /  \
        20   30
       /
      40
     /
    50
```

One path is:

```text
10 → 20 → 40 → 50
```

Path length is usually measured by the number of edges.

Here:

```text
10 → 20 = 1 edge
20 → 40 = 1 edge
40 → 50 = 1 edge

Total path length = 3 edges
```

Note: Some contexts measure path length by nodes. Always check the definition being used.

---

## 10. Ancestor and Descendant

### Ancestor

An **Ancestor** of a node is any node that appears above it along the path from the root.

### Descendant

A **Descendant** of a node is any node that appears below it in its subtree.

Example:

```text
             10
            /  \
           20   30
          / \
         40  50
```

For node 40:

Ancestors:
- 20
- 10

Descendants of node 20:
- 40
- 50

Important:
- Parent is the immediate ancestor.
- Child is the immediate descendant.

---

## 11. Depth of a Node

**Depth** is the number of edges from the root node to a particular node.

The root has depth 0.

```text
             10       Depth 0
            /  \
           20   30    Depth 1
          / \
         40  50       Depth 2
```

Examples:

| Node | Depth |
|---|---:|
| 10 | 0 |
| 20 | 1 |
| 30 | 1 |
| 40 | 2 |
| 50 | 2 |

Depth measures how far a node is from the root.

---

## 12. Height of a Node

**Height of a node** is the number of edges in the longest downward path from that node to a leaf.

```text
             10
            /  \
           20   30
          / \
         40  50
```

Heights:

| Node | Height |
|---|---:|
| 40 | 0 |
| 50 | 0 |
| 30 | 0 |
| 20 | 1 |
| 10 | 2 |

A leaf node has height 0.

The height of a tree is the height of its root.

Therefore, the tree above has height 2.

**Remember the difference:**

- Depth: Root to node.
- Height: Node to its deepest leaf.

---

## 13. Level of a Node

The **Level** of a node describes its position in the tree.

In the common convention used here:

```text
Level = Depth + 1
```

Example:

```text
             10       Level 1
            /  \
           20   30    Level 2
          / \
         40  50       Level 3
```

| Node | Level |
|---|---:|
| 10 | 1 |
| 20 | 2 |
| 30 | 2 |
| 40 | 3 |
| 50 | 3 |

Note: Some textbooks define the root at level 0. Always identify the convention.

---

## 14. Subtree

A **Subtree** is a tree formed by a node and all its descendants.

Consider:

```text
             10
            /  \
           20   30
          / \
         40  50
```

The subtree rooted at node 20 is:

```text
          20
         /  \
        40   50
```

A subtree is itself a tree.

---

## 15. Degree of a Node

The **Degree of a Node** is the number of children that node has.

Example:

```text
             10
           / | \
          20 30 40
             |
             50
```

| Node | Degree |
|---|---:|
| 10 | 3 |
| 20 | 0 |
| 30 | 1 |
| 40 | 0 |
| 50 | 0 |

The degree of the tree is the maximum degree of any node.

In this example:

```text
Degree of tree = 3
```

---

## 16. Types of Trees - Basic Introduction

### General Tree

A general tree allows a node to have any number of children.

```text
             A
          /  |  \
         B   C   D
            / \
           E   F
```

### Binary Tree

A Binary Tree is a tree in which each node can have at most two children.

They are commonly called:
- Left Child
- Right Child

```text
             10
            /  \
           20   30
          / \
         40  50
```

A node can have:
- Zero children.
- One child.
- Two children.

### Binary Search Tree (BST)

A Binary Search Tree is a binary tree with an ordering rule:

- Values smaller than a node are placed in its left subtree.
- Values greater than a node are placed in its right subtree.

Example:

```text
             50
            /  \
           30   70
          / \   / \
         20 40 60 80
```

For now, understand the structure. BST operations will be covered separately.

---

## 17. Python Representation of a Tree

We can represent a binary tree using a Python class.

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None
```

Create nodes:

```python
root = Node(10)

root.left = Node(20)
root.right = Node(30)

root.left.left = Node(40)
root.left.right = Node(50)
```

The resulting tree:

```text
             10
            /  \
           20   30
          / \
         40  50
```

Explanation:

- `data` stores the node's value.
- `left` stores the reference to the left child.
- `right` stores the reference to the right child.
- `None` means that child does not currently exist.

Print the root and its children:

```python
print(root.data)
print(root.left.data)
print(root.right.data)
```

Output:

```text
10
20
30
```

This is a basic way to build a binary tree in Python.

---

## 18. Important Tree Properties

For a non-empty tree:

1. A tree has exactly one root.
2. Every node except the root has exactly one parent.
3. A tree with N nodes has N - 1 edges.
4. There is exactly one simple path between any two nodes in a tree.
5. A leaf node has zero children.
6. A binary tree allows at most two children per node.
7. The height of a leaf is 0 when height is measured in edges.

---

## 19. Real-World Applications of Trees

| Application | How Trees Are Used |
|---|---|
| File systems | Organize folders and files |
| HTML DOM | Represent nested HTML elements |
| Database indexes | Support efficient data lookup |
| AI decision trees | Represent decisions and outcomes |
| Search engines | Organize and search structured information |
| Network routing | Represent hierarchical routing structures |
| Compilers | Represent expressions and program syntax |

### FDE Connection

As a Forward-Deployed Engineer, you may work with:

- JSON responses containing nested objects.
- API responses with hierarchical data.
- File and folder structures.
- HTML document structures.
- AI systems that use tree-based decision logic.

For example, an API might return:

```json
{
    "department": "Engineering",
    "employees": [
        {
            "name": "Arun",
            "role": "Developer"
        },
        {
            "name": "Priya",
            "role": "Tester"
        }
    ]
}
```

Understanding hierarchical structures helps you process nested API responses and transform them into useful application data.

---

## 20. Practice Exercises

### Exercise 1: Identify Tree Components

Consider:

```text
             A
            / \
           B   C
          / \
         D   E
```

Identify:
1. Root node.
2. Parent of D.
3. Siblings.
4. Leaf nodes.
5. Internal nodes.
6. Number of edges.

### Exercise 2: Calculate Depth and Height

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
1. Depth of node 50.
2. Height of node 20.
3. Height of the entire tree.
4. Level of node 40 using root level 1.

### Exercise 3: Python Implementation

Create a binary tree with:

```text
             100
            /   \
           50    150
          / \
         25  75
```

Tasks:
1. Create a `Node` class.
2. Create the root node.
3. Connect the left and right children.
4. Print the root value.
5. Print the value of the left child's right child.

### Exercise 4: Conceptual Questions

1. What is the difference between a node and an edge?
2. Can a root node also be a leaf node?
3. What is the difference between depth and height?
4. Are all binary trees Binary Search Trees?
5. What is a subtree?

---

## 21. Quick Revision

| Term | Meaning |
|---|---|
| Tree | Hierarchical data structure |
| Node | Individual element in a tree |
| Root | Topmost node |
| Parent | Node with one or more children |
| Child | Node directly below a parent |
| Sibling | Nodes sharing the same parent |
| Leaf | Node with no children |
| Internal Node | Node with at least one child |
| Edge | Connection between two nodes |
| Path | Sequence of connected nodes |
| Ancestor | Node above another node |
| Descendant | Node below another node |
| Depth | Edges from root to a node |
| Height | Longest downward path to a leaf |
| Level | Position of a node in the tree |
| Subtree | A node and all its descendants |
| Degree | Number of children of a node |

---

## 22. Self-Assessment

After completing this topic, you should be able to:

- [ ] Explain what a tree data structure is.
- [ ] Identify root, parent, child and sibling nodes.
- [ ] Identify leaf and internal nodes.
- [ ] Understand edges and paths.
- [ ] Calculate depth and height.
- [ ] Identify ancestors, descendants and subtrees.
- [ ] Understand the degree of a node.
- [ ] Differentiate a general tree, binary tree and BST.
- [ ] Create a basic binary tree using Python.

## 23. Learning Outcome

You now understand the fundamental terminology and structure of trees.

**Next recommended topic:** Binary Tree - Structure, Properties and Types.
