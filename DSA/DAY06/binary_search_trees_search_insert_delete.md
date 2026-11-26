
# Binary Search Trees – Search, Insert, Delete

**Suggested filename:** `04_binary_search_trees_search_insert_delete.md`

## 1. Introduction to Binary Search Trees

A **Binary Search Tree (BST)** is a special type of Binary Tree that follows a specific ordering rule.

For every node:

- Values smaller than the current node are placed in the left subtree.
- Values greater than the current node are placed in the right subtree.

This rule applies recursively to every node.

### Example

```text
              50
             /  \
            30   70
           / \   / \
          20 40 60 80
```

Observe:

For node 50:
- Left subtree contains 30, 20 and 40.
- Right subtree contains 70, 60 and 80.

For node 30:
- Left child = 20.
- Right child = 40.

For node 70:
- Left child = 60.
- Right child = 80.

This ordering makes searching, inserting, and deleting values more efficient when the tree is reasonably balanced.

---

## 2. Binary Tree vs Binary Search Tree

A Binary Search Tree is a type of Binary Tree, but not every Binary Tree is a BST.

| Binary Tree | Binary Search Tree |
|---|---|
| Each node has at most two children. | Each node has at most two children. |
| No ordering rule is required. | Follows a specific ordering rule. |
| Values can be arranged anywhere. | Smaller values go left and larger values go right. |
| Searching may require visiting every node. | Searching can use the ordering to eliminate branches. |

Example of a Binary Tree:

```text
              50
             /  \
            70   30
```

This is a valid Binary Tree, but not a valid BST under the usual ordering rule.

Example of a BST:

```text
              50
             /  \
            30   70
```

---

## 3. Important BST Rules

Consider:

```text
              50
             /  \
            30   70
           / \   / \
          20 40 60 80
```

Rules:

1. Every value in the left subtree of a node must be smaller than that node.
2. Every value in the right subtree of a node must be greater than that node.
3. Both left and right subtrees must also follow BST rules.
4. The root is the starting point for searching and insertion.
5. Each node can have at most two children.

**Important:** It is not enough to compare only the immediate children. Every descendant must satisfy the ordering constraints of all its ancestors.

For example:

```text
              50
             /  \
            30   70
           / \
          20  60
```

This is NOT a valid BST.

Why?

Node 60 is in the left subtree of 50, but 60 is greater than 50.

---

## 4. Creating a Binary Search Tree Using Python

First, create a Node class.

Each node stores:

- Data
- Reference to the left child
- Reference to the right child

### Python Code

```python
class Node:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None
```

Create the root:

```python
root = Node(50)
```

Add children manually:

```python
root.left = Node(30)
root.right = Node(70)

root.left.left = Node(20)
root.left.right = Node(40)

root.right.left = Node(60)
root.right.right = Node(80)
```

Result:

```text
              50
             /  \
            30   70
           / \   / \
          20 40 60 80
```

This is a valid BST.

However, manually connecting nodes is not practical for large datasets. We need insertion logic to construct the tree automatically.

---

## 5. Searching in a Binary Search Tree

Searching means finding whether a particular value exists in the BST.

The BST ordering rule helps us decide which direction to move.

### Searching Logic

Suppose we want to search for 60.

```text
              50
             /  \
            30   70
           / \   / \
          20 40 60 80
```

Step 1: Start at root 50.

Step 2: Compare 60 with 50.

```text
60 > 50
```

Move to the right child.

Step 3: Current node is 70.

```text
60 < 70
```

Move to the left child.

Step 4: Current node is 60.

```text
60 == 60
```

Value found!

### Search Algorithm

1. Start from the root.
2. If the current node is `None`, the value does not exist.
3. If the target equals the current node, return the node.
4. If the target is smaller, search the left subtree.
5. If the target is greater, search the right subtree.

### Python Implementation - Recursive

```python
def search(root, target):

    if root is None:
        return False

    if root.data == target:
        return True

    elif target < root.data:
        return search(root.left, target)

    else:
        return search(root.right, target)
```

### Testing

```python
print(search(root, 60))
print(search(root, 100))
```

Output:

```text
True
False
```

### Understanding the Code

```python
if root is None:
    return False
```

If we reach an empty position, the value is not present.

```python
if root.data == target:
    return True
```

If the current node matches the target, the search is successful.

```python
elif target < root.data:
    return search(root.left, target)
```

