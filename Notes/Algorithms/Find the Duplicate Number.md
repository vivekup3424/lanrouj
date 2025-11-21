Questio
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

this above approach is not going to work, because in the question 