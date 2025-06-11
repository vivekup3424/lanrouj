Given an integer array `nums` where every element appears **three times** except for one, which appears **exactly once**. _Find the single element and return it_.

You must implement a solution with a linear runtime complexity and use only constant extra space.

## Solutions
1. Approach 1
The very naïve approach is to count the frequency of every integer in `nums`. If the frequency of any integer is 1, we can return it. It will take O(N2) time and hence is slow.
```python
singleNumber(nums) {
    for num in nums {
        freq = 0
        for x in nums {
            if x == num {
                freq += 1
            }
        }
        if freq == 1 {
            loner = num
            break
        }
    }

    return loner
}
```

2. Sort the array and then search the loner element
```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        for (int i = 0; i < nums.size() - 1; i += 3) {
            if (nums[i] == nums[i + 1]) {
                continue;
            } else {
                return nums[i];
            }
        }
        return nums[nums.size() - 1];
    }
};
```

3. Using BIT Manipulation
	1. In our case we are interested in XOR based 3, since all the elements except one has a frequency of 3
	2. convert each number into a number system with base 3