```c++
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    string alienOrder(vector<string>& words) {
        unordered_map<char, unordered_set<char>> graph;
        unordered_map<char, int> indegree;
        
        // Initialize all characters in indegree map
        for (const string& word : words) {
            for (char c : word) {
                indegree[c] = 0;
            }
        }

        // Build the graph and populate the indegree map
        for (int i = 1; i < words.size(); i++) {
            string prev = words[i - 1], current = words[i];
            if (prev.size() > current.size() && prev.substr(0, current.size()) == current) {
                return ""; // Invalid case due to prefix condition
            }
            for (int j = 0; j < min(prev.size(), current.size()); j++) {
                if (prev[j] != current[j]) {
                    if (graph[prev[j]].emplace(current[j]).second) { // Only add if not already present
                        indegree[current[j]]++;
                    }
                    break; // Only the first differing character determines the order
                }
            }
        }

        // Collect nodes with zero indegree
        queue<char> start;
        for (const auto& [node, count] : indegree) {
            if (count == 0) start.push(node);
        }

        // Perform topological sort
        string answer;
        while (!start.empty()) {
            char node = start.front();
            start.pop();
            answer.push_back(node);
            for (char neighbor : graph[node]) {
                if (--indegree[neighbor] == 0) {
                    start.push(neighbor);
                }
            }
        }

        return answer.size() == indegree.size() ? answer : "";
    }
};

```