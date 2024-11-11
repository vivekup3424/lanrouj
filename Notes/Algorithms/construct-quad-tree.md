Given a `n * n` matrix `grid` of `0's` and `1's` only. We want to represent `grid` with a Quad-Tree.

Return _the root of the Quad-Tree representing_ `grid`.

A Quad-Tree is a tree data structure in which each internal node has exactly four children. Besides, each node has two attributes:

- `val`: True if the node represents a grid of 1's or False if the node represents a grid of 0's. Notice that you can assign the `val` to True or False when `isLeaf` is False, and both are accepted in the answer.
- `isLeaf`: True if the node is a leaf node on the tree or False if the node has four children.

class Node {
    public boolean val;
    public boolean isLeaf;
    public Node topLeft;
    public Node topRight;
    public Node bottomLeft;
    public Node bottomRight;
}

We can construct a Quad-Tree from a two-dimensional area using the following steps:

1. If the current grid has the same value (i.e all `1's` or all `0's`) set `isLeaf` True and set `val` to the value of the grid and set the four children to Null and stop.
2. If the current grid has different values, set `isLeaf` to False and set `val` to any value and divide the current grid into four sub-grids as shown in the photo.
3. Recurse for each of the children with the proper sub-grid.

![](https://assets.leetcode.com/uploads/2020/02/11/new_top.png)

If you want to know more about the Quad-Tree, you can refer to the [wiki](https://en.wikipedia.org/wiki/Quadtree).


**Example 1:**

![](https://assets.leetcode.com/uploads/2020/02/11/grid1.png)

**Input:** grid = \[\[0,1],\[1,0]]
**Output:** \[\[0,1],\[1,0],\[1,1],\[1,1],\[1,0]]
**Explanation:** The explanation of this example is shown below:
Notice that 0 represents False and 1 represents True in the photo representing the Quad-Tree.
![](https://assets.leetcode.com/uploads/2020/02/12/e1tree.png)

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/02/12/e2mat.png)

**Input:** grid as shown above
**Output:** \[\[0,1],\[1,1],\[0,1],\[1,1],\[1,0],null,null,null,null,\[1,0],\[1,0],\[1,1],\[1,1]]
**Explanation:** All values in the grid are not the same. We divide the grid into four sub-grids.
The topLeft, bottomLeft and bottomRight each has the same value.
The topRight have different values so we divide it into 4 sub-grids where each has the same value.
Explanation is shown in the photo below:
![](https://assets.leetcode.com/uploads/2020/02/12/e2tree.png)

**Constraints:**

- `n == grid.length == grid[i].length`
- `n == 2x` where `0 <= x <= 6`

---

## My initial approach
```c++
class Solution {
public:
    Node* constructTreeNode(vector<vector<int>> &grid, int x1, int x2, int y1, int y2) {
        int count0 = 0, count1 = 0;
        for(int i = x1; i < x2; i++) {
            for(int j = y1; j < y2; j++) {
                if(grid[i][j] == 0) count0++;
                else count1++;
            }
        }

        // Check if the current region is uniform
        if(count0 == 0) {
            return new Node(1, true);
        } else if(count1 == 0) {
            return new Node(0, true);
        } else {
            // The node is not a leaf, so it has four children
            Node* newNode = new Node(0, false);
            int midx = (x1 + x2) / 2;
            int midy = (y1 + y2) / 2;
            
            // Recursively divide the grid into four quadrants
            newNode->topLeft = constructTreeNode(grid, x1, midx, y1, midy);
            newNode->topRight = constructTreeNode(grid, x1, midx, midy, y2);
            newNode->bottomLeft = constructTreeNode(grid, midx, x2, y1, midy);
            newNode->bottomRight = constructTreeNode(grid, midx, x2, midy, y2);
            
            return newNode;
        }
    }

    Node* construct(vector<vector<int>>& grid) {
        int rows = grid.size(), cols = grid[0].size();
        return constructTreeNode(grid, 0, rows, 0, cols);
    }
};

```

But this approach is giving me some error.