
# BST Complexity and Problem Solving

## 1. Introduction

In the previous chapter, we learned how to perform three important operations in a Binary Search Tree (BST):

1. Search
2. Insert
3. Delete

Now we need to understand how efficiently these operations work.

**BST Complexity** describes how much time and additional memory an operation requires as the number of nodes increases.

The performance of a BST mainly depends on its height.

Remember:

- A balanced BST has a relatively small height.
- An unbalanced BST can have a very large height.
- A skewed BST can behave like a linked list.

---

## 2. Understanding BST Height

Height is the number of edges on the longest path from a node to its deepest leaf.

Consider two BSTs containing the same five values.

### Balanced BST

```text
          30
         /  \
       20    40
      /        \
     10         50
```

Height = 2 edges.

### Skewed BST

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

Height = 4 edges.

Both trees contain five nodes, but their heights are different.

This difference directly affects the performance of BST operations.

---

## 3. Time Complexity of BST Operations

The three fundamental BST operations are:

- Search
- Insert
- Delete

Their time complexity depends on the height of the tree.

| Operation | Balanced-height BST | Worst-case skewed BST |
|---|---|---|
| Search | O(log n) | O(n) |
| Insert | O(log n) | O(n) |
| Delete | O(log n) | O(n) |

Here, `n` represents the number of nodes.

### Why is the balanced BST O(log n)?

Consider a balanced BST:

```text
             50
           /    \
         30      70
        /  \    /  \
       20  40  60  80
```

Suppose we search for 80.

Steps:

1. Compare 80 with 50.
2. Move right to 70.
3. Move right to 80.
4. Target found.

Only three comparisons are required.

In a balanced tree, the number of levels grows approximately logarithmically as the number of nodes increases.

For example:

| Number of nodes | Approximate balanced height |
|---:|---:|
| 7 | 2 |
| 15 | 3 |
| 31 | 4 |
| 63 | 5 |
| 127 | 6 |

The height increases slowly even when the number of nodes grows significantly.

Therefore, searching, inserting, and deleting take O(log n) time in a balanced-height BST.

### Why is the skewed BST O(n)?

Consider this tree:

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

Suppose we search for 50.

We must visit:

1. 10
2. 20
3. 30
4. 40
5. 50

All five nodes may need to be checked.

In the worst case, we visit every node.

Therefore, the time complexity becomes O(n).

---

## 4. Understanding Space Complexity

Space complexity describes how much additional memory an algorithm requires.

For recursive BST operations, memory is used by the function call stack.

Consider recursive search:

```python
def search(root, target):

    if root is None:
        return False

    if root.data == target:
        return True

    if target < root.data:
        return search(root.left, target)

    return search(root.right, target)
```

Every recursive call waits for the next call to finish.

The maximum number of active calls depends on the height of the tree.

Therefore:

| Tree structure | Recursive auxiliary space |
|---|---|
| Balanced-height BST | O(log n) |
| Skewed BST | O(n) |

**Important:** An iterative BST search uses O(1) auxiliary space because it does not require recursive calls.

---

## 5. Best Case, Average Case and Worst Case

Let's understand the three common complexity scenarios.

### Best Case – O(1)

The target is available at the root.

```text
        50
       /  \
     30    70
```

Searching for 50 requires only one comparison.

Time complexity = O(1).

### Balanced-height case – O(log n)

The tree has a height proportional to log n.

Searching may require visiting only a small number of levels.

Time complexity = O(log n).

### Worst Case – O(n)

The BST becomes completely skewed.

```text
10
  \
   20
     \
      30
        \
         40
```

Searching for the deepest value requires visiting all nodes.

Time complexity = O(n).

**Note:** O(log n) is not guaranteed merely because a tree is called a BST. It requires the tree to have logarithmic height.

---

## 6. Problem Solving – Example 1: Count BST Nodes

### Problem

Given a BST, count the total number of nodes.

