---
id: Rat in a Maze
aliases: 
tags:
  - backtracking
  - dfs
---

Consider a grid, where 0 symbolises empty path, and 1 symbolises blocked path
There is a source and a destination
The rat can move only in 4 directions: up, down, left, right
We have to print all the possible paths that the rat can take to reach the destination

```python
moves = [[-1, 0], [1, 0], [0, 1], [0, -1]]
total_moves = []
def dfs(x, y, path, maze):
    rows = len(maze)
    cols = len(maze[0])
    if x == rows - 1 and y == cols - 1:
        total_moves.append(path)
        return
    if x < 0 or x >= rows or y < 0 or y >= cols or maze[x][y] == 0:
        return
    maze[x][y] = 0
    for dx, dy in moves:
        newx = x + dx
        newy = y + dy
        dfs(newx, newy, path + [(newx, newy)], maze)

```

