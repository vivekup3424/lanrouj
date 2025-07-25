---
tags:
  - algorithms
  - blind-75
---

Given an integer array nums, return true if there exists a triple of indices (i, j, k) 
such that 
i < j < k and 
nums[i] < nums[j] < nums[k]. 
If no such indices exists, return false.

*Example 3:*
Input: nums = [2,1,5,0,4,6]
Output: true
Explanation: The triplet (3, 4, 5) is valid because nums[3] == 0 < nums[4] == 4 < nums[5] == 6.

**Constraints:**
    1 <= nums.length <= 5 * 105
    -2^31 <= nums[i] <= 2^31 - 1

My approaches were:-

1. Deciding upon three variables (smallest, middle, and highest)
![[Pasted image 20250707231307.png|600]]