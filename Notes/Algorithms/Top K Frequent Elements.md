- **Problem**: Return the `k` most frequent elements.
- **Solution**: 
	- Use a Min-Heap to store elements by frequency. Insert elements, and 
	- if size > `k`, remove the least frequent. Extract elements to get the top `k` frequent items.

```cpp
vector<int> topKFrequent(vector<int>& nums, int k) {
    unordered_map<int, int> freq;
    for (int num : nums) freq[num]++;
    
    auto cmp = [](pair<int, int>& a, pair<int, int>& b) { return a.second > b.second; };
    priority_queue<pair<int, int>, vector<pair<int, int>>, decltype(cmp)> minHeap(cmp);
    
    for (auto& [num, count] : freq) {
        minHeap.push({num, count});
        if (minHeap.size() > k) minHeap.pop();
    }

    vector<int> result;
    while (!minHeap.empty()) {
        result.push_back(minHeap.top().first);
        minHeap.pop();
    }
    return result;
}
```
