### Leetcode 133: Clone Graph

#### Problem Overview
- **Goal**: Given a reference to a node in an undirected graph, return a **deep copy** (clone) of the graph.
- Each node in the graph contains a value (`val`) and a list of its neighbors (`neighbors`).

#### Key Insights
- The problem is essentially about performing a **graph traversal** (DFS/BFS) to clone each node and its neighbors.
- Use a **hashmap** to map original nodes to their cloned counterparts to avoid revisiting/cloning the same node.
![[Pasted image 20241014020108.png]]
#### Approach: DFS (Depth-First Search)
1. **Use a hashmap** to store already cloned nodes.
2. For each node, if it hasn’t been cloned yet, create a new node.
3. Recursively clone all its neighbors and add them to the new node's neighbor list.

#### Code (DFS Approach):
```cpp
class Solution {
public:
    unordered_map<Node*, Node*> cloned;  // To track cloned nodes

    Node* cloneGraph(Node* node) {
        if (!node) return nullptr;  // Empty graph case

        if (cloned.find(node) != cloned.end()) {
            return cloned[node];  // Return already cloned node
        }

        Node* newNode = new Node(node->val);  // Clone the node
        cloned[node] = newNode;

        for (auto neighbor : node->neighbors) {
            newNode->neighbors.push_back(cloneGraph(neighbor));  // Clone neighbors recursively
        }

        return newNode;
    }
};
```

#### BFS Approach:
- Similar to DFS, but instead use a queue to iterate through the graph level by level.
  
#### Time and Space Complexity:
- **Time Complexity**: `O(N + E)`
- **Space Complexity**: `O(N)` for storing the cloned nodes and the recursion/queue.

---

#### Key Takeaway:
- The **hashmap** is crucial to ensure each node is cloned only once and to avoid infinite loops in cyclic graphs.