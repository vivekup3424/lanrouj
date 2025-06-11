
**Dijkstra's Algorithm** is a popular algorithm used for finding the shortest path from a starting node to all other nodes in a graph. The graph can be either directed or undirected, but **all edges must have non-negative weights.**

#### Key Concepts:

1. **Graph Representation**: The graph is usually represented as an adjacency list or adjacency matrix. Dijkstra's algorithm is most commonly implemented using an adjacency list.
2. **Priority Queue**: A priority queue (or min-heap) is used to always expand the node with the current smallest tentative distance.
3. **Relaxation**: The algorithm repeatedly updates the shortest distance of each node based on its neighbors.

#### Steps of Dijkstra's Algorithm:

1. **Initialization**:
    - Set the distance of the source node to 0 and all other nodes to infinity (`inf`).
    - Add all nodes to the priority queue, initially using the distances as priorities.
2. **Relaxation**:
    - While the priority queue is not empty:
        - Extract the node with the smallest distance.
        - For each neighbor of this node, if the tentative distance through this node is smaller than the current known distance, update the distance.
3. **Termination**:
    - The algorithm terminates when the priority queue is empty, meaning all nodes have been processed and the shortest paths have been found.

#### Time Complexity:

- The time complexity of Dijkstra’s algorithm is $O(Elog⁡V)$, where E is the number of edges and V is the number of vertices. This assumes the use of a priority queue implemented as a binary heap.

---

### Dijkstra's Algorithm Code in Python

```python
import heapq

def dijkstra(graph, start):
    # Initialize the distances to all nodes as infinity, except the start node
    distances = {node: float('inf') for node in graph}
    distances[start] = 0
    
    # Create a priority queue and add the start node with a distance of 0
    priority_queue = [(0, start)]  # (distance, node)
    
    # Keep track of the shortest path to each node
    while priority_queue:
        # Get the node with the smallest distance
        current_distance, current_node = heapq.heappop(priority_queue)
        
        # Skip this node if we have already found a shorter path
        if current_distance > distances[current_node]:
            continue
        
        # Explore the neighbors of the current node
        for neighbor, weight in graph[current_node]:
            distance = current_distance + weight
            
            # If a shorter path to the neighbor is found, update the distance and add to the queue
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                heapq.heappush(priority_queue, (distance, neighbor))
    
    return distances

# Example usage:
graph = {
    'A': [('B', 1), ('C', 4)],
    'B': [('A', 1), ('C', 2), ('D', 5)],
    'C': [('A', 4), ('B', 2), ('D', 1)],
    'D': [('B', 5), ('C', 1)]
}

start_node = 'A'
shortest_paths = dijkstra(graph, start_node)
print(f"Shortest distances from {start_node}: {shortest_paths}")
```

#### Explanation:

- **Graph Representation**: The graph is represented as a dictionary of lists, where each key is a node and the value is a list of tuples, each containing a neighboring node and the weight of the edge.
    
- **Priority Queue**: The priority queue (min-heap) is implemented using Python's `heapq` library. The queue stores tuples of `(distance, node)`, where the node with the smallest distance has the highest priority.
    
- **Updating Distances**: For each node, its neighbors are checked, and if a shorter path through the current node is found, the distance is updated, and the neighbor is added to the priority queue with the updated distance.
    

#### Example Output:

```
Shortest distances from A: {'A': 0, 'B': 1, 'C': 3, 'D': 4}
```

This code calculates the shortest path from the start node to all other nodes in the graph using Dijkstra's algorithm and prints the shortest distances.