If the target is smaller, search the left subtree.

```python
else:
    return search(root.right, target)
```

Otherwise, search the right subtree.

### Time Complexity

| Situation | Time Complexity |
|---|---|
| Best case | O(1) |
| Average case for a reasonably balanced BST | O(log n) |
| Worst case | O(n) |

The worst case happens when the BST becomes highly skewed.

---

## 6. Inserting a Node into a BST

Insertion means adding a new value while maintaining the BST ordering rule.

Consider inserting:

```text
25
```

Starting BST:

```text
              50
             /  \
            30   70
           / \   / \
          20 40 60 80
```

### Step-by-Step Insertion

**Step 1:** Start at root 50.

```text
25 < 50
```

Move left.

**Step 2:** Current node is 30.

```text
25 < 30
```

Move left.

**Step 3:** Current node is 20.

```text
25 > 20
```

Move right.

**Step 4:** The right position of 20 is empty.

Insert 25 there.

Final BST:

```text
              50
             /  \
            30   70
           / \   / \
          20 40 60 80
            \
             25
```

### Insertion Algorithm

1. If the current position is empty, create a new node.
2. If the new value is smaller, move left.
3. If the new value is greater, move right.
4. Repeat until an empty position is found.

### Python Implementation - Recursive

```python
def insert(root, value):

    if root is None:
        return Node(value)

    if value < root.data:
        root.left = insert(root.left, value)

    elif value > root.data:
        root.right = insert(root.right, value)

    return root
```

### Testing

```python
root = insert(root, 25)
root = insert(root, 90)
```

The new nodes are inserted in their correct positions.

### Why Do We Return root?

This line is important:

```python
return root
```

It ensures that the root reference is returned after insertion.

When an empty position is found:

```python
return Node(value)
```

A new node is created and returned to the parent node, which connects it as its left or right child.

### Important: Duplicate Values

In this implementation, duplicate values are ignored because neither the smaller nor greater condition is satisfied.

Other BST implementations may:
- Store a count for duplicate values.
- Always place duplicates on one chosen side.
- Use a composite key.

The policy must be consistent.

---

## 7. Deleting a Node from a BST

Deletion is more complicated than searching and insertion because removing a node must preserve the BST ordering rule.

There are three main deletion cases:

1. Deleting a leaf node.
2. Deleting a node with one child.
3. Deleting a node with two children.

### Case 1: Deleting a Leaf Node

A leaf node has no children.

Example:

```text
              50
             /  \
            30   70
           / \   / \
          20 40 60 80
```

Delete node 20.

Since 20 has no children, simply remove it.

Result:

```text
              50
             /  \
            30   70
              \  / \
              40 60 80
```

Logic:

```python
if root.left is None and root.right is None:
    return None
```

### Case 2: Deleting a Node with One Child

Consider:

```text
              50
             /  \
            30   70
           /      \
          20       80
```

Delete node 30.

Node 30 has only one child: 20.

We connect its parent directly to 20.

Result:

```text
              50
             /  \
            20   70
                   \
                    80
```

Logic:

```python
if root.left is None:
    return root.right

if root.right is None:
    return root.left
```

If the left child is missing, return the right child.

If the right child is missing, return the left child.

### Case 3: Deleting a Node with Two Children

This is the most important deletion case.

Consider:

```text
              50
             /  \
            30   70
           / \   / \
          20 40 60 80
```

Delete node 50.

Node 50 has two children.

We cannot simply remove it because both subtrees must remain connected and the BST ordering must be preserved.

A common solution is to replace it with its **Inorder Successor**.

### What Is an Inorder Successor?

The inorder successor of a node is the next node in inorder traversal.

For a node with a right subtree, its inorder successor is the smallest node in that right subtree.

For node 50:

1. Move to its right child: 70.
2. Move as far left as possible.
3. Reach 60.

Therefore:

```text
Inorder Successor = 60
```

Replace 50 with 60, then delete the original node 60.

Final tree:

```text
              60
             /  \
            30   70
           / \     \
          20 40     80
```

The BST property is preserved.

**Alternative:** We can also use the inorder predecessor, which is the largest value in the left subtree.

### Finding the Minimum Value

To find the inorder successor, use a helper function:

```python
def find_min(root):

    current = root

    while current.left is not None:
        current = current.left

    return current
```

This returns the leftmost node in the subtree.

