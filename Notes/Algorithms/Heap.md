To make these notes more readable in Obsidian, use markdown formatting to create clear headings, bullet points, code blocks, and lists for structured readability. Here’s a reformatted version:

---

# Heap

### What is a Heap?
A heap is a special tree-based data structure that satisfies the **heap property**. There are two types:

- **Max-Heap**: Parent node ≥ its children.
- **Min-Heap**: Parent node ≤ its children.

Each level of the binary tree fills from left to right.

### Why Use Heaps?
Heaps are useful for fast access to the largest or smallest elements and are commonly applied in:

- **Priority Queues**: Elements with higher priority are served first.
- **Efficient Sorting**: **Heapsort** is based on the heap structure.
- **Graph Algorithms**: Used in **Dijkstra’s shortest path** and **Prim's MST**.

### Implementation
Heaps are often implemented as arrays:
- **Left Child**: `2 * i + 1`
- **Right Child**: `2 * i + 2`
- **Parent**: `(i - 1) / 2`

#### C++ Implementation of Max-Heap
```cpp
#include <iostream>
#include <vector>
using namespace std;

class MaxHeap {
    vector<int> heap;

    void heapifyUp(int index) {
        while (index > 0 && heap[(index - 1) / 2] < heap[index]) {
            swap(heap[(index - 1) / 2], heap[index]);
            index = (index - 1) / 2;
        }
    }

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
    void insert(int value) {
        heap.push_back(value);
        heapifyUp(heap.size() - 1);
    }

    int extractMax() {
        if (heap.empty()) return -1;
        int maxElement = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);
        return maxElement;
    }

    int getMax() {
        return heap.empty() ? -1 : heap[0];
    }
};
```

---

### Common Interview Questions Using Heaps

1. [[Kth Largest Element in an Array]]
2. [[Merge K Sorted Lists]]
3. [[Top K Frequent Elements]]
4. [[Find Median from Data Stream]]
5. [[Continuous Subarrays]] - Leetcode daily 2024-12-14 (did on discord study session with Vik and Aman)
6. 