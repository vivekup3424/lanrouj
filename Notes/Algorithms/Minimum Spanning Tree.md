### **Minimum Spanning Tree (MST) - Obsidian Notes**

#### **1. What is a Minimum Spanning Tree (MST)?**
A **Minimum Spanning Tree (MST)** is a subset of the edges in a **connected, undirected, weighted graph** that connects all the vertices with the minimum possible total edge weight. It does not contain any cycles, and it always includes exactly **V-1 edges**, where V is the number of vertices.

---

#### **2. Why do we use MST?**
- **Cost-efficient networking**: MST is used to design networks (like computer, telephone, or road networks) that minimize the cost of connecting multiple points.
- **Approximation Algorithms**: MST serves as a basis for approximation algorithms, such as those used in the **Travelling Salesman Problem (TSP)**.
- **Clustering**: MST can help in clustering data points by creating trees that connect the closest points.

---

#### **3. Where did MST come from / Real-life Usage?**
- **Origins**: The MST problem has been studied for decades, and various algorithms have been developed to solve it efficiently. Algorithms like **Kruskal’s** and **Prim’s** are named after their creators.
- **Real-life Applications**:
  - **Network design**: Building communication, electrical, or road networks at the lowest cost.
  - **Biology**: Analyzing evolutionary trees in bioinformatics.
  - **Image Processing**: MST is used to define regions in image segmentation tasks.
  - **Civil Engineering**: Designing transportation or water pipeline systems.

---

#### **4. How do we find an MST?**
There are several algorithms to find the MST in a graph:

- **[[Prim's]] Algorithm**:
  - A **greedy** algorithm that starts from an arbitrary vertex and grows the MST by adding the smallest edge that connects the current MST to a new vertex.
  - Efficient for **dense graphs**.

- **[[Kruskal's]] Algorithm**:
  - A **greedy** algorithm that sorts all edges by weight and adds the smallest edge to the MST, ensuring that no cycles are formed.
  - Efficient for **sparse graphs**.
  - Typically uses a **Disjoint Set Union (DSU)** data structure to detect cycles.

- **Borůvka’s Algorithm**:
  - It finds MST by repeatedly adding the smallest edge from each connected component until all vertices are included.
  - Useful in parallel and distributed environments.

---

#### **5. Common MST Algorithms - Code Examples**

##### **Kruskal’s Algorithm - C++**

```cpp
#include <bits/stdc++.h>
using namespace std;

class DSU {
private:
    vector<int> parent, size;

public:
    DSU(int n) {
        parent.resize(n);
        size.resize(n, 1);
        iota(parent.begin(), parent.end(), 0);
    }

    int find(int a) {
        if (parent[a] != a) 
            parent[a] = find(parent[a]);
        return parent[a];
    }

    void unionNodes(int u, int v) {
        int rootU = find(u), rootV = find(v);
        if (rootU == rootV) return;
        if (size[rootU] < size[rootV]) {
            parent[rootU] = rootV;
            size[rootV] += size[rootU];
        } else {
            parent[rootV] = rootU;
            size[rootU] += size[rootV];
        }
    }
};

int kruskalMST(int V, vector<vector<int>>& edges) {
    DSU dsu(V);
    sort(edges.begin(), edges.end(), [](auto &a, auto &b) {
        return a[2] < b[2]; // Sort by edge weight
    });

    int mstCost = 0, edgesUsed = 0;
    for (auto& edge : edges) {
        if (dsu.find(edge[0]) != dsu.find(edge[1])) {
            dsu.unionNodes(edge[0], edge[1]);
            mstCost += edge[2];
            edgesUsed++;
        }
        if (edgesUsed == V - 1) break;
    }
    return mstCost;
}
```

##### **Prim’s Algorithm - C++**

```cpp
#include <bits/stdc++.h>
using namespace std;

int primMST(int V, vector<vector<pair<int, int>>>& adj) {
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    vector<int> key(V, INT_MAX);
    vector<bool> inMST(V, false);
    int mstCost = 0;

    pq.push({0, 0});
    key[0] = 0;

    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();
        if (inMST[u]) continue;
        inMST[u] = true;
        mstCost += key[u];

        for (auto &[weight, v] : adj[u]) {
            if (!inMST[v] && weight < key[v]) {
                key[v] = weight;
                pq.push({key[v], v});
            }
        }
    }

    return mstCost;
}
```

---

#### **6. Frequently Asked Interview Questions on MST**

1. **What is the difference between Prim’s and Kruskal’s algorithms?**
   - Prim’s algorithm grows the MST by selecting the smallest edge connected to the current tree, whereas Kruskal’s algorithm starts by sorting all edges and adds the smallest edge while ensuring no cycles.
   - Prim’s is better for **dense graphs** (lots of edges), while Kruskal’s is better for **sparse graphs**.

2. **How does Kruskal’s algorithm detect cycles?**
   - Kruskal’s algorithm uses the **Disjoint Set Union (DSU)** data structure, also known as **Union-Find**, to detect cycles. If two vertices are already in the same connected component, adding an edge between them would form a cycle.

3. **What is the time complexity of Prim’s and Kruskal’s algorithms?**
   - **Prim’s Algorithm**:
     - Using a priority queue (min-heap): **O(E log V)**, where E is the number of edges and V is the number of vertices.
   - **Kruskal’s Algorithm**:
     - Sorting edges takes **O(E log E)**, and using DSU takes approximately **O(α(V))**, where α is the inverse Ackermann function (very slow-growing, almost constant in practice). Overall complexity: **O(E log E)**.

4. **Can MST algorithms work on directed graphs?**
   - No, MST algorithms like Prim’s and Kruskal’s only work on **undirected graphs**. For directed graphs, the **minimum spanning arborescence** (or minimum cost branching) algorithms are used instead.

5. **Why is Prim’s algorithm better for dense graphs, while Kruskal’s is better for sparse graphs?**
   - In Prim’s algorithm, the priority queue only stores vertices, making it scale better when there are many edges (**dense graph**). Kruskal’s algorithm sorts all edges first, so it works better when there are fewer edges (**sparse graph**).

6. **What are some real-world applications of MST?**
   - **Network Design**: Telecommunication, electrical grids, or transportation networks.
   - **Clustering Algorithms**: MST is used in clustering analysis in machine learning.
   - **Approximation Algorithms**: MST is often used as a subroutine in other algorithms, such as approximations for NP-hard problems like the **Travelling Salesman Problem (TSP)**.

7. **Can an MST be unique?**
   - Yes, an MST can be unique if all edge weights are distinct. However, if there are edges with the same weights, there could be multiple valid MSTs.

---

#### **7. Time Complexity Overview**
- **Prim’s Algorithm**: O(E log V) with a priority queue.
- **Kruskal’s Algorithm**: O(E log E) due to edge sorting.
