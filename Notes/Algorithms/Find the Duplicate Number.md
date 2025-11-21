Question
Given an array of integers `nums` containing `n + 1` integers where each integer is in the range `[1, n]` inclusive.

There is only **one repeated number** in `nums`, return _this repeated number_.

You must solve the problem **without** modifying the array `nums` and using only constant extra space.

-----

the first solution, that I've thought of was this number = 
```python
from typing import List
class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        # first approach: calculate the sum of numbers from 1 to n-1
        n = len(nums) - 1
        expected_sum = n * (n + 1) // 2
        actual_sum = sum(nums)
        return actual_sum - expected_sum
```

this above approach is not going to work, because in the question it is not mentioned that all the members are appearing atleast once,
what that means is they can probably appear or not appear

now I need it some other efficient way of knowing whether I have 