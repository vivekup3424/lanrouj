### **Breadth-First Search (BFS)**

#### **What is it?**
BFS is an algorithm that traverses graphs or trees level by level, using a queue to explore nodes layer by layer.

#### **Why use it?**
BFS finds the shortest path in an unweighted graph and ensures all nodes are explored level by level.

#### **Real-life Use:**
- **Web Crawlers**: Exploring websites and pages level by level.
- **Social Networks**: Finding friends or connections within a given number of degrees of separation.
- **Network Routing**: Finding the shortest path for data packets in networks.
- **AI/Game Development**: For pathfinding algorithms (e.g., in maze-solving or game level navigation).
- **Flood-Fill Algorithms**: Used in image processing (e.g., paint bucket tool in image editing software).

#### **How to use it (in C++):**

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

void BFS(int start, const vector<vector<int>>& graph) {
    vector<bool> visited(graph.size(), false);
    queue<int> q;
    
    q.push(start);
    visited[start] = true;
    
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        cout << node << " ";
        
        for (int neighbor : graph[node]) {
            if (!visited[neighbor]) {
                q.push(neighbor);
                visited[neighbor] = true;
            }
        }
    }
}

int main() {
    vector<vector<int>> graph = {
        {1, 2},   // Neighbors of node 0
        {0, 3, 4},// Neighbors of node 1
        {0, 4},   // Neighbors of node 2
        {1},      // Neighbors of node 3
        {1, 2}    // Neighbors of node 4
    };
    
    BFS(0, graph); // Start BFS from node 0
    return 0;
}
```

This code traverses the graph starting from node `0` and prints the nodes visited in BFS order.
*Linked Problems*
[[Word Break]]
[[Word Ladder]]
### **DFS (Depth First Traversal)**

#### **What is it?**
Depth-First Search (DFS) is an algorithm used to traverse or search through graph or tree structures. DFS explores as far as possible along each branch before backtracking, using a stack (or recursion) to keep track of nodes.

#### **Why use it?**
DFS is used to explore all nodes of a graph or tree and is particularly useful when solving problems involving 
1. pathfinding, 
2. cycle detection, 
3. topological sorting, and 
4. connectivity.

#### **Real-life Use:**
- **Maze/Path Solving**: Exploring all possible paths in a maze.
- **Backtracking Algorithms**: In puzzles like Sudoku or N-Queens.
- **Web Crawlers**: Traversing the web in a depth-first manner.

#### **How to use it (in C++):**

```cpp
#include <iostream>
#include <vector>

using namespace std;

void DFS(int node, const vector<vector<int>>& graph, vector<bool>& visited) {
    visited[node] = true;
    cout << node << " ";

    for (int neighbor : graph[node]) {
        if (!visited[neighbor]) {
            DFS(neighbor, graph, visited);
        }
    }
}

void DFS_Iterative(int start, const vector<vector<int>>& graph) {
    vector<bool> visited(graph.size(), false);
    stack<int> s;
    
    s.push(start);
    
    while (!s.empty()) {
        int node = s.top();
        s.pop();
        
        if (!visited[node]) {
            cout << node << " ";
            visited[node] = true;
        }
        
        // Explore the neighbors in reverse order to mimic recursion order.
        for (auto it = graph[node].rbegin(); it != graph[node].rend(); ++it) {
            if (!visited[*it]) {
                s.push(*it);
            }
        }
    }
}

```

This code explores all nodes starting from node `0` in DFS order, visiting each node once.

*Linked Problems*
1. [[Clone Graph]]
3. [[Course Schedule]]