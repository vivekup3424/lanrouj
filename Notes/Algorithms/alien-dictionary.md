There is a new alien language that uses the English alphabet. However, the order among the letters is unknown to you.

You are given a list of strings `words` from the alien language's dictionary, where the strings in `words` are **sorted lexicographically** by the rules of this new language.

Return _a string of the unique letters in the new alien language sorted in **lexicographically increasing order** by the new language's rules._ If there is no solution, return `""`_._ If there are multiple solutions, return _**any of them**_.

**Example 1:**

**Input:** words = ["wrt","wrf","er","ett","rftt"]
**Output:** "wertf"

**Example 2:**

**Input:** words = ["z","x"]
**Output:** "zx"

**Example 3:**

**Input:** words = ["z","x","z"]
**Output:** ""
**Explanation:** The order is invalid, so return `""`.

**Constraints:**

- `1 <= words.length <= 100`
- `1 <= words[i].length <= 100`
- `words[i]` consists of only lowercase English letters.

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