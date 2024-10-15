derived from [[DSU]]
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
