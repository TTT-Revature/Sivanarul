
# AVL Trees – Conceptual Understanding

## 1. Introduction to AVL Trees

An AVL Tree is a **self-balancing Binary Search Tree (BST)**.

It follows all the normal BST rules:

- Smaller values are placed in the left subtree.
- Greater values are placed in the right subtree.

However, an AVL Tree has one additional condition:

**The height difference between the left and right subtrees of every node must not exceed 1.**

This condition keeps the tree balanced and prevents it from becoming excessively skewed.

### Why do we need AVL Trees?

Consider inserting these values into a normal BST:

```python
values = [10, 20, 30, 40, 50]
```

A normal BST may look like this:

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

This is a skewed BST.

Searching for 50 may require checking every node.

Time complexity: O(n).

An AVL Tree automatically adjusts its structure to maintain balance.

### Balanced AVL Tree

The same values can be organized as:

```text
          30
         /  \
       20    40
      /        \
     10         50
```

Now the height is much smaller.

Searching, inserting, and deleting take O(log n) worst-case time in an AVL Tree.

---

## 2. AVL Tree Properties

An AVL Tree follows these important properties:

1. It is a Binary Search Tree.
2. Every node can have at most two children.
3. The height difference between the left and right subtrees of every node must be at most 1.
4. It automatically restores balance after insertion or deletion when necessary.
5. It maintains O(log n) worst-case height.

### Example of a valid AVL Tree

```text
          40
         /  \
       20    60
      / \    / \
     10 30  50 70
```

This tree is balanced at every node.

### Example of an unbalanced tree

```text
          40
         /
       20
      /
     10
    /
   5
```

The node 40 has:

- Left subtree height = 2
- Right subtree height = -1

Height difference = 3.

Therefore, this is not a valid AVL Tree.

---

## 3. Understanding Balance Factor

The Balance Factor (BF) tells us how balanced a particular node is.

It is calculated using:

```text
Balance Factor =
Height of Left Subtree - Height of Right Subtree
```

### Possible balance factors in an AVL Tree

| Balance Factor | Meaning |
|---|---|
| 0 | Both subtrees have equal height |
| +1 | Left subtree is taller by 1 |
| -1 | Right subtree is taller by 1 |
| +2 | Left-heavy and unbalanced |
| -2 | Right-heavy and unbalanced |

A valid AVL Tree requires every node to have a balance factor of:

```text
-1, 0, or +1
```

### Example 1: Balance Factor = 0

```text
        30
       /  \
     20    40
```

Left height = 0

Right height = 0

Balance Factor = 0 - 0 = 0

This node is balanced.

### Example 2: Balance Factor = +1

```text
        30
       /
     20
```

Left height = 0

Right height = -1

Balance Factor = 0 - (-1) = +1

This node is balanced.

### Example 3: Balance Factor = -2

```text
        30
          \
           40
             \
              50
```

Using the edge-based height convention:

- Left subtree height = -1
- Right subtree height = 1

Balance Factor = -1 - 1 = -2

This node is unbalanced.

**Important:** We use height = -1 for an empty subtree and height = 0 for a leaf node.

---

## 4. Why Do AVL Trees Need Rotations?

When we insert or delete a node, the height of a subtree may change.

This can cause a node's balance factor to become +2 or -2.

To restore balance, AVL Trees use an operation called **Rotation**.

A rotation changes the arrangement of nodes while preserving the BST ordering property.

There are four major rotation cases:

1. LL – Left Left
2. RR – Right Right
3. LR – Left Right
4. RL – Right Left

Let's understand each case.

---

## 5. LL Rotation – Left Left Case

### When does it happen?

LL imbalance occurs when a new node is inserted into the left subtree of the left child.

Example: Insert 30, 20, 10.

Before rotation:

```text
        30
       /
      20
     /
    10
```

Node 30 becomes left-heavy.

Its balance factor becomes +2.

### Solution: Right Rotation

We perform a right rotation around node 30.

After rotation:

```text
        20
       /  \
      10   30
```

Now the tree is balanced.

**Remember:**

LL case → Right Rotation.

---

## 6. RR Rotation – Right Right Case

### When does it happen?

RR imbalance occurs when a new node is inserted into the right subtree of the right child.

Example: Insert 10, 20, 30.

Before rotation:

```text
    10
      \
       20
         \
          30
```

Node 10 becomes right-heavy.

Its balance factor becomes -2.

### Solution: Left Rotation

We perform a left rotation around node 10.

After rotation:

```text
        20
       /  \
      10   30
```

Now the tree is balanced.

**Remember:**

RR case → Left Rotation.

---

## 7. LR Rotation – Left Right Case

### When does it happen?

LR imbalance occurs when a new node is inserted into the right subtree of the left child.

Example: Insert 30, 10, 20.

Before rotation:

```text
        30
       /
      10
        \
         20
```

Node 30 becomes left-heavy, but its left child is right-heavy.

A single right rotation is not sufficient.

### Solution: Two Rotations

Step 1: Left rotation around node 10.

```text
        30
       /
      20
     /
    10
```

Step 2: Right rotation around node 30.

Final result:

```text
        20
       /  \
      10   30
```

**Remember:**

LR case → Left Rotation followed by Right Rotation.

---

