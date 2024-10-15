### **Prim’s Algorithm - Obsidian Notes**

#### **1. What is Prim's Algorithm?**
Prim's Algorithm is a **greedy algorithm** used to find the **Minimum Spanning Tree (MST)** for a weighted, connected, and undirected graph. The MST is a subset of the graph that includes all vertices with the minimum possible total edge weight and no cycles.

Prim’s algorithm grows the MST one vertex at a time, starting from an arbitrary vertex and continuously adding the smallest possible edge that connects a vertex in the MST to a vertex outside it.

---

#### **2. Why do we use Prim's Algorithm?**
- **Efficiency**: Prim's algorithm is particularly efficient for dense graphs where many edges exist. It's useful in scenarios where you need to connect different points with the least cost, such as:
  - **Network design**: Laying cables or connecting points (cities, computers) at minimal cost.
  - **Telecommunications**: Efficiently connecting multiple hubs or nodes.
  - **Road networks**: Finding the shortest way to connect cities without forming loops.

---

#### **3. Where did it come from / real-life usage?**
- **Origin**: Prim’s algorithm was originally discovered by Czech mathematician **Vojtěch Jarník** in 1930 and later rediscovered by **Robert C. Prim** in 1957.
- **Real-life applications**:
  - **Network Design**: Minimizing the cost of linking multiple locations in telecoms or infrastructure projects.
  - **Clustering**: Prim’s algorithm can be used in unsupervised learning to cluster data points by connecting similar points (via edge weights).
  - **Approximation Algorithms**: It forms the basis for approximation algorithms for problems like the **Steiner Tree problem**.

---

#### **4. How do we use Prim's Algorithm?**

##### **Steps to Implement Prim’s Algorithm**:
1. **Start** from an arbitrary vertex and mark it as part of the MST.
2. **Find the minimum edge** that connects a vertex in the MST to a vertex outside the MST.
3. **Add that vertex** to the MST.
4. **Repeat** until all vertices are included in the MST.

---

##### **Key Points**:
- **Greedy approach**: At each step, we select the minimum weight edge that connects the MST with a vertex outside it.
- **Priority Queue/Min-Heap**: Prim's algorithm can be efficiently implemented using a **priority queue** (min-heap) to quickly select the minimum weight edge.

---

#### **5. Prim's Algorithm - C++ Code Example:**

```cpp
#include <bits/stdc++.h>
using namespace std;

typedef pair<int, int> pii; // (weight, vertex)

// Function to perform Prim's algorithm
int primMST(int V, vector<vector<pii>>& adjList) {
    priority_queue<pii, vector<pii>, greater<pii>> pq;  // Min-heap priority queue
    vector<int> key(V, INT_MAX);  // Minimum edge weight to include each vertex
    vector<bool> inMST(V, false); // Track vertices included in MST
    int start = 0;
    
    pq.push({0, start});  // Start with vertex 0
    key[start] = 0;
    int mstCost = 0;
    
    while (!pq.empty()) {
        int u = pq.top().second;  // Get vertex with minimum edge weight
        pq.pop();
        
        if (inMST[u]) continue;  // Skip if already in MST
        inMST[u] = true;         // Mark it as included
        mstCost += key[u];       // Add edge weight to total cost
        
        // Explore the adjacent vertices of 'u'
        for (auto& [weight, v] : adjList[u]) {
            if (!inMST[v] && weight < key[v]) {
                key[v] = weight;    // Update minimum edge weight for vertex 'v'
                pq.push({key[v], v}); // Push it to the priority queue
            }
        }
    }
    
    return mstCost;  // Total cost of the MST
}

int main() {
    int V = 5;
    vector<vector<pii>> adjList(V);
    
    // Graph in the form of adjacency list (u -> (weight, v))
    adjList[0] = {{2, 1}, {3, 3}, {6, 2}};
    adjList[1] = {{2, 0}, {5, 2}, {4, 3}};
    adjList[2] = {{6, 0}, {5, 1}, {8, 3}, {7, 4}};
    adjList[3] = {{3, 0}, {4, 1}, {8, 2}, {9, 4}};
    adjList[4] = {{7, 2}, {9, 3}};

    int mstCost = primMST(V, adjList);
    cout << "Total cost of MST: " << mstCost << endl;
    
    return 0;
}
```

---

#### **6. Summary:**
- **Prim's Algorithm** grows the Minimum Spanning Tree (MST) one vertex at a time by selecting the smallest possible edge.
- It is optimal for dense graphs and ensures the minimum cost to connect all vertices.
- **Key Features**:
  - **Greedy approach**.
  - Use of a **priority queue** to select minimum edges efficiently.
- **Real-world applications** include network design, road construction, and clustering in data analysis.

---

#### **7. Time Complexity:**
- **Using priority queue (Min-Heap)**: The time complexity is **O(E log V)**, where E is the number of edges, and V is the number of vertices.