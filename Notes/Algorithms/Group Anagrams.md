
---

### Problem
Given an array of strings, group the strings that are anagrams of each other.

### Key Points
1. **Anagram Definition**: Two words are anagrams if they contain the same characters in the same frequency but can be in any order.
2. **Problem Goal**: Group words that are anagrams into individual lists within a result list.

### Approach
- **Hashing by Sorted Word**:
  - Sort each word and use the sorted string as the key in a hash map.
  - Append words with the same sorted version to the list corresponding to that key.
- **Hashing by Frequency Array**:
  - For each word, calculate a frequency array (size 26 for lowercase alphabets).
  - Convert this array into a tuple (or a unique string) and use it as the key in a hash map.

### Code (C++)

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
#include <algorithm>

std::vector<std::vector<std::string>> groupAnagrams(std::vector<std::string>& strs) {
    std::unordered_map<std::string, std::vector<std::string>> anagramGroups;
    
    for (const auto& word : strs) {
        std::string sortedWord = word;
        std::sort(sortedWord.begin(), sortedWord.end());
        anagramGroups[sortedWord].push_back(word);
    }
    
    std::vector<std::vector<std::string>> result;
    for (const auto& group : anagramGroups) {
        result.push_back(group.second);
    }
    return result;
}
```

### Complexity
- **Time Complexity**: \(O(N $\cdot$ M $\log$ M)\), where \(N\) is the number of strings, and \(M\) is the maximum string length.
- **Space Complexity**: \(O(N $\cdot$ M)\), for storing groups in the hash map.

### Edge Cases
- Empty string array.
- Single character words.
- Words with different cases (optional, if case-sensitive).

---

## Variants: Group Sentences by Anagram Words

### Problem Variant
Given an array of sentences, group sentences that are anagrams of each other. Here, sentences are considered anagrams if they contain the same words, regardless of order.

### Approach
- **Normalize Sentence**:
  - Split each sentence into words, sort the words, and join them back into a normalized form.
  - Use this sorted word form as a key in a hash map to group sentences.
  
### Code (C++)

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
#include <sstream>
#include <algorithm>

std::vector<std::vector<std::string>> groupSentenceAnagrams(std::vector<std::string>& sentences) {
    std::unordered_map<std::string, std::vector<std::string>> sentenceGroups;
    
    for (const auto& sentence : sentences) {
        std::istringstream ss(sentence);
        std::vector<std::string> words;
        std::string word;
        
        while (ss >> word) {
            words.push_back(word);
        }
        
        std::sort(words.begin(), words.end());
        std::string sortedSentence;
        
        for (const auto& w : words) {
            sortedSentence += w + " ";
        }
        
        sentenceGroups[sortedSentence].push_back(sentence);
    }
    
    std::vector<std::vector<std::string>> result;
    for (const auto& group : sentenceGroups) {
        result.push_back(group.second);
    }
    return result;
}
```

### Complexity
- **Time Complexity**: \(O(N \cdot M \log M)\), where \(N\) is the number of sentences, and \(M\) is the average number of words in each sentence.
- **Space Complexity**: \(O(N \cdot M)\), to store grouped sentences.

### Edge Cases
- Empty sentences.
- Sentences with identical words in different orders.
- Sentences with punctuation (if required to handle).

---

This format should help you quickly reference solutions, complexities, and edge cases for **Group Anagrams** and **Group Sentence Anagrams**. Let me know if you'd like further breakdowns!