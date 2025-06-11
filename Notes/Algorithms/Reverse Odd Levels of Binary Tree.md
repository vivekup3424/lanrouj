---
tags:
  - tree
  - binary-tree
---

Given the `root` of a **perfect** binary tree, reverse the node values at each **odd** level of the tree.

- For example, suppose the node values at level 3 are `[2,1,3,4,7,11,29,18]`, then it should become `[18,29,11,7,4,3,1,2]`.

Return _the root of the reversed tree_.

A binary tree is **perfect** if all parent nodes have two children and all leaves are on the same level.

The **level** of a node is the number of edges along the path between it and the root node.

**Example 1:**

![](https://assets.leetcode.com/uploads/2022/07/28/first_case1.png)

**Input:** root = [2,3,5,8,13,21,34]
**Output:** [2,5,3,8,13,21,34]
**Explanation:** 
The tree has only one odd level.
The nodes at level 1 are 3, 5 respectively, which are reversed and become 5, 3.



### Overview

We are given the `root` of a perfect binary tree, and our task is to return the `root` after reversing the values at the odd levels of the tree.

> A binary tree is considered perfect if all parent nodes have exactly two children and all leaves are on the same level.  
> The level of a node is defined as the number of edges along the path between it and the root node.

---

### Approach 1: Depth-First Search

#### Intuition

The structure of binary trees is inherently recursive; that is, each node's left and right children can themselves be considered the roots of smaller binary trees. This allows us to traverse the tree using recursion, breaking the problem into smaller, independent subproblems.

As we traverse the tree recursively, we process the left and right children of the current `root`. For nodes at even levels, we swap the values at their left and right child nodes to reverse the arrangement of nodes below their level, while leaving the children of odd levels unchanged.

Let's discuss the implementation of the recursive function `traverseDFS(node, leftChild, rightChild, int level)`:

- Base case: If `leftChild` or `rightChild` is null, then we can stop the recursive traversal for further child nodes.
    
- Even level: If the current level is even, swap the values rooted at `leftChild` and `rightChild`.
    
- Perfect binary tree: Since the binary tree is perfect, it is symmetrical in nature. Therefore, to reverse the levels, we would want to swap the left value of the left child with the right value of the right child, and the right value of the left child with the left value of the right child. This can be illustrated using the slideshow shown below:
    

![Current](blob:https://leetcode.com/9f6ea4a3-77ae-4a5c-b1af-6f318e6ae7be)
1 / 8

> For a more comprehensive understanding of depth-first search, check out the [DFS Explore Card 🔗](https://leetcode.com/explore/learn/card/graph/619/depth-first-search-in-graph/). This resource provides an in-depth look at DFS, explaining its key concepts and applications with a variety of problems to solidify understanding of the pattern.

#### Algorithm

Main function - `reverseOddLevels(Node root)`

- Call `traverseDFS` with the left and right children of the root, starting at level 0.

`traverseDFS` function:

- If either `leftChild` or `rightChild` is null, return immediately (base case).
    
- If the current `level` is even (odd-level swapping occurs at 0-based indexing):
    
    - Swap the values of `leftChild` and `rightChild` using a temporary variable.
- Recursively call `traverseDFS` for the next level:
    
    - Call `traverseDFS` with `leftChild.left` and `rightChild.right` (mirroring structure).
    - Call `traverseDFS` with `leftChild.right` and `rightChild.left` (mirroring structure).
- Continue recursion until all levels of the tree are processed.
    
- Return the updated `root` after all odd levels are reversed.
    

#### Implementation

#### Complexity Analysis

Let n be the number of nodes in the given tree.

- Time complexity: O(n)
    
    In the worst case, the algorithm visits each node exactly once, resulting in a time complexity of O(n). The swapping at each recursive step takes constant time. Therefore, the overall time complexity is O(n).
    
- Space complexity: O(logn))
    
    The space complexity is determined by the recursion depth of the DFS. Since we are given a perfect binary tree, the height of the tree is bounded by logn. Therefore, the space complexity is given by O(logn)).
    

---

### [

](https://leetcode.com/problems/reverse-odd-levels-of-binary-tree/editorial/#approach-2-breadth-first-search)Approach 2: Breadth-First Search

#### Intuition

Instead of DFS, we can use a breadth-first search (BFS) to traverse the tree level by level and reverse values at odd levels. We start by adding the root node to a queue, which helps manage nodes at each level.

For each level, we will pop all the nodes currently in the queue, which represent the nodes at the current level. Then, we will push their children to the queue to represent the next level. This ensures that the queue always contains the nodes for just one level at a time. When processing odd levels, we will collect the values of the nodes in an array, reverse that array, and then update the nodes' values with the reversed values. This step only happens for odd levels, while even levels remain unchanged.

This process continues until all levels are traversed. Finally, we return the root with the values at odd levels reversed.

> For a more comprehensive understanding of breadth-first search, check out the [BFS Explore Card 🔗](https://leetcode.com/explore/featured/card/graph/620/breadth-first-search-in-graph/). This resource provides an in-depth look at BFS, explaining its key concepts and applications with a variety of problems to solidify understanding of the pattern.

#### Algorithm

1. Create a queue `queue` to store the level-order traversal of the tree. Initialize it with the `root` node.
2. Initialize a variable `level` to `0` to keep track of the current tree level.
3. Perform BFS traversal:
    - While the `queue` is not empty, process the nodes level by level:
        - Retrieve the size of the current level using the queue size.
        - Create a list, `currentLevelNodes`, to store all nodes at the current level.
        - Iterate over all nodes in the current level:
            - Dequeue each node and add it to `currentLevelNodes`.
            - Enqueue its left and right children (if they exist) to the queue for the next level.
        - Check if the current level is odd:
            - If `level % 2 == 1`, reverse the values of nodes in `currentLevelNodes`.
            - Use two pointers (`left` and `right`) to swap values from the leftmost and rightmost ends of the list.
4. Increment the `level` counter after processing each level.
5. Return the `root` node after completing the traversal and reversing odd levels.

#### Implementation

#### Complexity Analysis

Let n be the number of nodes in the tree.

- Time complexity: O(n)
    
    The algorithm iterates through the tree, processing each level of nodes. The main loop performs BFS traversal, visiting each node exactly once, which results in a time complexity of O(n).
    
    Additionally, at each level, the algorithm checks if it is odd and reverses the node values if necessary. This operation occurs for each node in the queue and takes constant time per node. The overall time complexity is dominated by the BFS traversal, resulting in O(n).
    
- Space complexity: O(n)
    
    The space used by the algorithm is determined by the queue that holds the nodes at each level during BFS traversal. At most, the queue will hold all the nodes at one level, which is bounded by the number of nodes in the tree, resulting in a space complexity of O(n).
    
    Other space requirements are constant and do not contribute significantly to the space complexity. Therefore, the overall space complexity is O(n).