## 8. RL Rotation – Right Left Case

### When does it happen?

RL imbalance occurs when a new node is inserted into the left subtree of the right child.

Example: Insert 10, 30, 20.

Before rotation:

```text
    10
      \
       30
      /
     20
```

Node 10 becomes right-heavy, but its right child is left-heavy.

### Solution: Two Rotations

Step 1: Right rotation around node 30.

```text
    10
      \
       20
         \
          30
```

Step 2: Left rotation around node 10.

Final result:

```text
        20
       /  \
      10   30
```

**Remember:**

RL case → Right Rotation followed by Left Rotation.

---

## 9. Comparison of the Four Rotation Cases

| Case | Insertion location | Rotation required |
|---|---|---|
| LL | Left of left child | Right rotation |
| RR | Right of right child | Left rotation |
| LR | Right of left child | Left, then right |
| RL | Left of right child | Right, then left |

### Easy way to remember

- LL → Right
- RR → Left
- LR → Left + Right
- RL → Right + Left

The case name describes the direction of the imbalance path, not the rotation direction.

---

## 10. AVL Tree vs Normal BST

| Feature | Normal BST | AVL Tree |
|---|---|---|
| Data ordering | BST property | BST property |
| Self-balancing | No | Yes |
| Balance factor | Not required | Maintained |
| Rotations | Not required | Used when necessary |
| Worst-case search | O(n) | O(log n) |
| Worst-case insertion | O(n) | O(log n) |
| Worst-case deletion | O(n) | O(log n) |
| Implementation | Simpler | More complex |

AVL Trees require additional work to maintain their balance, but provide predictable worst-case lookup performance.

---

## 11. Time and Space Complexity

Because an AVL Tree maintains logarithmic height, its fundamental operations have the following worst-case complexities.

| Operation | Time Complexity |
|---|---|
| Search | O(log n) |
| Insert | O(log n) |
| Delete | O(log n) |
| Find minimum | O(log n) |
| Find maximum | O(log n) |
| Single rotation | O(1) |

### Space Complexity

- Recursive search, insertion and deletion: O(log n) auxiliary stack space.
- Iterative search: O(1) auxiliary space.
- AVL node storage: O(n) total space.

The tree itself requires O(n) memory to store n nodes.

---

## 12. Where Are AVL Trees Useful?

AVL Trees are useful when applications require:

1. Fast searching.
2. Maintaining sorted data.
3. Frequent lookup operations.
4. Predictable worst-case search performance.
5. Ordered in-memory collections.

### FDE connection

Imagine building an application that maintains customer records in memory.

You frequently need to:

- Search customers by ID.
- Insert new customers.
- Delete old records.
- Maintain ordered data.

An AVL Tree provides predictable O(log n) worst-case operations.

However, the best production data structure depends on the workload, storage requirements, concurrency and available libraries.

---

## 13. Common Mistakes

1. Assuming every BST is balanced.
2. Confusing a Binary Tree with an AVL Tree.
3. Calculating balance factor using the wrong subtraction order.
4. Assuming balance factor must always be zero.
5. Confusing LL rotation with left rotation.
6. Forgetting that LR and RL require two rotations.
7. Checking only the root balance factor instead of every node.
8. Assuming rotations change the sorted ordering of the BST.

---

## 14. Practice Exercises

### Exercise 1 – Identify the Balance Factor

Consider:

```text
        40
       /  \
     20    60
    /
   10
```

Find the balance factor of node 40.

### Exercise 2 – Identify the Rotation

Insert the following values:

```python
[30, 20, 10]
```

Questions:

- Which imbalance occurs?
- Which rotation is required?
- What will the final tree look like?

### Exercise 3 – Identify the Rotation

Insert:

```python
[10, 20, 30]
```

Identify the imbalance and the required rotation.

### Exercise 4 – Identify LR or RL

Insert:

```python
[30, 10, 20]
```

Which rotation is required?

### Exercise 5 – Understand the Difference

Why can a normal BST take O(n) time for searching while an AVL Tree guarantees O(log n) worst-case search time?

---

## 15. Quick Revision

| Concept | Key Point |
|---|---|
| AVL Tree | Self-balancing BST |
| Balance Factor | Left height - Right height |
| Valid balance factor | -1, 0, +1 |
| LL imbalance | Right rotation |
| RR imbalance | Left rotation |
| LR imbalance | Left + Right rotation |
| RL imbalance | Right + Left rotation |
| Search | O(log n) |
| Insert | O(log n) |
| Delete | O(log n) |
| Main objective | Maintain logarithmic tree height |

---

## 16. Self-Assessment Checklist

Before moving to the next chapter, make sure you can:

- [ ] Explain what an AVL Tree is.
- [ ] Explain why normal BSTs can become skewed.
- [ ] Calculate the balance factor.
- [ ] Identify an unbalanced node.
- [ ] Explain LL and RR rotations.
- [ ] Explain LR and RL rotations.
- [ ] Differentiate AVL Trees from normal BSTs.
- [ ] Explain AVL time and space complexity.

## Learning Outcome

After completing this chapter, you should understand how AVL Trees maintain balance, how balance factors work, and why rotations are necessary.

**Next Recommended Topic:** AVL Trees – Insertion and Rotations Implementation in Python.
