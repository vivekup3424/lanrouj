You are given an array `nums` of **non-negative** integers and an integer `k`.

An array is called **special** if the bitwise `OR` of all of its elements is **at least** `k`.

Return _the length of the **shortest** **special** **non-empty**_ _subarray_

_of_ `nums`, _or return_ `-1` _if no special subarray exists_.

**Example 1:**

**Input:** nums = [1,2,3], k = 2

**Output:** 1

**Explanation:**

The subarray `[3]` has `OR` value of `3`. Hence, we return `1`.

**Example 2:**

**Input:** nums = [2,1,8], k = 10

**Output:** 3

**Explanation:**

The subarray `[2,1,8]` has `OR` value of `11`. Hence, we return `3`.

**Example 3:**

**Input:** nums = [1,2], k = 0

**Output:** 1

**Explanation:**

The subarray `[1]` has `OR` value of `1`. Hence, we return `1`.

**Constraints:**

- `1 <= nums.length <= 2 * 105`
- `0 <= nums[i] <= 109`
- `0 <= k <= 109`

## Some thinking done by me

![[Pasted image 20241110224620.png]]


## Some other approach which I think my work

![[Pasted image 20241110225627.png]]

>[!WARNIING]
>Largest value of usigned integer = $2^(32)$ -1
>Largest value of integer  = $2^\(31\)$-1

## First sliding window approach
```c++

class Solution {
public:
    int minimumSubarrayLength(vector<int>& nums, int k) {
        int countBits = 0;
        vector<int> activeBitsK(31, 0); // We assume 32-bit integers
        // Calculate the active bits of k
        for (int i = 0; i < 31; i++) {
            if (k & (1 << i)) {
                activeBitsK[i] = 1;
                countBits++;
            }
        }
        int currentCountBits = 0;
        int start = 0, end = 0;
        int n = nums.size();
        vector<int> windowBits(31, 0);
        int minLength = INT_MAX;
        // Start sliding window
        while (end < n) {
            // Update windowBits for nums[end]
            for (int i = 0; i < 31; i++) {
                if (nums[end] & (1 << i)) {
                    windowBits[i]++;
                    if (windowBits[i] == activeBitsK[i]) {
                        currentCountBits++;
                    }
                }
            }
            // Try to contract the window from the start if it meets the condition
            while (currentCountBits == countBits && start <= end) {
                minLength = min(minLength, end - start + 1);
                // Remove nums[start] from windowBits
                for (int i = 0; i < 31; i++) {
                    if (nums[start] & (1 << i)) {
                        windowBits[i]--;
                        if (windowBits[i] < activeBitsK[i]) {
                            currentCountBits--;
                        }
                    }
                }
                start++;
            }
            // Move the end of the window forward
            end++;
        }
        return (minLength == INT_MAX) ? -1 : minLength;
    }
};
```
this approach is not working because it may happen that
even though I have a larger number in my window, but it wouldn't necessarily 
matches with the k, so answer is not alway possible 

### _For Example_
- Input
nums = [41]
k = 3
- Stdout
    Active bits of k:
    1100000000000000000000000000000
    Total countBits required: 2
    Processing nums\[0\] = 41
    Window bits after adding nums\[0\]: 1001010000000000000000000000000
    Current count of matching bits: 1
    No valid subarray found.
- Output
    -1
- Expected
    1

## My review and reflections
1. Atleast I thought of a good approach and tried to relate with a previous
question of minimum window substring
2. This shows the I am learning about things and keeping them in my mind


Maybe like I am checking for
` while (currentCountBits == countBits && start <= end) { `
number of bits to be equal we dont need to do that
rather from the windowBits I can construct the binaryNumber
and get the smallest windowLength neeeded to get the binaryNumber >=
requiredNumber

```c++
class Solution {
public:
    int minimumSubarrayLength(vector<int>& nums, int k) {
        int minLength = INT_MAX;
        int windowStart = 0;
        int windowEnd = 0;
        vector<int> bitCounts(32,
                              0);  // Tracks count of set bits at each position

        // Expand window until end of array
        while (windowEnd < nums.size()) {
            // Add current number to window
            updateBitCounts(bitCounts, nums[windowEnd], 1);

            // Contract window while OR value is valid
            while (windowStart <= windowEnd &&
                   convertBitCountsToNumber(bitCounts) >= k) {
                // Update minimum length found so far
                minLength = min(minLength, windowEnd - windowStart + 1);

                // Remove leftmost number and shrink window
                updateBitCounts(bitCounts, nums[windowStart], -1);
                windowStart++;
            }

            windowEnd++;
        }

        return minLength == INT_MAX ? -1 : minLength;
    }

private:
    // Updates bit count array when adding/removing a number from window
    void updateBitCounts(vector<int>& bitCounts, int number, int delta) {
        for (int bitPosition = 0; bitPosition < 32; bitPosition++) {
            // Check if bit is set at current position
            if ((number >> bitPosition) & 1) {
                bitCounts[bitPosition] += delta;
            }
        }
    }

    // Converts bit count array back to number using OR operation
    int convertBitCountsToNumber(const vector<int>& bitCounts) {
        int result = 0;
        for (int bitPosition = 0; bitPosition < 32; bitPosition++) {
            if (bitCounts[bitPosition] != 0) {
                result |= 1 << bitPosition;
            }
        }
        return result;
    }
 };
```




