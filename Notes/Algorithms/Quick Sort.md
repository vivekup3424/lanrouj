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

## ✅ Why It Works (Even If Pivot Isn’t Finalized)

- The partition function creates _valid subarrays_ that are correctly ordered relative to the pivot.
    
- Recursively applying this process ensures every element eventually lands at its correct position.
    

> The final sorting emerges from recursive structure, not from individual pivot placements.

---

Let me know if you want this in multiple programming languages or converted to HTML/Markdown with tabbed code blocks.