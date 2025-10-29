# Breadth First Search or BFS for a Graph

Last Updated : 26 Sep, 2024

****Breadth First Search (BFS)**** is a fundamental ****graph traversal algorithm.**** It begins with a node, then first traverses all its adjacent. Once all adjacent are visited, then their adjacent are traversed. We mainly traverse vertices level by level. 
A lot of popular graph algorithms like [[Dijkstra’s shortest path]], [[Kahn’s Algorithm]], and [[Prim’s algorithm]] are based on BFS. BFS itself can be used to detect cycle in a directed and undirected graph, find shortest path in an unweighted graph and many more problems.
## BFS from a Given Source:

The algorithm starts from a given source and explores all reachable vertices from the given source. It is similar to the [[Breadth-First Traversal of a tree]]. Like tree, we begin with the given source (in tree, we begin with root) and traverse vertices level by level using a queue data structure. The only catch here is that, unlike trees, graphs may contain cycles, so we may come to the same node again. To avoid processing a node more than once, we use a *boolean visited array.*

> [!NOTE]
> PSUEDO CODE

****Initialization:**** Enqueue the given source vertex into a queue and mark it as visited.

1. ****Exploration:**** While the queue is not empty:
    - Dequeue a node from the queue and visit it (e.g., print its value).
    - For each unvisited neighbor of the dequeued node:
        - Enqueue the neighbor into the queue.
        - Mark the neighbor as visited.
2. ****Termination:**** Repeat step 2 until the queue is empty.

This algorithm ensures that all nodes in the graph are visited in a breadth-first manner, starting from the starting node.

### How Does the BFS Algorithm Work?

![BFS-on-Graph.webp](https://media.geeksforgeeks.org/wp-content/uploads/20240924153148/BFS-on-Graph.webp)![BFS-on-Graph.webp](https://media.geeksforgeeks.org/wp-content/uploads/20240924153148/BFS-on-Graph.webp)


```c++
#include <iostream>
#include <queue>
#include <vector>
using namespace std;

void bfs(vector<vector<int>>& adj, int s) {
    vector<bool> visited(adj.size(), false);
    queue<int> q;
    visited[s] = true;
    q.push(s);

    while (!q.empty()) {
        int curr = q.front();
        q.pop();
        cout << curr << " ";

        for (int neighbor : adj[curr]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                q.push(neighbor);
            }
        }
    }
}
```

****Time Complexity:**** O(V+E), where V is the number of nodes and E is the number of edges.  
****Auxiliary Space:**** O(V)
## Complexity Analysis of Breadth-First Search (BFS) Algorithm:

### Time Complexity of BFS Algorithm: O(V + E)

- BFS explores all the vertices and edges in the graph. In the worst case, it visits every vertex and edge once. Therefore, the time complexity of BFS is O(V + E), where V and E are the number of vertices and edges in the given graph.

### Auxiliary Space of BFS Algorithm: O(V)

- BFS uses a queue to keep track of the vertices that need to be visited. In the worst case, the queue can contain all the vertices in the graph. Therefore, the space complexity of BFS is O(V).

## Applications of BFS in Graphs:

BFS has various applications in graph theory and computer science, including:

- ****Shortest Path Finding:**** BFS can be used to find the shortest path between two nodes in an unweighted graph. By keeping track of the parent of each node during the traversal, the shortest path can be reconstructed.
- ****Cycle Detection:**** BFS can be used to detect cycles in a graph. If a node is visited twice during the traversal, it indicates the presence of a cycle.
- ****Connected Components:**** BFS can be used to identify connected components in a graph. Each connected component is a set of nodes that can be reached from each other.
- ****Topological Sorting:**** BFS can be used to perform topological sorting on a directed acyclic graph (DAG). Topological sorting arranges the nodes in a linear order such that for any edge (u, v), u appears before v in the order.
- ****Level Order Traversal of Binary Trees:**** BFS can be used to perform a level order traversal of a binary tree. This traversal visits all nodes at the same level before moving to the next level.
- ****Network Routing:**** BFS can be used to find the shortest path between two nodes in a network, making it useful for routing data packets in network protocols.

## Problems on Breadth First Search or BFS for a Graph:
1. [[Minimum Genetic Mutation]]
2. 