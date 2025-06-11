---
id: Knight Tour
aliases: []
tags:
  - backtracking
  - dfs
---
## ***Naive Algorithm for Knight’s tour***
The Naive Algorithm is to generate all tours one by one and check if the generated tour satisfies the constraints.

```
while there are untried tours  
{   
   generate the next tour   
   if this tour covers all squares   
   {   
      print this path;  
   }  
}
```

## DFS Code or Backtracking Code
```python
    # Check if the time limit is exceeded
    if time.time() - start_time > time_limit:
        return False

    if move_count == size * size:
        return True

    knight_moves = [
        (2, 1),
        (1, 2),
        (-1, 2),
        (-2, 1),
        (-2, -1),
        (-1, -2),
        (1, -2),
        (2, -1),
    ]

    for dx, dy in knight_moves:
        new_x, new_y = x + dx, y + dy
        if is_valid_move(new_x, new_y, board):
            board[new_x][new_y] = move_count
            if solve_knights_tour(
                board, new_x, new_y, move_count + 1, start_time, time_limit
            ):
                return True
            board[new_x][new_y] = -1  # Backtrack
    return False

```
