 sfHere's a detailed breakdown of the **Sliding Window Maximum** problem with a focus on using a sf monotonic deque:

---

### **Problem Description**
Given an array of integers `nums` and a sliding window of size `k`, the task is to find the largest number in each sliding window as it moves from left to right across the array. The output is a list of maximum values for each window.

### **Approach: Monotonic Deque**

1. **Intuition**:
   - To solve this efficiently, we need a data structure that allows both inserting elements and removing the smallest element in constant time.
   - A **monotonic deque** fits these requirements. Here, elements are stored in descending order of values within the window, so the front of the deque always has the largest element.
   - We keep only "useful" elements in the deque by removing elements that are smaller than the current one, as they won’t be the maximum in any future windows.

2. **Algorithm Steps**:
   - Initialize an empty deque `dq` and a result list `res`.
   - **Initialize the First Window**:
     - For the first `k` elements in `nums`, maintain the deque’s descending order by removing elements smaller than the current element from the back of `dq`.
   - **Slide the Window Across the Array**:
     - For each element from index `k` to `n - 1`, check if the deque's front element is outside the current window and remove it.
     - Insert the current element while maintaining the deque’s descending order by removing elements from the back that are smaller than the current element.
     - Add the front element of `dq` to `res`, as it represents the largest element in the current window.

3. **Complexity Analysis**:
   - **Time Complexity**: \(O(n)\), since each element is added and removed from the deque at most once.
   - **Space Complexity**: \(O(k)\), as the deque's size is at most `k`.

---

### **C++ Implementation**

```cpp
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k){
        deque<int> dq;
        vector<int> res;
        for (int i = 0; i < k; i++) {
            while (!dq.empty() && nums[i] >= nums[dq.back()]) {
                dq.pop_back();
            }
            dq.push_back(i);
        }
        res.push_back(nums[dq.front()]);

        for (int i = k; i < nums.size(); i++) {
            if(dq.front() == i - k) {
                dq.pop_front(); //remove the left extreme element
                //sliding the window
            }
            while (!dq.empty() && nums[i] >= nums[dq.back()]) {
                dq.pop_back();
            }

            dq.push_back(i);
            res.push_back(nums[dq.front()]);
        }
        
        return res;
    }
};
```
