### Notes for Creating the Union of Two Sorted Arrays

The goal is to find the **union** of two sorted arrays, meaning we need to identify all distinct elements from both arrays in ascending order.

---

### **Key Approaches**

#### 1. **Using a Map**

- **Idea**: Use a `map` to store the frequencies of elements from both arrays. This works because:
    - A `map` automatically sorts its keys in ascending order.
    - It ensures no duplicate elements are included in the result.

**Steps**:

1. Traverse through the first array and insert elements into the map.
2. Traverse through the second array and insert elements into the map.
3. Extract keys from the map to form the union array.

**Time Complexity**: O((m+n)log⁡(m+n))O((m+n)\log(m+n)) for insertion into the map.  
**Space Complexity**: O(m+n)O(m+n).

---

#### 2. **Using a Set**

- **Idea**: Combine both arrays into a single array, then use a `set` to extract distinct elements.
    - A `set` stores only unique elements.
    - It automatically keeps elements sorted (ascending order).

**Steps**:

1. Combine both arrays into a single array.
2. Insert all elements into a `set`.
3. Convert the `set` to a vector or array to get the result.

**Time Complexity**: O((m+n)log⁡(m+n))O((m+n)\log(m+n)) for insertion into the set.  
**Space Complexity**: O(m+n)O(m+n).

---

#### 3. **Two Pointer Method**

- **Idea**: Since the arrays are sorted, we can use two pointers to traverse both arrays simultaneously and compare elements.
    - This ensures we avoid duplicates while maintaining sorted order.

**Steps**:

1. Initialize two pointers (`i`, `j`) to the start of both arrays and an empty result vector.
2. Compare elements at `arr1[i]` and `arr2[j]`:
    - If `arr1[i] < arr2[j]`: Add `arr1[i]` to the result and move pointer `i`.
    - If `arr1[i] > arr2[j]`: Add `arr2[j]` to the result and move pointer `j`.
    - If `arr1[i] == arr2[j]`: Add the element once and move both pointers.
3. After one array is fully traversed, add the remaining elements from the other array.
4. Ensure no duplicates are added by checking the last element in the result vector.

**Time Complexity**: O(m+n)O(m+n), as both pointers traverse their respective arrays once.  
**Space Complexity**: O(m+n)O(m+n), considering the result vector.

---

### **Comparison of Approaches**

|**Method**|**Time Complexity**|**Space Complexity**|**Best For**|
|---|---|---|---|
|Map|O((m+n)log⁡(m+n))O((m+n)\log(m+n))|O(m+n)O(m+n)|When input arrays are unsorted.|
|Set|O((m+n)log⁡(m+n))O((m+n)\log(m+n))|O(m+n)O(m+n)|When arrays are unsorted or for simplicity.|
|Two Pointers|O(m+n)O(m+n)|O(m+n)O(m+n)|When arrays are sorted and memory efficiency is needed.|

---

### **Best Approach**

- Use the **Two Pointer Method** when arrays are already sorted.
    - It’s the most time-efficient for sorted arrays (O(m+n)O(m+n)).
- Use `map` or `set` if the input arrays are **not sorted**.

---

### **Implementation Using Two Pointers**

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> FindUnion(int arr1[], int arr2[], int n, int m) {
    int i = 0, j = 0; // Initialize pointers
    vector<int> Union; // To store the result
    
    while (i < n && j < m) {
        if (arr1[i] <= arr2[j]) { // Case 1: arr1[i] <= arr2[j]
            if (Union.empty() || Union.back() != arr1[i]) 
                Union.push_back(arr1[i]);
            i++;
        } else { // Case 3: arr1[i] > arr2[j]
            if (Union.empty() || Union.back() != arr2[j]) 
                Union.push_back(arr2[j]);
            j++;
        }
    }
    
    // Add remaining elements from arr1
    while (i < n) {
        if (Union.empty() || Union.back() != arr1[i]) 
            Union.push_back(arr1[i]);
        i++;
    }
    
    // Add remaining elements from arr2
    while (j < m) {
        if (Union.empty() || Union.back() != arr2[j]) 
            Union.push_back(arr2[j]);
        j++;
    }
    
    return Union;
}

int main() {
    int n = 10, m = 7;
    int arr1[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int arr2[] = {2, 3, 4, 4, 5, 11, 12};
    
    vector<int> Union = FindUnion(arr1, arr2, n, m);
    cout << "Union of arr1 and arr2 is: ";
    for (auto val : Union)
        cout << val << " ";
    return 0;
}
```

---

### **Output Example**

**Input**:  
`arr1 = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}`  
`arr2 = {2, 3, 4, 4, 5, 11, 12}`

**Output**:  
`Union of arr1 and arr2 is: 1 2 3 4 5 6 7 8 9 10 11 12`