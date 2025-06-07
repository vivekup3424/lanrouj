- **Problem**: Find the \( $k^{th}$ \) largest element.
- **Solution**: Use a Min-Heap of size `k`. Traverse the array, pushing elements into the heap. If size exceeds `k`, remove the smallest element. The top element of the heap is the \( $k^{th}$ \) largest.

```cpp
int findKthLargest(vector<int>& nums, int k) {
    priority_queue<int, vector<int>, greater<int>> minHeap;
    for (int num : nums) {
        minHeap.push(num);
        if (minHeap.size() > k) minHeap.pop();
    }
    return minHeap.top();
}
```