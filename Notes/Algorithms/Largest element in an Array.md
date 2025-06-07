Given an array ****arr.**** The task is to find the largest element in the given array.

> ****Input:**** arr[] = [10, 20, 4]  
> ****Output:**** 20  
> ****Explanation:**** Among 10, 20 and 4, 20 is the largest. 
> 
> ****Input:**** arr[] = [20, 10, 20, 4, 100]  
> ****Output:**** 100

### Iterative Approach - O(n) Time and O(1) Space
The approach to solve this problem is to traverse the whole array and find the maximum among them.
```python
def largest(arr, n):
    mx = arr[0]
    
    for i in range(1, n):
        if arr[i] > mx:
            mx = arr[i]

    return mx
```

### Recursive Approach - O(n) Time and O(n) Space
```python
def findMax(arr, n):
    if n == 0:
        return arr[n]
        
    recMax = findMax(arr, n - 1)

    return max(recMax, arr[n])

def largest(arr):
    return findMax(arr, len(arr)-1)
```
