#### Problem Statement

Given an integer array `arr`, find the contiguous subarray (containing at least one number) which  
has the largest sum. Return the sum of the subarray and print the subarray.

---

#### Approach

Kadane’s Algorithm uses dynamic programming to solve the problem efficiently in O(n) time.

1. **Initialization**:
    
    - Maintain two variables:
        - `max_sum` to store the maximum sum encountered so far (initialize it to the first element of the array).
        - `current_sum` to store the sum of the current subarray being evaluated (also initialized to the first element).
    - Additionally, to keep track of the subarray itself, maintain indices:
        - `start`, `end` for the final subarray.
        - `temp_start` for the potential start of the current subarray.
2. **Iteration**:
    
    - Iterate through the array starting from the second element. For each element:
        - Add it to the `current_sum`. If the element itself is greater than `current_sum + element`, start a new subarray at the current index (update `temp_start`).
        - Update `max_sum` if `current_sum` exceeds `max_sum`. If updated, also set `start = temp_start` and `end = current index`.
3. **Output**:
    
    - Return `max_sum`.
    - Extract the subarray using `start` and `end` indices and print it.

---

#### Algorithm

```python
def kadane_with_subarray(arr):
    # Initialize variables
    max_sum = arr[0]
    current_sum = arr[0]
    start = 0
    end = 0
    temp_start = 0
    
    # Traverse the array
    for i in range(1, len(arr)):
        # Check if we should start a new subarray
        if arr[i] > current_sum + arr[i]:
            current_sum = arr[i]
            temp_start = i
        else:
            current_sum += arr[i]
        
        # Update max_sum and subarray indices
        if current_sum > max_sum:
            max_sum = current_sum
            start = temp_start
            end = i
    
    # Extract the subarray
    subarray = arr[start:end + 1]
    
    # Return the result
    return max_sum, subarray

# Example Usage
arr = [-2, -3, 4, -1, -2, 1, 5, -3]
result = kadane_with_subarray(arr)
print(f"Maximum Sum: {result[0]}")
print(f"Subarray: {result[1]}")
```

---

#### Example

Input:  
`arr = [-2, -3, 4, -1, -2, 1, 5, -3]`

Output:  
`Maximum Sum: 7`  
`Subarray: [4, -1, -2, 1, 5]`

---

#### Complexity

- **Time Complexity**: O(n) — Each element is processed once.
- **Space Complexity**: O(1) — Only a few variables are used for computation.

---

This approach ensures that we efficiently compute the maximum sum while keeping track of the corresponding subarray.

### Problems making use of Kadane's algorithms
1.[[Maximum Sum Subarray]]