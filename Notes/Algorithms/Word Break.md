### **Word Break Problem**

#### **What is it?**
The Word Break problem is a classic algorithmic challenge where you are given a string `s` and a list (or dictionary) of words. The task is to determine if `s` can be segmented into a space-separated sequence of one or more dictionary words.

#### **Why do we use it?**
The Word Break problem is often used to:
- Test understanding of dynamic programming and string manipulation.
- Solve problems in natural language processing (NLP), such as tokenization.
- Implement features in applications like spell checkers, auto-completion, and text segmentation.

#### **Real-life Use Cases:**
- **Text Processing**: Splitting continuous text into recognizable words for search engines and chatbots.
- **Spell Checkers**: Verifying if a string can be formed using valid words from a dictionary.
- **Natural Language Processing**: Tokenizing text for analysis, translation, or understanding.

#### **How to Approach the Problem:**
There are several methods to solve the Word Break problem, including:

1. **Dynamic Programming**:
   - Use a boolean array `dp` where `dp[i]` indicates whether the substring `s[0:i]` can be segmented into dictionary words.
   - Iterate through the string, checking each possible end index and validating against the dictionary.

2. **Backtracking**:
   - Explore all possible partitions recursively, checking if each substring exists in the dictionary.
   - If a valid partition is found, return true; otherwise, backtrack.

3. **Breadth-First Search (BFS)**:
   - Use a queue to explore possible segments of the string, checking if they exist in the dictionary.
   - Track visited indices to avoid reprocessing.

#### **Example of Dynamic Programming Approach (in C++):**

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>
using namespace std;

class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        unordered_set<string> wordSet(wordDict.begin(), wordDict.end());
        vector<bool> dp(s.length() + 1, false);
        dp[0] = true;  // Base case: empty string can always be segmented

        for (int i = 1; i <= s.length(); i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && wordSet.count(s.substr(j, i - j))) {
                    dp[i] = true;
                    break;  // No need to check further
                }
            }
        }

        return dp[s.length()];  // Result for the full string
    }
};
```


#### **My BFS Approach:**
2024-10-14
Initially I thought of this code
```cpp
    bool wordBreak(string s, vector<string>& wordDict) {
        queue<int> q;
        q.push(0);
        while(!q.empty()){
            int idx = q.front();
            if(idx==s.length()){
                return true;
            }
            q.pop();
            for(auto word: wordDict){
                int l = word.length();
                if(s.substr(idx,l)==word){
                    q.push(idx+l);
                }
            }
        }
        return false;
    }

```
> [!WARNING]
> but this one causes TLE, because of not using a visited hashset

> [!NOTE]
> For now I am going to solve word ladder, will come to this problem again.

### **Key Points:**
- **Input**: A string `s` and a list of words (`wordDict`).
- **Output**: A boolean value indicating if the string can be segmented.
- **Complexity**:
  - **Time Complexity**: \(O(n^2 \cdot m)\), where \(n\) is the length of `s`, and \(m\) is the average length of the words in the dictionary.
  - **Space Complexity**: \(O(n)\) for the `dp` array or `visited` array used in other approaches.

### **Conclusion**
The Word Break problem is a useful exercise in understanding string manipulation, dynamic programming, and recursion. It has practical applications in various fields, including text processing and natural language understanding.
