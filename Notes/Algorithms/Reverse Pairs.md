Given an integer array `nums`, return _the number of **reverse pairs** in the array_.

A **reverse pair** is a pair `(i, j)` where:

- `0 <= i < j < nums.length` and
- `nums[i] > 2 * nums[j]`.


### Naive Solution
```c++
    int naiveMethod(vector<int> & nums){
        int count = 0;
        for (int i = 0; i < nums.size(); i++)
        {
            for(int j = 0; j < i; j++){
                if(nums[j]>2LL * nums[i]){
                    count+=1;
                }
            }
        }
        return count;
    }
```

**Complexity Analysis**

- Time complexity: O(n2)
    - We iterate over all the possible pairs wherein (i<j) in the array which is O(n2)
- Space complexity: O(1) only constant extra space is required for n, count etc