---

## 8. Complete BST Deletion Implementation

```python
def delete(root, key):

    if root is None:
        return None

    if key < root.data:

        root.left = delete(root.left, key)

    elif key > root.data:

        root.right = delete(root.right, key)

    else:

        # Case 1 and Case 2:
        # No left child
        if root.left is None:
            return root.right

        # No right child
        if root.right is None:
            return root.left

        # Case 3:
        # Find inorder successor
        successor = find_min(root.right)

        # Copy successor value
        root.data = successor.data

        # Delete original successor node
        root.right = delete(root.right, successor.data)

    return root
```

### Testing

```python
root = delete(root, 50)
```

The root value becomes the inorder successor, 60.

### Understanding the Logic

```python
if key < root.data:
    root.left = delete(root.left, key)
```

Search for the key in the left subtree.

```python
elif key > root.data:
    root.right = delete(root.right, key)
```

Search for the key in the right subtree.

```python
successor = find_min(root.right)
```

Find the smallest value in the right subtree.

```python
root.data = successor.data
```

Replace the current node's data with the successor's data.

```python
root.right = delete(root.right, successor.data)
```

Remove the original successor node to avoid having the same value twice.

---

## 9. Complete BST Program

Here is a complete runnable implementation containing:

- Node creation
- Insertion
- Searching
- Finding minimum
- Deletion
- Inorder traversal

```python
class Node:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None


def insert(root, value):

    if root is None:
        return Node(value)

    if value < root.data:
        root.left = insert(root.left, value)

    elif value > root.data:
        root.right = insert(root.right, value)

    return root


def search(root, target):

    if root is None:
        return False

    if root.data == target:
        return True

    if target < root.data:
        return search(root.left, target)

    return search(root.right, target)


def find_min(root):

    current = root

    while current.left is not None:
        current = current.left

    return current


def delete(root, key):

    if root is None:
        return None

    if key < root.data:
        root.left = delete(root.left, key)

    elif key > root.data:
        root.right = delete(root.right, key)

    else:

        if root.left is None:
            return root.right

        if root.right is None:
            return root.left

        successor = find_min(root.right)

        root.data = successor.data

        root.right = delete(root.right, successor.data)

    return root


def inorder(root):

    if root is None:
        return

    inorder(root.left)

    print(root.data, end=" ")

    inorder(root.right)


# Build BST
root = None

values = [50, 30, 70, 20, 40, 60, 80]

for value in values:
    root = insert(root, value)


print("Original BST:")
inorder(root)

print("\nSearch 60:", search(root, 60))

root = insert(root, 25)

print("After inserting 25:")
inorder(root)

root = delete(root, 50)

print("\nAfter deleting 50:")
inorder(root)
```

### Expected Output

```text
Original BST:
20 30 40 50 60 70 80

Search 60: True
After inserting 25:
20 25 30 40 50 60 70 80

After deleting 50:
20 25 30 40 60 70 80
```

Notice that inorder traversal displays the BST values in ascending order.

---

## 10. Time and Space Complexity of BST Operations

Let `n` represent the number of nodes and `h` represent the height of the BST.

| Operation | Average Case (Balanced) | Worst Case (Skewed) |
|---|---|---|
| Search | O(log n) | O(n) |
| Insert | O(log n) | O(n) |
| Delete | O(log n) | O(n) |
| Find Minimum | O(log n) | O(n) |

### Why Does a Balanced BST Perform Better?

Balanced BST:

```text
              50
             /  \
            30   70
           / \   / \
          20 40 60 80
```

The height is small.

Searching can eliminate approximately half of the remaining search space at each level.

Skewed BST:

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

This structure behaves similarly to a linked list.

Searching may require checking every node.

### Space Complexity

For the recursive implementations:

- Search: O(h) auxiliary space.
- Insert: O(h) auxiliary space.
- Delete: O(h) auxiliary space.

The recursive call stack depends on tree height.

---

## 11. Important BST Applications

| Application | Purpose |
|---|---|
| Searching | Find values efficiently |
| Dynamic data storage | Insert and remove values |
| Sorted data retrieval | Inorder traversal |
| Range queries | Find values within a range |
| Symbol tables | Organize keys |
| Database concepts | Understand ordered indexing structures |

Note: Production databases generally use B-trees or B+ trees for indexes rather than ordinary BSTs.

