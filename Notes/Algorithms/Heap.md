### Heap

**What is a Heap?**  
A heap is a special tree-based data structure that satisfies the *heap property*. There are two main types of heaps:
- **Max-Heap**: The key of a node is always greater than or equal to the keys of its children.
- **Min-Heap**: The key of a node is always less than or equal to the keys of its children.

Heaps are commonly implemented as binary trees, where each level is filled from left to right.

**Why do we use Heaps?**  
Heaps are primarily used for operations that involve quick access to the largest or smallest element. The common applications of heaps include:
- **Priority Queues**: Heaps can be used to implement priority queues where elements with higher priority are served first.
- **Efficient Sorting**: Heapsort algorithm is a comparison-based sorting technique based on a binary heap data structure.
- **Graph Algorithms**: Algorithms like Dijkstra's shortest path and Prim's minimum spanning tree use heaps for efficient minimum/maximum retrieval.

**How is it implemented?**  
A heap can be efficiently represented using an array. For a given index `i`:
- The left child is at index `2 * i + 1`
- The right child is at index `2 * i + 2`
- The parent is at index `(i - 1) / 2`

Here’s a basic implementation of a Max-Heap in C++:

```cpp
#include <iostream>
#include <vector>
using namespace std;

class MaxHeap {
    vector<int> heap;

    // Helper function to maintain the max-heap property
    void heapifyUp(int index) {
        while (index > 0 && heap[(index - 1) / 2] < heap[index]) {
            swap(heap[(index - 1) / 2], heap[index]);
            index = (index - 1) / 2;
        }
    }

    // Helper function to maintain the max-heap property after removal
    void heapifyDown(int index) {
        int size = heap.size();
        int largest = index;
        int left = 2 * index + 1;
        int right = 2 * index + 2;

        if (left < size && heap[left] > heap[largest]) largest = left;
        if (right < size && heap[right] > heap[largest]) largest = right;

        if (largest != index) {
            swap(heap[index], heap[largest]);
            heapifyDown(largest);
        }
    }

public:
    // Insert a new element into the heap
    void insert(int value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    // Remove and return the maximum element
    int extractMax() {
        if (heap.size() == 0) return -1;
        int maxElement = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);
        return maxElement;
    }

    // Return the maximum element
    int getMax() {
        return heap.size() > 0 ? heap[0] : -1;
    }
};
```

**Common Interview Questions Using Heaps**

1. **Kth Largest Element in an Array**
   - **Description**: Given an array of integers, find the \( k^{th} \) largest element.
   - **Solution**: Use a Min-Heap of size `k`. Traverse the array, and if the size exceeds `k`, remove the smallest element. At the end, the root of the heap will contain the \( k^{th} \) largest element.
   
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

2. **Merge K Sorted Lists**
   - **Description**: Merge \( k \) sorted linked lists into one sorted list.
   - **Solution**: Use a Min-Heap to keep track of the smallest elements from each list. Insert the first element from each list into the heap. Extract the smallest element from the heap and insert the next element from that list into the heap until all elements are merged.
   
   ```cpp
   ListNode* mergeKLists(vector<ListNode*>& lists) {
       auto cmp = [](ListNode* a, ListNode* b) { return a->val > b->val; };
       priority_queue<ListNode*, vector<ListNode*>, decltype(cmp)> minHeap(cmp);
       
       for (auto l : lists) {
           if (l) minHeap.push(l);
       }

       ListNode dummy(0), *tail = &dummy;
       while (!minHeap.empty()) {
           tail->next = minHeap.top(); minHeap.pop();
           tail = tail->next;
           if (tail->next) minHeap.push(tail->next);
       }
       return dummy.next;
   }
   ```

3. **Top K Frequent Elements**
   - **Description**: Given an integer array, return the \( k \) most frequent elements.
   - **Solution**: Use a Min-Heap to store elements with frequency counts. Traverse the array and push elements with their frequencies. Maintain the heap size to be at most `k`. At the end, extract the elements from the heap to get the top `k` frequent elements.

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

4. **Find Median from Data Stream**
   - **Description**: Design a data structure that supports adding numbers and finding the median.
   - **Solution**: Use two heaps: a Max-Heap for the lower half and a Min-Heap for the upper half. This allows for efficient retrieval of the median.
   
   ```cpp
   class MedianFinder {
       priority_queue<int> maxHeap; // lower half
       priority_queue<int, vector<int>, greater<int>> minHeap; // upper half

   public:
       void addNum(int num) {
           maxHeap.push(num);
           minHeap.push(maxHeap.top());
           maxHeap.pop();
           if (maxHeap.size() < minHeap.size()) {
               maxHeap.push(minHeap.top());
               minHeap.pop();
           }
       }

       double findMedian() {
           if (maxHeap.size() > minHeap.size()) return maxHeap.top();
           return (maxHeap.top() + minHeap.top()) / 2.0;
       }
   };
   ```

These questions are commonly asked in coding interviews and test a candidate's ability to use heaps effectively.