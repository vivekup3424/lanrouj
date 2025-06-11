---
id: BinarySearch
aliases: []
tags:
  - "[binarySearch](Notes/Algorithms/BinarySearch.md)"
---

### Binary Search Overview

#### What is Binary Search?
Binary search is an efficient algorithm used to find the position of a target value within a sorted array or list. The key idea is to repeatedly divide the search interval in half. If the target value is equal to the middle element, the search ends. If the target value is less than the middle element, the search continues in the left half, otherwise in the right half.

#### Why Use Binary Search?
Binary search has a time complexity of $( O(\log n) )$, making it highly efficient for searching in sorted data structures compared to linear search, which has \( O(n) \) complexity. It’s widely applicable in contexts where rapid lookups are needed, such as in databases, search engines, and data analysis.

#### How to Implement Binary Search
1. Define a search range with two pointers, `left` and `right`, initialized to the start and end of the array, respectively.
2. Calculate the middle index: `mid = left + (right - left) / 2`.
3. Compare the middle element with the target:
   - If `arr[mid] == target`, return `mid`.
   - If `arr[mid] < target`, search in the right half (`left = mid + 1`).
   - If `arr[mid] > target`, search in the left half (`right = mid - 1`).
4. Repeat steps 2–3 until `left` exceeds `right` (target not found).

### Key Binary Search Variants and Problems

1. **Standard Binary Search**
   - **Problem**: Find an element’s index in a sorted array.
   - **Approach**: Implement the basic binary search algorithm.
   - **Code Example**:
     ```cpp
     int binarySearch(vector<int>& arr, int target) {
         int left = 0, right = arr.size() - 1;
         while (left <= right) {
             int mid = left + (right - left) / 2;
             if (arr[mid] == target) return mid;
             else if (arr[mid] < target) left = mid + 1;
             else right = mid - 1;
         }
         return -1;
     }
     ```

2. **First and Last Position of Element in Sorted Array**
   - **Problem**: Given a sorted array, find the first and last occurrences of a target element.
   - **Approach**: Use modified binary search twice, once for the first occurrence and once for the last.
   - **Code Example**:
     ```cpp
     vector<int> searchRange(vector<int>& arr, int target) {
         return {findPosition(arr, target, true), findPosition(arr, target, false)};
     }

     int findPosition(vector<int>& arr, int target, bool findFirst) {
         int left = 0, right = arr.size() - 1, position = -1;
         while (left <= right) {
             int mid = left + (right - left) / 2;
             if (arr[mid] == target) {
                 position = mid;
                 if (findFirst) right = mid - 1;
                 else left = mid + 1;
             } else if (arr[mid] < target) left = mid + 1;
             else right = mid - 1;
         }
         return position;
     }
     ```
3. **Search in Rotated Sorted Array**
   - **Problem**: Given a sorted array rotated at an unknown pivot, find a target element.
   - **Approach**: Use binary search by determining which half of the array is sorted and adjusting the search accordingly.
   - **Code Example**:
     ```cpp
     int search(vector<int>& arr, int target) {
         int left = 0, right = arr.size() - 1;
         while (left <= right) {
             int mid = left + (right - left) / 2;
             if (arr[mid] == target) return mid;
             if (arr[left] <= arr[mid]) { // Left half is sorted
                 if (target >= arr[left] && target < arr[mid]) right = mid - 1;
                 else left = mid + 1;
             } else { // Right half is sorted
                 if (target > arr[mid] && target <= arr[right]) left = mid + 1;
                 else right = mid - 1;
             }
         }
         return -1;
     }
     ```
4. **Find Minimum in Rotated Sorted Array**
   - **Problem**: Find the minimum element in a rotated sorted array.
   - **Approach**: Use binary search with a focus on finding the inflection point.
   - **Code Example**:
     ```cpp
     int findMin(vector<int>& arr) {
         int left = 0, right = arr.size() - 1;
         while (left < right) {
             int mid = left + (right - left) / 2;
             if (arr[mid] > arr[right]) left = mid + 1;
             else right = mid;
         }
         return arr[left];
     }
     ```
5. **Square Root of an Integer**
   - **Problem**: Find the integer part of the square root of a number.
   - **Approach**: Use binary search within the range `[0, n/2]` to approximate the square root.
   - **Code Example**:
     ```cpp
     int mySqrt(int x) {
         int left = 0, right = x, result = -1;
         while (left <= right) {
             int mid = left + (right - left) / 2;
             if ((long long) mid * mid <= x) {
                 result = mid;
                 left = mid + 1;
             } else {
                 right = mid - 1;
             }
         }
         return result;
     }
     ```
6. **Median of Two Sorted Arrays**
   - **Problem**: Find the median of two sorted arrays.
   - **Approach**: Apply binary search to partition the arrays to obtain a balanced median.
7. **Most Beautiful Item for Each Query** 
	- **Problem:**- Given a array contain item with their price and their beauty, and given q queries for each query find the most beautiful item whose price <= query
	- **Approach:** Sort the array based on price, at every index save the maxBeauty encountered so far from left to right, for each query find the maxBeauty using binarySearch
	- Code Sample:-
	```c++
	    vector<int> maximumBeauty(vector<vector<int>>& items, vector<int>& queries) {
        sort(items.begin(),items.end());
        int maxBeauty = items[0][1];
        for(int i = 0; i < items.size(); i++){
            if(items[i][1]>maxBeauty){
                maxBeauty = items[i][1];
            }
            items[i][1] = maxBeauty;
        }
        vector<int> ans;
        for(int i = 0; i < queries.size(); i++){
            auto q = queries[i];
            //find the highest beauty with price <= q
            int l = 0, r = items.size()-1;
            int maxPrice = 0;
            while(l<=r){
                int mid = (l+r)/2;
                if(items[mid][0]>q){
                    //mid price > given price
                    //go left
                    r = mid-1;
                }else{
                    //find the upper bound
                    l = mid+1;
                    maxPrice = items[mid][1];
                }
            }
            ans.push_back(maxPrice);
        }
        return ans;
    }
	
	```

