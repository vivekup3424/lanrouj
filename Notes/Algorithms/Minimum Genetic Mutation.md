## Problem Description

In the "Minimum Genetic Mutation" problem, we are given:

- A start gene string and an end gene string (both 8 characters long)
- A bank of valid gene strings
- We need to find the minimum number of mutations needed to mutate from the start to the end gene

A mutation involves changing one character in the gene. Each mutation must result in a valid gene string that exists in the bank.

If such a mutation sequence is impossible, return -1.

## Key Insights

1. This is essentially a **shortest path problem** in a graph where:
    
    - Nodes are gene strings
    - Edges connect genes that differ by exactly one character
    - We want the shortest path from start to end gene
2. The problem constraints make it manageable:
    
    - Gene strings are only 8 characters long
    - Each position can only be 'A', 'C', 'G', or 'T'

## Solution Approach: Breadth-First Search (BFS)

BFS is ideal for this problem because:

- It explores all possible paths level by level
- Guarantees the first path found is the shortest
- Works well for unweighted graphs (each mutation has cost = 1)

## Algorithm Steps

1. **Create a queue** and initialize it with the start gene
2. **Initialize a visited set** to track genes we've already processed
3. **Initialize a level counter** to track the number of mutations
4. **While the queue is not empty**:
    - Process all genes at the current level
    - For each gene at this level, try all possible mutations
    - If a mutation results in a valid gene in the bank, add to queue
    - If we find the end gene, return the current level
5. **If we exhaust all possibilities** without finding the end gene, return -1

## Code Implementation

```python
from collections import deque

def minMutation(start: str, end: str, bank: list[str]) -> int:
    bank_set = set(bank)
    if end not in bank_set:
        return -1
    gene_chars = ['A', 'C', 'G', 'T']
    queue = deque([(start, 0)])
    visited = {start}
    
    while queue:
        current_gene, mutations = queue.popleft()
        
        # If we've reached the end gene, return the mutation count
        if current_gene == end:
            return mutations
        
        # Try all possible one-character mutations
        for i in range(len(current_gene)):
            # Try replacing this position with each possible character
            for char in gene_chars:
                if char != current_gene[i]:
                    # Create the new mutated gene
                    mutated_gene = current_gene[:i] + char + current_gene[i+1:]
                    
                    # If mutation is valid and not visited
                    if mutated_gene in bank_set and mutated_gene not in visited:
                        visited.add(mutated_gene)
                        queue.append((mutated_gene, mutations + 1))
    
    # If we can't reach the end gene
    return -1
```

## Time and Space Complexity

- **Time Complexity**: O(L × N × 4)
    
    - L = length of gene string (8 in this problem)
    - N = number of genes in the bank
    - 4 = number of possible characters at each position
    - For each gene, we try L positions with 4 characters each
- **Space Complexity**: O(N)
    
    - We store at most N genes in our queue and visited set

## Common Variations and Follow-up Questions

1. **What if gene strings are longer?**
    
    - The solution approach remains the same, but efficiency becomes more important
    - Consider using a character-based adjacency list instead of trying all mutations
2. **What if we want all shortest paths, not just one?**
    
    - Modify BFS to continue exploring the current level even after finding the end gene
    - Use backtracking to reconstruct all paths
3. **What if mutations have different costs?**
    
    - Switch from BFS to Dijkstra's algorithm for weighted graphs