Single Source Shortest Path, with no negative cycle
#### **What is it?**
Dijkstra's Algorithm is a greedy algorithm used to find the shortest path from a source node to all other nodes in a weighted graph. It works by selecting the node with the minimum distance, updating its neighbors, and iterating until all nodes are processed.

#### **Why do we use it?**
- **Optimal Shortest Path Calculation**: 
>[!Note]
>It guarantees the shortest path from the source to all other vertices in a graph with ***non-negative edge weights.***

- **Efficient in Networks**: It's widely used in network routing protocols (e.g., OSPF, routing packets in the internet) to find the shortest route.
- **Navigation Systems**: Dijkstra's algorithm is also used in GPS systems and mapping software to find the shortest route between two points.

---

#### **Where did it come from / Real-Life Encounters:**
- **Developed by Edsger W. Dijkstra** in 1956, it is one of the foundational algorithms in graph theory.
- **Applications**:
  - **Network Routing**: Internet routing algorithms use it to find the least-cost path between devices.
  - **Transportation**: Used in maps and navigation systems to compute the shortest driving or walking routes.
  - **Telecommunications**: In telecommunication networks to find optimal data paths.
  - **AI and Robotics**: In pathfinding algorithms for AI navigation.
---

#### **How do we use it?**

1. **Data Structures**:
   - **Priority Queue (Min-Heap)**: For efficiently picking the next minimum distance vertex.
   - **Distance Array**: To keep track of the shortest distance from the source to each vertex.
   - **Graph Representation**: Typically represented as an adjacency list.

2. **Steps**:
   - Initialize distances from the source to all vertices as infinity (`INF`), except for the source itself (set to `0`).
   - Use a priority queue to repeatedly extract the vertex with the smallest known distance.
   - For each neighboring vertex, update its distance if a shorter path is found via the current vertex.
   - Repeat the process until all vertices are processed.
---

#### **Code Example (C++ Using Priority Queue)**:
```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> dijkstra(int V, vector<pair<int, int>> adj[], int source) {
    vector<int> dist(V, INT_MAX);
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;

    dist[source] = 0;
    pq.push({0, source});

    while (!pq.empty()) {
        int u = pq.top().second;
        int d = pq.top().first;
        pq.pop();

        for (auto& neighbor : adj[u]) {
            int v = neighbor.first;
            int weight = neighbor.second;

            if (dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
                pq.push({dist[v], v});
            }
        }
    }

    return dist; // Distances from source to all vertices
}

int main() {
    int V = 5;
    vector<pair<int, int>> adj[V];

    // Example graph
    adj[0].push_back({1, 9});
    adj[0].push_back({2, 6});
    adj[0].push_back({3, 5});
    adj[0].push_back({4, 3});
    adj[2].push_back({1, 2});
    adj[2].push_back({3, 4});

    vector<int> distances = dijkstra(V, adj, 0);

    for (int i = 0; i < V; i++) {
        cout << "Distance to node " << i << ": " << distances[i] << endl;
    }

    return 0;
}
```
---

### **Key Points**:
- **Input**: A graph (adjacency list), number of vertices, and a source node.
- **Output**: The shortest distances from the source node to all other nodes.
- **Greedy Approach**: It selects the closest unvisited node and updates the distances of its neighbors.
- **Time Complexity**: \(O(E \log V)\), where \(E\) is the number of edges and \(V\) is the number of vertices.
- **Space Complexity**: \(O(V + E)\) due to the storage of the graph and distance array.

### **Conclusion**:
Dijkstra's algorithm is fundamental for shortest path calculations in weighted graphs and is widely applicable in networking, AI, and transportation problems. It efficiently handles graphs with non-negative weights using a priority queue for optimal performance.