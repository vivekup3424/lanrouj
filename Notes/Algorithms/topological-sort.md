### Topological Sorting

**What is it?**
Topological sorting is a linear ordering of vertices in a directed graph where for every directed edge `u → v`, vertex `u` appears before vertex `v` in the ordering. Topological sorting is applicable only to Directed Acyclic Graphs (DAGs), as cycles prevent a strict ordering of vertices.

**Why do we use it?**
Topological sorting is useful in scenarios where certain tasks or dependencies need to be completed in a specific order. For example:
- **Task scheduling**: Ensuring that prerequisites are completed before tasks.
- **Compilation order**: Determining which code modules need to be compiled before others.
- **Course prerequisite resolution**: Ensuring courses are taken in the correct sequence.

**Where did it come from?**
Topological sorting is derived from graph theory and is a foundational concept for solving dependency-related problems in computer science. It is used extensively in systems that manage dependency chains or directed workflows.

**Implementations of Topological Sorting**

1. **DFS (Depth-First Search)-based Topological Sort**
2. **Kahn's Algorithm (BFS-based Topological Sort)**

---

### 1. DFS-based Topological Sort

**How it works**:
- Perform a Depth-First Search on each node.
- As nodes complete all recursive DFS calls, push them onto a stack (or a list).
- The stack represents the reverse of the topological order, so popping all elements in stack order provides the topological ordering.

**Steps**:
1. Initialize an empty stack and a visited set.
2. For each unvisited vertex, perform DFS:
   - For each neighbor, recursively call DFS if unvisited.
   - Push the node to the stack after all neighbors are visited.
3. Pop all elements from the stack to get the topological order.

**Code Example**:

```cpp
#include <iostream>
#include <vector>
#include <stack>
using namespace std;

void dfs(int node, vector<int> adj[], vector<bool>& visited, stack<int>& st) {
    visited[node] = true;
    for (int neighbor : adj[node]) {
        if (!visited[neighbor]) {
            dfs(neighbor, adj, visited, st);
        }
    }
    st.push(node);
}

vector<int> topologicalSortDFS(int V, vector<int> adj[]) {
    stack<int> st;
    vector<bool> visited(V, false);

    for (int i = 0; i < V; i++) {
        if (!visited[i]) {
            dfs(i, adj, visited, st);
        }
    }

    vector<int> topologicalOrder;
    while (!st.empty()) {
        topologicalOrder.push_back(st.top());
        st.pop();
    }
    return topologicalOrder;
}
```

**Time Complexity**: \(O(V + E)\), where \(V\) is the number of vertices and \(E\) is the number of edges.

**Space Complexity**: \(O(V)\) for the visited array and stack.

**Pros**:
- Easy to implement and understand.
- Efficient for dense graphs.

**Cons**:
- DFS-based approach does not inherently detect cycles; you would need additional logic for that.

---

### 2. Kahn's Algorithm (BFS-based Topological Sort)

**How it works**:
- Uses in-degree (number of incoming edges) to identify nodes with zero in-degree as starting points.
- Process nodes with zero in-degree, then remove each node from the graph, decrementing the in-degree of its neighbors.
- Continue until all nodes are processed or a cycle is detected.

**Steps**:
1. Calculate the in-degree for each node.
2. Add nodes with zero in-degree to a queue.
3. While the queue is not empty:
   - Remove the front node and add it to the topological order.
   - Decrement the in-degree of all its neighbors.
   - If any neighbor’s in-degree becomes zero, add it to the queue.
4. If the topological order contains all nodes, return it; otherwise, a cycle exists.

**Code Example**:

```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

vector<int> topologicalSortKahn(int V, vector<int> adj[]) {
    vector<int> indegree(V, 0), topologicalOrder;
    queue<int> zeroIndegree;

    for (int i = 0; i < V; i++) {
        for (int neighbor : adj[i]) {
            indegree[neighbor]++;
        }
    }

    for (int i = 0; i < V; i++) {
        if (indegree[i] == 0) {
            zeroIndegree.push(i);
        }
    }

    while (!zeroIndegree.empty()) {
        int node = zeroIndegree.front();
        zeroIndegree.pop();
        topologicalOrder.push_back(node);

        for (int neighbor : adj[node]) {
            if (--indegree[neighbor] == 0) {
                zeroIndegree.push(neighbor);
            }
        }
    }

    return (topologicalOrder.size() == V) ? topologicalOrder : vector<int>(); // empty vector if cycle
}
```

**Time Complexity**: \(O(V + E)\)

**Space Complexity**: \(O(V)\) for the in-degree array and queue.

**Pros**:
- Simple and effective for detecting cycles.
- Useful in sparse graphs due to its queue-based approach.

**Cons**:
- May be slightly less intuitive compared to DFS for some.

---

### Differences Between DFS-based and Kahn’s Algorithm

| Feature                  | DFS-based Topological Sort               | Kahn’s Algorithm (BFS-based)     |
|--------------------------|------------------------------------------|----------------------------------|
| Approach                 | Depth-First Search                       | Breadth-First Search             |
| Cycle Detection          | Requires additional logic                | Detects cycles naturally         |
| Suitable Graph Density   | Dense graphs                            | Sparse graphs                    |
| Complexity               | \(O(V + E)\)                            | \(O(V + E)\)                     |
| Usage                    | Simple ordering                          | Both ordering and cycle detection|

---

### Real-World Applications
- **Build Systems**: Determining the order in which code files or modules should be compiled.
- **Task Scheduling**: Organizing tasks with dependencies (e.g., project management software).
- **Package Management**: Ensuring packages with dependencies are installed in the correct order.
- **Course Scheduling**: Determining the correct order for students to complete course prerequisites.

### Summary
- **Topological Sort** is a linear ordering for tasks with dependencies.
- **DFS-based approach** is easy to implement but requires additional logic for cycle detection.
- **Kahn's Algorithm** is efficient, naturally detects cycles, and works well for sparse graphs.

### Questions
1.[[alien-dictionary]]