Consider:

```text
        50
       /  \
     30    70
    / \    /
   20 40  60
```

Total nodes = 6.

### Python solution

```python
def count_nodes(root):

    if root is None:
        return 0

    return (
        1
        + count_nodes(root.left)
        + count_nodes(root.right)
    )
```

### Understanding the logic

- If the node is `None`, return 0.
- Count the current node as 1.
- Recursively count the left subtree.
- Recursively count the right subtree.
- Add all three results.

### Complexity

- Time: O(n), because every node is visited once.
- Auxiliary space: O(h), due to recursion.

---

## 7. Problem Solving – Example 2: Find the Minimum Value

### Problem

Find the smallest value in a BST.

Consider:

```text
          50
         /  \
       30    70
      /
     20
    /
   10
```

The smallest value is always located at the leftmost node.

### Python solution

```python
def find_min(root):

    if root is None:
        return None

    while root.left is not None:
        root = root.left

    return root.data
```

### Output

```python
print(find_min(root))
```

```text
10
```

### Complexity

- Time: O(h).
- Auxiliary space: O(1).

This is an iterative solution, so it does not create recursive calls.

---

## 8. Problem Solving – Example 3: Find the Maximum Value

### Problem

Find the largest value in a BST.

The largest value is located at the rightmost node.

### Python solution

```python
def find_max(root):

    if root is None:
        return None

    while root.right is not None:
        root = root.right

    return root.data
```

### Complexity

- Time: O(h).
- Auxiliary space: O(1).

---

## 9. Problem Solving – Example 4: Validate a BST

### Problem

Determine whether a binary tree follows the BST ordering property.

Consider:

```text
        50
       /  \
     30    70
    / \    / \
   20 40  60 80
```

This is a valid BST.

However, consider:

```text
        50
       /  \
     30    70
          /
         45
```

Although 45 is smaller than 70, it appears in the right subtree of 50.

Since 45 is smaller than 50, the tree is not a valid BST.

**Important:** Checking only the immediate parent and child is not enough. Every node must satisfy the ordering constraints of all its ancestors.

### Python solution

```python
def is_valid_bst(root, low=float("-inf"), high=float("inf")):

    if root is None:
        return True

    if not (low < root.data < high):
        return False

    return (
        is_valid_bst(root.left, low, root.data)
        and
        is_valid_bst(root.right, root.data, high)
    )
```

### Understanding the logic

For every node:

- Its value must be greater than the lower bound.
- Its value must be smaller than the upper bound.
- The left subtree receives the current node's value as its upper bound.
- The right subtree receives the current node's value as its lower bound.

### Complexity

- Time: O(n), because every node may need to be checked.
- Auxiliary space: O(h), due to recursion.

**Note:** This implementation assumes distinct values and uses strict BST ordering.

---

## 10. Problem Solving – Example 5: Find the Kth Smallest Element

### Problem

Find the Kth smallest value in a BST.

Consider:

```text
        50
       /  \
     30    70
    / \    / \
   20 40  60 80
```

Inorder traversal:

```text
20, 30, 40, 50, 60, 70, 80
```

If K = 3:

The third smallest element is 40.

### Python solution

```python
def kth_smallest(root, k):

    result = []

    def inorder(node):

        if node is None:
            return

        inorder(node.left)
        result.append(node.data)
        inorder(node.right)

    inorder(root)

    if k < 1 or k > len(result):
        return None

    return result[k - 1]
```

### Output

```python
print(kth_smallest(root, 3))
```

```text
40
```

### Complexity

- Time: O(n), because this implementation visits every node.
- Auxiliary space: O(n), for the result list, plus O(h) recursion stack.

**Optimization:** An inorder traversal can stop as soon as the Kth element is reached. An iterative implementation can achieve O(h + k) time and O(h) auxiliary space.

---

## 11. Comparing BST with Other Data Structures

