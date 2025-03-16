---
id: binary-search-tree
aliases: []
tags:
  - bst
---

### Binary Search Tree (BST)

**What is it?**  
A Binary Search Tree (BST) is a binary tree structure where each node has a key, and all nodes follow the properties:
1. The left subtree of a node contains only nodes with keys lesser than the node’s key.
2. The right subtree of a node contains only nodes with keys greater than the node’s key.
3. Both the left and right subtrees must also be binary search trees.

**Why do we use it?**  
BSTs are efficient for operations like searching, insertion, and deletion, taking \(O(\log n)\) on average for balanced trees. They are used in scenarios where data is dynamically updated and efficiently searchable.

**Where is it used in real life?**  
BSTs are commonly used in databases and file systems, where efficient data lookup, insertion, and deletion are required. They’re also foundational in implementing associative containers in many programming languages (e.g., `map` in C++).

**How to use it?**  
1. **Insertion**: Insert a new node by comparing it with the current node and recursively moving left or right until an empty spot is found.
2. **Search**: Search by comparing the target key with the current node’s key, moving left or right as appropriate.
3. **Deletion**: Delete a node based on three cases:
   - Node has no children (simply remove it).
   - Node has one child (link the child to the parent of the deleted node).
   - Node has two children (replace the node with its in-order successor or predecessor).


### Some questions based on BST
1. [[kth-smallest-element-in-a-bst]]

