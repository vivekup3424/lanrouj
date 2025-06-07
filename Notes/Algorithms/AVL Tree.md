---
tags:
  - avl-tree
  - binary-tree
  - tree
  - self-balanced
---
Adelson-Velsy and Landis
It is a self-balancing [[Binary Search Tree]] 

Both AVL trees and red-black trees are balanced binary search trees, but they differ in how strictly they maintain their balance:

1. **AVL trees** enforce a very strict balance where the height difference between left and right subtrees of any node can't be more than 1. This is called the "balance factor" requirement.
2. **[[Red-black trees]]** maintain balance through a different set of properties (involving node coloring), which results in a less strict height balance. In red-black trees, one path from root to leaf can be up to twice as long as another path.

AVL trees are often compared with [red–black trees](https://en.wikipedia.org/wiki/Red%E2%80%93black_tree "Red–black tree") because both support the same set of operations and take O ( log ⁡ n ) time for the basic operations. For lookup-intensive applications, AVL trees are faster than red–black trees because they are more strictly balanced.