| Feature | Array (unsorted) | Linked List | Balanced BST |
|---|---|---|---|
| Search | O(n) | O(n) | O(log n) |
| Insert | O(1) at end, excluding resizing | O(1) at known position | O(log n) |
| Delete | O(n) in general | O(1) at known node, excluding lookup | O(log n) |
| Maintains sorted order | No | No | Yes |

**Important:** These complexities assume the operation and its position requirements are handled as stated. For example, inserting into a sorted array generally takes O(n).

---

## 12. How to Improve BST Performance

An ordinary BST does not automatically maintain its balance.

If values are inserted in sorted order, the tree can become skewed.

To solve this problem, we use self-balancing BSTs.

Examples:

1. AVL Tree
2. Red-Black Tree

These structures perform rotations to maintain a controlled tree height.

Their search, insertion, and deletion operations have O(log n) worst-case time complexity.

### Example: AVL Tree

An AVL Tree maintains a balance condition at every node.

Its balance factor is:

```text
Balance Factor = Height of Left Subtree - Height of Right Subtree
```

For a valid AVL node, the balance factor must be -1, 0, or +1.

We will study AVL Trees separately.

---

## 13. Real-world Applications

Understanding BST complexity is useful in software engineering.

Examples:

1. Ordered data management.
2. Searching and maintaining sorted records.
3. Implementing ordered sets and maps.
4. Understanding indexing and tree-based data structures.
5. Designing efficient in-memory lookup systems.

**FDE connection:** When integrating APIs and working with customer records, you may need efficient lookup, validation, and ordered data processing. Understanding tree complexity helps you choose an appropriate data structure rather than assuming every search takes O(1).

Production database indexes commonly use B-trees or B+ trees rather than ordinary BSTs.

---

## 14. Practice Exercises

### Beginner Level

**Exercise 1:** Count the number of nodes in a BST.

**Exercise 2:** Find the minimum and maximum values.

**Exercise 3:** Calculate the height of a BST.

### Intermediate Level

**Exercise 4:** Validate whether a given binary tree is a BST.

**Exercise 5:** Find the Kth smallest element.

**Exercise 6:** Find the inorder predecessor of a given value.

### Advanced Level

**Exercise 7:** Find the lowest common ancestor (LCA) of two values in a BST.

**Exercise 8:** Find the range of values between two given numbers.

**Exercise 9:** Determine whether two BSTs contain the same set of values.

---

## 15. Quick Revision

| Concept | Key Point |
|---|---|
| BST height | Longest root-to-leaf path measured in edges |
| Balanced-height BST | O(log n) operations |
| Skewed BST | O(n) operations |
| Search | O(h) |
| Insert | O(h) |
| Delete | O(h) |
| Count nodes | O(n) |
| Find minimum | O(h) |
| Find maximum | O(h) |
| Validate BST | O(n) |
| Kth smallest | O(n) in the basic implementation |
| Recursive auxiliary space | O(h) |

Remember:

- `n` = number of nodes.
- `h` = height of the tree.
- Balanced-height BST: h = O(log n).
- Skewed BST: h = O(n).

---

## 16. Self-Assessment Checklist

Before moving to the next topic, make sure you can:

- [ ] Explain why BST height affects performance.
- [ ] Differentiate balanced and skewed BSTs.
- [ ] Explain O(log n) and O(n) with examples.
- [ ] Calculate search, insertion, and deletion complexity.
- [ ] Find minimum and maximum values.
- [ ] Count the total number of nodes.
- [ ] Validate a BST using lower and upper bounds.
- [ ] Find the Kth smallest element.
- [ ] Explain why self-balancing trees are useful.

## Learning Outcome

After completing this chapter, you should be able to analyze BST time and space complexity, solve common BST problems using Python, and understand when an ordinary BST needs balancing.

**Next Recommended Topic:** Balanced Trees – AVL Trees and Rotations.
