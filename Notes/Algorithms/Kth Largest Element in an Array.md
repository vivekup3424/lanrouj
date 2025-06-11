---
tags:
  - algorithms
  - sorting
  - priority-queue
---

## Problem Statement

Find the kth largest element in an unsorted array. Note that it is the kth largest element in sorted order, not the kth distinct element.

## Approaches Overview

|Approach|Time Complexity|Space Complexity|Best Use Case|
|---|---|---|---|
|QuickSelect|O(N) avg, O(N²) worst|O(1)|General case|
|Min Heap|O(N log K)|O(K)|Small K values|
|Max Heap|O(N + K log N)|O(N)|Small K values|
|Full Sort|O(N log N)|O(1)|Multiple queries|
|nth_element|O(N) avg|O(1)|STL solution|

---

## Approach 1: QuickSort (Full Sort)

### Algorithm

Sort the entire array in descending order and return the element at index k-1.

### Implementation

```cpp
class Solution {
public:
    int partition(vector<int> &nums, int left, int right) {
        int pivot_index = right;
        int pivot = nums[pivot_index];
        int j = left; // j is for elements greater than or equal to the pivot
        for (int i = left; i < right; i++) {
            if (nums[i] >= pivot) {
                swap(nums[i], nums[j]);
                j++;
            }
        }
        swap(nums[j], nums[pivot_index]);
        return j;
    }
    
    void quicksortInDescendingOrder(vector<int> &nums, int left, int right) {
        if (left < right) {
            int pivotIndex = partition(nums, left, right);
            quicksortInDescendingOrder(nums, left, pivotIndex - 1);
            quicksortInDescendingOrder(nums, pivotIndex + 1, right);
        }
    }
    
    int findKthLargestByQuickSort(vector<int> &nums, int k) {
        quicksortInDescendingOrder(nums, 0, nums.size() - 1);
        return nums[k - 1];
    }
};
```

### Complexity Analysis

- **Time**: O(N log N)
- **Space**: O(log N) for recursion stack
- **Pros**: Simple to understand, works for multiple K queries
- **Cons**: Overkill for single query, not optimal

---

## Approach 2: Min Heap

### Algorithm

Maintain a min heap of size K. The root will always be the Kth largest element.

### Implementation

```cpp
int findKthLargestByMinHeap(vector<int> &nums, int k) {
    priority_queue<int, vector<int>, greater<int>> minHeap;
    for (int num : nums) {
        minHeap.push(num);
        if (minHeap.size() > k) {
            minHeap.pop();
        }
    }
    return minHeap.top();
    // Time complexity = O(N*logK)
}
```

### Complexity Analysis

- **Time**: O(N log K)
- **Space**: O(K)
- **Pros**: Excellent for small K, memory efficient
- **Cons**: Not optimal for large K

### Trace Example

```
nums = [3,2,1,5,6,4], k = 2
Step 1: [3] (heap size = 1)
Step 2: [2,3] (heap size = 2)
Step 3: [2,3] → pop 1, add 1 → [1,3] → pop 1 → [3]
Step 4: [3,5] (heap size = 2)
Step 5: [5,6] → pop 3, add 6 → [5,6]
Step 6: [5,6] → pop 4, stays [5,6]
Result: 5 (2nd largest)
```

---

## Approach 3: QuickSelect (Optimal)

### Algorithm

Use the partition logic of quicksort but only recurse on the side containing the Kth largest element.

### Implementation

```cpp
int partitionForQuickSelect(vector<int> &nums, int left, int right) {
    int pivot_index = right;
    int j = left; // stores the element greater or equal to pivot
    for (int i = left; i < right; i++) {
        if (nums[i] >= nums[pivot_index]) {
            swap(nums[i], nums[j]);
            j++;
        }
    }
    swap(nums[j], nums[pivot_index]);
    return j; // place where the pivot is supposed to go after sorting
}

int quickSelect(vector<int> &nums, int k, int left, int right) {
    if (left == right) {
        return nums[left];
    }
    int pivotIndex = partitionForQuickSelect(nums, left, right);
    if (pivotIndex == k) {
        return nums[k];
    } else if (k < pivotIndex) {
        return quickSelect(nums, k, left, pivotIndex - 1);
    } else {
        return quickSelect(nums, k, pivotIndex + 1, right);
    }
}

int findKthLargestByQuickSelect(vector<int> &nums, int k) {
    return quickSelect(nums, k - 1, 0, nums.size() - 1);
}
```

### Complexity Analysis

- **Time**: O(N) average, O(N²) worst case
- **Space**: O(log N) average for recursion
- **Pros**: Optimal average case, in-place
- **Cons**: Worst case can be O(N²)

### Key Insight

QuickSelect eliminates half the array on average with each partition, leading to:

```
N + N/2 + N/4 + N/8 + ... ≈ 2N = O(N)
```

---

## Alternative Approaches

### Max Heap Approach

```cpp
int findKthLargestByMaxHeap(vector<int>& nums, int k) {
    priority_queue<int> maxHeap(nums.begin(), nums.end());
    for(int i = 0; i < k-1; i++) {
        maxHeap.pop();
    }
    return maxHeap.top();
}
```

### STL nth_element

```cpp
int findKthLargestByNthElement(vector<int>& nums, int k) {
    nth_element(nums.begin(), nums.begin() + k - 1, nums.end(), greater<int>());
    return nums[k-1];
}
```

---

## When to Use Each Approach

### Use **Min Heap** when:

- K is small (K ≤ log N)
- Memory constraint allows O(K) space
- Need to maintain top K elements

### Use **QuickSelect** when:

- K is large
- Need optimal average time complexity
- In-place solution preferred

### Use **Full Sort** when:

- Multiple queries for different K values
- Array needs to be sorted anyway
- Simplicity is preferred over optimization

---

## Common Pitfalls

1. **Off-by-one errors**: Remember k-1 for 0-indexed arrays
2. **Partition direction**: Use `>=` for descending order in partition
3. **Heap type confusion**: Min heap keeps K largest, max heap needs K pops
4. **Worst case**: QuickSelect can degrade to O(N²) with bad pivot selection

---

## Key Takeaways

- **QuickSelect** is theoretically optimal with O(N) average time
- **Min Heap** is practically better for small K values
- **Understanding trade-offs** between time, space, and implementation complexity is crucial
- **Partition logic** is the heart of both QuickSort and QuickSelect