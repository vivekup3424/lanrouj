![[Pasted image 20241221125700.png]]
2. [[maximum-number-of-k-divisible-component.excalidraw]]
Editorial
To solve this problem, let’s consider how the structure of a tree can help us.

A tree consists of nodes connected by edges, and each edge connects a parent node to one of its children. Once we pick a node as the root, we can break the tree down into smaller parts, called subtrees, based on the parent-child relationships. The tree is undirected, so we can choose any node to be the root without affecting the result.

Now, let’s think about how we can use recursion to solve this. We want to calculate the sum of each subtree. After calculating the sum, we need to check: _Is this sum divisible by k?_ If it is, we can detach the subtree at that point because it forms a valid component.

But what if the sum isn’t divisible by k? In that case, we need to "carry over" the remainder (the leftover part when divided by k) to the parent node. This way, the parent node can combine its remainder with its children's remainders to check if the total sum becomes divisible by k. This recursive process naturally fits a Depth-First Search (DFS) approach:

1. Start from the leaves of the tree (the smallest subtrees) and compute their sums.
2. Propagate the results up to their parent nodes, adding up the remainders modulo k.
3. Whenever a subtree's sum is divisible by k, count it as a valid component.

```python

from collections import defaultdict
class Solution:
    def dfs(self, graph, values, source, visited, k):
        if source in visited:
            return 0
        visited.add(source)
        total_subtree_value = 0
        for neighbor in graph[source]:
            total_subtree_value += self.dfs(graph, values, neighbor, visited, k)
        total_subtree_value += values[source]
        if total_subtree_value % k == 0:
            self.count += 1
            return 0
        return total_subtree_value
    def maxKDivisibleComponents(self, n: int, edges: list[list[int]], values: list[int], k: int) -> int:
        graph = defaultdict(set)
        for edge in edges:
            graph[edge[0]].add(edge[1])
            graph[edge[1]].add(edge[0])
        visited = set()
        self.count = 0
        self.dfs(graph, values, 0, visited, k)
        return self.count
```


### Approach 2: Breadth-First Search (BFS)

#### Intuition

Instead of using Depth-First Search (DFS) to build the solution from the bottom up, we can approach the problem in a different way: what if we process the tree layer by layer? This means we start with the simplest parts of the tree — the leaf nodes — and work our way up.

A leaf node is a node that has only one neighbor, which makes it easy to handle because it doesn’t depend on any other parts of the tree once it’s processed. If a leaf node’s value is divisible by k, it can immediately form a valid component. If it’s not, its value is added to its parent’s sum. This leads to the insight that:

- We can iteratively remove processed leaf nodes, reducing the tree layer by layer.
- As we remove a leaf node, we update its parent with the carry-over sum (modulo k).

This iterative process naturally fits a Breadth-First Search (BFS) approach:

1. Start with all the leaf nodes, as they are the simplest to process.
2. Remove each leaf node, updating its parent node’s value with the carry-over sum.
3. If the parent node becomes a new leaf (i.e., it now has only one remaining neighbor), add it to the processing queue and repeat the process.
```python
class Solution:
    def maxKDivisibleComponents(
        self, n: int, edges: List[List[int]], values: List[int], k: int
    ) -> int:
        # Base case: if there are less than 2 nodes, return 1
        if n < 2:
            return 1
        component_count = 0
        graph = defaultdict(set)

        # Step 1: Build the graph
        for node1, node2 in edges:
            graph[node1].add(node2)
            graph[node2].add(node1)

        # Step 2: Initialize the BFS queue with leaf nodes (nodes with only one connection)
        queue = deque(
            node for node, neighbors in graph.items() if len(neighbors) == 1
        )

        # Step 3: Process nodes in BFS order
        while queue:
            current_node = queue.popleft()
            neighbor_node = (
                next(iter(graph[current_node])) if graph[current_node] else -1
            )

            # Remove the edge between current and neighbor
            if neighbor_node >= 0:
                graph[neighbor_node].remove(current_node)

            # Check divisibility of the current node's value
            if values[current_node] % k == 0:
                component_count += 1
            else:
                values[neighbor_node] += values[current_node]

            # If the neighbor becomes a leaf node, add it to the queue
            if neighbor_node >= 0 and len(graph[neighbor_node]) == 1:
                queue.append(neighbor_node)

        return component_count

```

