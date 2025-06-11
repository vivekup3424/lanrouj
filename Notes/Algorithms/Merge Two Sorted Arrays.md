In-place merging of two sorted arrays is a process where you combine two sorted arrays into one sorted array without using extra space for a third array. This requires careful management of elements in the arrays, especially since no additional storage is allowed.

---

### Problem Statement

Given two sorted arrays:

- AA of size mm (contains mm sorted elements and nn extra spaces at the end).
- BB of size nn (contains nn sorted elements).

Merge BB into AA **in-place** such that AA contains all m+nm + n elements sorted.

---

### Algorithm (Optimal Approach)

#### Idea

Since AA has extra space at the end, we can merge from the **end of the arrays** instead of the beginning. This avoids the need to shift elements multiple times.

---

### Steps

1. **Initialize Pointers**:
    
    - ii: Index of the last valid element in AA (initially m−1m - 1).
    - jj: Index of the last element in BB (initially n−1n - 1).
    - kk: Index of the last position in AA (initially m+n−1m + n - 1).
2. **Iterate Backwards**:
    
    - Compare A[i]A[i] and B[j]B[j].
    - Place the larger of the two at A[k]A[k].
    - Decrement ii, jj, or kk accordingly.
3. **Handle Remaining Elements**:
    
    - If BB still has elements left, copy them to AA.
    - If AA has elements left, they are already in place.

---

### Pseudocode

```python
def merge_in_place(A, m, B, n):
    i = m - 1  # Last element in the valid part of A
    j = n - 1  # Last element in B
    k = m + n - 1  # Last position in A

    # Merge in reverse order
    while i >= 0 and j >= 0:
        if A[i] > B[j]:
            A[k] = A[i]
            i -= 1
        else:
            A[k] = B[j]
            j -= 1
        k -= 1

    # Copy remaining elements from B (if any)
    while j >= 0:
        A[k] = B[j]
        j -= 1
        k -= 1
```

---

### Example

#### Input:

- A=[1,3,5,0,0,0]A = [1, 3, 5, 0, 0, 0], m=3m = 3 (valid elements are 1, 3, 5; extra space is at the end).
- B=[2,4,6]B = [2, 4, 6], n=3n = 3.

#### Output:
 
- A=[1,2,3,4,5,6]A = [1, 2, 3, 4, 5, 6].

#### Walkthrough:

1. i=2i = 2, j=2j = 2, k=5k = 5:
    
    - Compare A[i]=5A[i] = 5 and B[j]=6B[j] = 6: Place 6 at A[k]A[k].
    - A=[1,3,5,0,0,6]A = [1, 3, 5, 0, 0, 6], j=1j = 1, k=4k = 4.
2. i=2i = 2, j=1j = 1, k=4k = 4:
    
    - Compare A[i]=5A[i] = 5 and B[j]=4B[j] = 4: Place 5 at A[k]A[k].
    - A=[1,3,5,0,5,6]A = [1, 3, 5, 0, 5, 6], i=1i = 1, k=3k = 3.
3. Continue the process until BB is fully merged into AA.
    

---

### Complexity

1. **Time Complexity**: $O(m+n)$
    - Each element of AA and BB is processed exactly once.
2. **Space Complexity**: $O(1)$
    - No extra storage is used; everything is done in-place.

---
