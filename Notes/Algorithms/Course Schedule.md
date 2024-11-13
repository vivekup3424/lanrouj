
---

### Leetcode 207: Course Schedule

#### Problem Overview
- **Goal**: Determine if you can finish all courses given `numCourses` and a list of `prerequisites`, where prerequisites are directed edges in a graph.
- **Key Insight**: The problem can be reduced to cycle detection in a directed graph. If there is a cycle, it's impossible to finish all courses.
> [!NOTE]
> Similar to [[Word Ladder]] and [[Word Break]]
> I always get confused between them

#### Approach: Topological Sort (Kahn's Algorithm)
1. **Graph Representation**:  
![[courseSchedule.png]]
   - Courses are represented as nodes, and prerequisites as directed edges.
   - Use an **adjacency list** to represent the directed graph, where each node points to its prerequisites.

3. **Cycle Detection Insight**:  
   - If a cycle exists, it is impossible to complete all courses because there would be no valid order.
   - Topological sorting is useful to check for cycles. If the topological order includes all courses, no cycle exists.

4. **Algorithm Steps**:
   - **Step 1**: Build the adjacency list from `prerequisites`.
   - **Step 2**: Calculate the **in-degree** of each node (i.e., the number of prerequisites for each course).
   - **Step 3**: Initialize a queue with nodes having in-degree 0 (courses without prerequisites).
   - **Step 4**: Process each node, reducing the in-degree of its neighbors. Add neighbors to the queue when their in-degree becomes 0.
   - **Step 5**: If the topological order contains all courses, return `true` (no cycle); otherwise, return `false`.

5. **Code (C++ Kahn’s Algorithm)**:
```cpp
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> adj(numCourses);  // Adjacency list
        for (auto edge : prerequisites) {
            adj[edge[0]].push_back(edge[1]);
        }

        vector<int> indegree(numCourses, 0);  // In-degree array
        for (int i = 0; i < numCourses; i++) {
            for (auto it : adj[i]) {
                indegree[it]++;
            }
        }

        queue<int> q;
        for (int i = 0; i < numCourses; i++) {
            if (indegree[i] == 0) {
                q.push(i);
            }
        }

        vector<int> topo;  // To store topological order
        while (!q.empty()) {
            int node = q.front();
            q.pop();
            topo.push_back(node);
            for (auto it : adj[node]) {
                indegree[it]--;
                if (indegree[it] == 0) {
                    q.push(it);
                }
            }
        }

        return topo.size() == numCourses;
    }
};
```

#### Time and Space Complexity
- **Time Complexity**: `O(V + E)` where `V` is the number of courses (`numCourses`) and `E` is the number of prerequisites.
  - Building the graph and calculating in-degrees takes `O(E)`.
  - Processing each node and its edges in the topological sort takes `O(V + E)`.
  
- **Space Complexity**: `O(V + E)` to store the adjacency list and in-degree array.

#### Key Takeaways:
- The problem is equivalent to **cycle detection** in a directed graph.
- **Kahn's Algorithm** for topological sorting can efficiently detect cycles by checking if we can process all nodes (courses).
- If a node has a non-zero in-degree after topological sorting, it indicates a cycle.

---
