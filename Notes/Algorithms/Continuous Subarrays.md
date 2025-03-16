You are given a **0-indexed** integer array `nums`. A subarray of `nums` is called **continuous** if:

- Let `i`, `i + 1`, ..., `j` be the indices in the subarray. Then, for each pair of indices `i <= i1, i2 <= j`, `0 <= |nums[i1] - nums[i2]| <= 2`.

Return _the total number of **continuous** subarrays._

A subarray is a contiguous **non-empty** sequence of elements within an array.

**Example 1:**

**Input:** nums = [5,4,2,4]
**Output:** 8
**Explanation:** 
Continuous subarray of size 1: [5], [4], [2], [4].
Continuous subarray of size 2: [5,4], [4,2], [2,4].
Continuous subarray of size 3: [4,2,4].
Thereare no subarrys of size 4.
Total continuous subarrays = 4 + 3 + 1 = 8.
It can be shown that there are no more continuous subarrays.


## My first approach
```python
class Solution:
    def continuousSubarrays(self, nums: List[int]) -> int:
        total_count = 0
        start = 0
        current_min = nums[0]
        current_max = nums[0]
        for end in range(len(nums)):
            current_min = min(current_min, nums[end])
            current_max = max(current_max, nums[end])
            while current_max - current_min > 2:
                start += 1
                current_min = min(nums[start : end + 1])
                current_max = max(nums[start : end + 1])
            total_count += end - start + 1
        return total_count

```
### Problem I encountered
1. I didn't know how to find min and max in a continuous array in python
2. The time complexity was O($n^2$), since we need to traverse over all the elements so the `for end in range(len(nums))` can't be removed, hence the only scope of improvement was in finding the max_element and min_element of dynamic subarray of nums

## Optimized Approach using Priority Queue
```python
class Solution:
    def continuousSubarrays(self, nums: List[int]) -> int:
        # Two heaps to track min/max indices, sorted by nums[index]
        min_heap = []  # (nums[i], i) tuples for min tracking
        max_heap = []  # (-nums[i], i) tuples for max tracking
        left = right = 0
        count = 0

        while right < len(nums):
            # Add current index to both heaps
            # For max heap, negate value to convert min heap to max heap
            heapq.heappush(min_heap, (nums[right], right))
            heapq.heappush(max_heap, (-nums[right], right))

            # While window violates |nums[i] - nums[j]| ≤ 2
            # Shrink window from left and remove outdated indices
            while left < right and -max_heap[0][0] - min_heap[0][0] > 2:
                left += 1

                # Remove indices outside window from both heaps
                while min_heap and min_heap[0][1] < left:
                    heapq.heappop(min_heap)
                while max_heap and max_heap[0][1] < left:
                    heapq.heappop(max_heap)

            count += right - left + 1
            right += 1

        return count

```

