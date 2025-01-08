You are given an integer array arr[l of size n and an integer k. You have to select exactly k
different subarrays from arr[]. For each selected subarray, calculate the sum of its
elements. Then, compute the bitwise AND of all these sums. You need to return the
maximum possible value of this bitwise AND.

> [!NOTE]
> A subarray is a contiguous segment of the array.

**Examples:**

--------

Input: k = 2, arr = [3, 2, 5]
Output: 5
Explanation: We need to select two subarrays. If we choose the subarrays [2, 5]
and [5]. The sum of these subarray's are 7 and 5. The bitwise AND is 7 & 5 =
5, which is the maximum possible answer.

------

Input: k
= 1, arr = [2, 1, 4]
Output: 7
Explanation: If we select the subarray [2, 1, 4], we would get the maximum
possible bitwise AND of 7.

---------

### Approach: Using Greedy and Bit Manipulation

The idea is to find the maximum possible AND of at least K subarray sums. First, calculate the sums of all subarrays and store them. Since, the maximum subarray sum can be 10^11, so it can have at most 40 bits set. Initialize result = 0 and since we need to maximize the bitwise AND, so start greedily from MSB(bit 40) and for each ith bit, count the subarray sums having the ith bit set along with all the previous bits which are set in result. If there are at least k such subarrays, then set this bit in the result.
### Code
```python
class Solution:
    def maxAND(self, k : int, arr : List[int]) -> int:
        subarray_sums = []
        n = len(arr)
        for i in range(n):
            current_sum = 0
            for j in range(i, n):
                current_sum += arr[j]
                subarray_sums.append(current_sum)

        result = 0

        for bit in range(40, -1, -1):
            candidate = result | (1 << bit)
            count = 0
            for sum_ in subarray_sums:
                if (sum_ & candidate) == candidate:
                    count += 1
                    if count >= k:
                        break
            if count >= k:
                result = candidate

        return result
```