### FDE Connection

As a Forward-Deployed Engineer, BST concepts help you understand:

1. How ordered data structures work.
2. How search operations can reduce unnecessary comparisons.
3. How hierarchical data is organized.
4. Why balancing matters for performance.
5. How to reason about data structure choices in production systems.

For example, if an application frequently searches, inserts, and removes ordered values, understanding BSTs helps you compare possible data structures and their performance.

---

## 12. Common Mistakes

1. Assuming every Binary Tree is a BST.
2. Checking only immediate children instead of the entire subtree ordering.
3. Forgetting to return the updated root after insertion or deletion.
4. Forgetting to reconnect a child after deleting a node.
5. Deleting a node with two children without finding a valid replacement.
6. Forgetting to remove the original inorder successor.
7. Assuming every BST operation takes O(log n).
8. Ignoring the duplicate-value policy.
9. Confusing inorder successor with the right child. The successor is the leftmost node in the right subtree.

---

## 13. Practice Exercises

### Exercise 1: Identify the BST

Which of the following is a valid BST?

A:

```text
              50
             /  \
            30   70
           / \
          20 80
```

B:

```text
              50
             /  \
            30   70
           / \   / \
          20 40 60 80
```

C:

```text
              50
             /  \
            60   70
```

Explain your answer.

### Exercise 2: Search

Given:

```text
              50
             /  \
            30   70
           / \   / \
          20 40 60 80
```

Trace the search for:

1. 40
2. 80
3. 100

Write the nodes visited in each search.

### Exercise 3: Insert

Insert these values into an empty BST in the given order:

```python
values = [50, 30, 70, 20, 40, 60, 80, 35]
```

Draw the resulting tree.

### Exercise 4: Delete

Consider:

```text
              50
             /  \
            30   70
           / \   / \
          20 40 60 80
```

Draw the resulting BST after each operation, starting from the original tree:

1. Delete 20.
2. Delete 30.
3. Delete 50.

For question 2, use the tree after deleting 20.

For question 3, use the tree after deleting 30.

Identify which deletion case applies each time.

### Exercise 5: Python Coding

Implement the following:

1. Create a BST using `[40, 20, 60, 10, 30, 50, 70]`.
2. Search for 30.
3. Insert 25.
4. Delete 60.
5. Print the final inorder traversal.

### Exercise 6: Interview Questions

1. What is a Binary Search Tree?
2. Why is searching efficient in a balanced BST?
3. What happens when a BST becomes skewed?
4. What is an inorder successor?
5. How do you delete a node with two children?
6. What is the worst-case time complexity of BST search?
7. Why does inorder traversal produce sorted output in a BST?

---

## 14. Quick Revision

| Concept | Explanation |
|---|---|
| BST | Binary Tree with an ordering rule |
| Left Subtree | Contains smaller values |
| Right Subtree | Contains greater values |
| Search | Compare and move left or right |
| Insert | Find an empty position following BST rules |
| Delete - Case 1 | Remove a leaf node |
| Delete - Case 2 | Replace a node with its only child |
| Delete - Case 3 | Replace using inorder successor or predecessor |
| Inorder Successor | Smallest value in the right subtree |
| Inorder Predecessor | Largest value in the left subtree |

### Important Rules

```text
If target < current node:
    Move Left

If target > current node:
    Move Right

If target == current node:
    Value Found
```

### Important Complexity

```text
Balanced BST:
Search = O(log n)
Insert = O(log n)
Delete = O(log n)

Skewed BST:
Search = O(n)
Insert = O(n)
Delete = O(n)
```

---

## 15. Self-Assessment

- [ ] Explain the difference between a Binary Tree and a BST.
- [ ] Understand the BST ordering property.
- [ ] Create a BST using Python.
- [ ] Search for a value in a BST.
- [ ] Insert a new node into a BST.
- [ ] Delete a leaf node.
- [ ] Delete a node with one child.
- [ ] Delete a node with two children.
- [ ] Find an inorder successor.
- [ ] Understand BST time and space complexity.
- [ ] Explain why a skewed BST is inefficient.

## 16. Learning Outcome

You should now understand how Binary Search Trees organize ordered data and how to implement the three fundamental operations: searching, insertion, and deletion.

You should also be able to explain all three deletion cases and calculate their time complexity.

**Next recommended topic:** Balanced Trees – AVL Trees and Rotations.
