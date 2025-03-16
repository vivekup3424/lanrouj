
#### **1. Introduction to Shortest Path Algorithms**
Shortest path algorithms are used to find the minimum path between two nodes in a graph. They are crucial in various fields such as network design, GPS navigation, and AI-based pathfinding. Different algorithms are suited to different kinds of graphs (weighted/unweighted, directed/undirected).

---

#### **2. [[Djikstra's]]**
- **What is it?** A greedy algorithm to find the shortest path from a source node to all other nodes in a graph with non-negative weights.
- **Time Complexity:** \(O(E \log V)\), where \(E\) is the number of edges and \(V\) is the number of vertices.
- **Use Cases:**
  - **Network routing protocols** (e.g., OSPF).
  - **GPS navigation systems** for shortest route calculations.
  
##### **Code Example (C++)**:
```cpp
vector<int> dijkstra(int V, vector<pair<int, int>> adj[], int source) {
    vector<int> dist(V, INT_MAX);
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    dist[source] = 0;
    pq.push({0, source});

    while (!pq.empty()) {
        int u = pq.top().second;
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
    return dist;
}
```

---

#### **3. Bellman-Ford Algorithm**
- **What is it?** A dynamic programming-based algorithm that finds the shortest path from a source to all vertices, even with negative edge weights.
- **Why use it?** Unlike Dijkstra's algorithm, it works with graphs containing negative weight edges and can detect negative weight cycles.
- **Time Complexity:** \(O(VE)\), where \(V\) is the number of vertices and \(E\) is the number of edges.
  
##### **Use Cases**:
- **Currency arbitrage detection**.
- **Routing in networks** where costs may fluctuate negatively.

##### **Code Example (C++)**:
```cpp
bool bellmanFord(int V, vector<tuple<int, int, int>> edges, int source) {
    vector<int> dist(V, INT_MAX);
    dist[source] = 0;

    for (int i = 1; i < V; i++) {
        for (auto& [u, v, w] : edges) {
            if (dist[u] != INT_MAX && dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
            }
        }
    }

    // Check for negative-weight cycles
    for (auto& [u, v, w] : edges) {
        if (dist[u] != INT_MAX && dist[u] + w < dist[v]) {
            return false; // Negative cycle found
        }
    }
    return true;
}
```

---

#### **4. Floyd-Warshall Algorithm**
- **What is it?** An all-pairs shortest path algorithm that computes shortest paths between all pairs of vertices.
- **Why use it?** It’s useful when you need the shortest paths between every pair of nodes in the graph.
- **Time Complexity:** \(O(V^3)\), where \(V\) is the number of vertices.
  
##### **Use Cases**:
- **Finding shortest paths in dense graphs**.
- **Evaluating possible paths** between every pair of nodes in a transportation or communication network.

##### **Code Example (C++)**:
```cpp
void floydWarshall(vector<vector<int>>& graph, int V) {
    vector<vector<int>> dist = graph;

    for (int k = 0; k < V; k++) {
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < V; j++) {
                if (dist[i][k] != INT_MAX && dist[k][j] != INT_MAX && dist[i][k] + dist[k][j] < dist[i][j]) {
                    dist[i][j] = dist[i][k] + dist[k][j];
                }
            }
        }
    }

    // Output shortest distance matrix
    for (int i = 0; i < V; i++) {
        for (int j = 0; j < V; j++) {
            if (dist[i][j] == INT_MAX) cout << "INF ";
            else cout << dist[i][j] << " ";
        }
        cout << endl;
    }
}
```

---

#### **5. A* Algorithm**
- **What is it?** A heuristic search algorithm that is an extension of Dijkstra’s algorithm. It uses a heuristic function to estimate the distance to the target, allowing for faster pathfinding.
- **Why use it?** A* is more efficient than Dijkstra’s algorithm in certain cases because it considers both the current shortest distance and an estimate of the remaining distance to the goal.
- **Time Complexity:** Depends on the heuristic, but it can be more efficient than Dijkstra’s in practice.
  
##### **Use Cases**:
- **Pathfinding in games and AI**.
- **Navigation systems** when you need to find the shortest route with some estimation.

---

#### **6. Johnson’s Algorithm**
- **What is it?** An algorithm for all-pairs shortest paths that works on graphs with negative weights, but no negative weight cycles.
- **Why use it?** It uses a combination of Bellman-Ford and Dijkstra’s algorithms to handle graphs with negative weights efficiently.
- **Time Complexity:** \(O(V^2 \log V + VE)\).

##### **Use Cases**:
- **Sparse graphs with negative weights**, where Floyd-Warshall is too slow.

---

### **Summary of Key Algorithms**:
| Algorithm         | Handles Negative Weights | All Pairs | Time Complexity        | Typical Use Case                     |
|-------------------|--------------------------|-----------|------------------------|--------------------------------------|
| **Dijkstra**      | No                       | No        | \(O(E \log V)\)         | GPS, network routing                 |
| **Bellman-Ford**  | Yes                      | No        | \(O(VE)\)               | Detecting negative cycles, networks  |
| **Floyd-Warshall**| Yes                      | Yes       | \(O(V^3)\)              | Dense graphs, all-pairs pathfinding  |
| **A\***           | No                       | No        | Heuristic-based         | Pathfinding in AI, navigation        |
| **Johnson**       | Yes                      | Yes       | \(O(V^2 \log V + VE)\)  | Sparse graphs, handling negative weights |

---

### **Closing Thoughts**:
- Choose **Dijkstra's** for graphs with non-negative weights and single-source shortest paths.
- Use **Bellman-Ford** when you have negative weight edges and need to detect cycles.
- For all-pairs shortest paths, use **Floyd-Warshall** for dense graphs or **Johnson's** algorithm for sparse graphs.
- For heuristic-based or goal-oriented pathfinding, use **A\*** to improve efficiency.

These algorithms are essential in many real-world applications, from routing data packets across the internet to finding the shortest path in games and navigation systems.