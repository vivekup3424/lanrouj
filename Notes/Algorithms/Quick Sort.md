# QuickSort with Hoare's Partition Scheme

---

## 🧠 Core Idea

QuickSort is a **divide-and-conquer** sorting algorithm. It works by:

1. Choosing a pivot.
    
2. Partitioning the array around the pivot so that:
    
    - Left part contains elements <= pivot.
        
    - Right part contains elements >= pivot.
        
3. Recursively applying the same procedure on left and right partitions.
    

> In **Hoare's partition scheme**, the pivot is _not_ placed at its final sorted position immediately. Instead, the partitioning guarantees elements are correctly split into two halves.

---

## 📊 Time and Space Complexity

|Case|Time Complexity|
|---|---|
|Best Case|O(n log n)|
|Average|O(n log n)|
|Worst Case|O(n^2)|

- Worst case happens when partitioning is extremely unbalanced (e.g., sorted array with bad pivot selection).
    

### Space Complexity

- **O(log n)** (due to recursion stack in balanced case).
    
- **O(n)** worst case (if recursion is deeply unbalanced).
    

---

## 🧾 Pseudocode (Hoare Partition)

```
function quicksort(arr, low, high):
    if low < high:
        p = hoare_partition(arr, low, high)
        quicksort(arr, low, p)
        quicksort(arr, p + 1, high)

function hoare_partition(arr, low, high):
    pivot = arr[(low + high) // 2]
    i = low - 1
    j = high + 1
    while true:
        repeat:
            i = i + 1
        until arr[i] >= pivot

        repeat:
            j = j - 1
        until arr[j] <= pivot

        if i >= j:
            return j
        swap(arr[i], arr[j])
```

---

## 💻 Actual Code (Python)

```python
def hoare_partition(arr, low, high):
    pivot = arr[(low + high) // 2]
    i = low - 1
    j = high + 1

    while True:
        i += 1
        while arr[i] < pivot:
            i += 1
        j -= 1
        while arr[j] > pivot:
            j -= 1

        if i >= j:
            return j

        arr[i], arr[j] = arr[j], arr[i]


def quicksort(arr, low, high):
    if low < high:
        p = hoare_partition(arr, low, high)
        quicksort(arr, low, p)
        quicksort(arr, p + 1, high)
```

---

## 🖼 Visual Example

### Input: `[8, 3, 7, 4, 9, 1, 2, 6, 5]`

- Pivot = 4 (middle element)
    

Partition Step:

```
Initial:     [8, 3, 7, 4, 9, 1, 2, 6, 5]
→ Swap(8, 2): [2, 3, 7, 4, 9, 1, 8, 6, 5]
→ Swap(7, 1): [2, 3, 1, 4, 9, 7, 8, 6, 5]
→ i >= j, return j=2
```

Now `quicksort(arr, 0, 2)` and `quicksort(arr, 3, 8)` are called recursively.

Eventually:

```
Sorted: [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

---
## Quicksort using Lomuto's Partition
```c++
    //returns the index where pivot element is going to be inside the sorted array
    int partition(vector<int> &nums, int left, int right){
        int pivot_index = right;
        int pivot = nums[pivot_index];
        int j = left; //j is for storing the smaller elements
        for(int i = left; i < right; i++){
            if(nums[i]<=pivot){
                swap(nums[i],nums[j]);
                j++;
            }
        }
        swap(nums[j],nums[pivot_index]);
        return j;
    }
    void quicksort(vector<int> &nums, int left, int right){
        if(left<right){
            int pivotIndex = partition(nums,left,right);
            quicksort(nums,left,pivotIndex-1);
            quicksort(nums,pivotIndex+1,right);
        }
    }
```

