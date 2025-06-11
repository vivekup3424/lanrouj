---
id: Sort 0s and 1s
aliases: []
tags:
  - pointers
---

## Problem Statement
So the easier variant of this problem goes like this

We have a binary string of 0s and 1s, we need to rearrange such
that all 0s comes on left side and 1s comes on right side

### My solution
```cpp
void rearrange(vector<int> &v){
    int j = 0;
    for(int i = 0; i < v.size(); i++){
        if(v[i]==0){
            swap(v[i],v[j]);
            j++;
        }
    }
}
```
## Sort negatives and positives

This is another variant in which negatives are sorted in left manner
with their respective order preserved, similarly positives are shifted to 
right with their respective order preserved.

> [!NOTE]
> This can be done in a bruteforce way
> but the approach presented above is the optimal one

```c++
void rearrange(vector<int> &v){
  int j = 0;
  for(int i = 0; i < v.size(); i++){
    if(v[j]<0){
      swap(v[i],v[j]);
      j++;
    }
  }
}
```
----------

## Sort evens and odds, preserving the order of evens and odds
It can be done using the above approach
but what I wanted to do here specifically if introduce a new approach
this new approach would be similar to the approach of sort 0s 1s and 2s.
i.e. similar to Dutch Flag Problem

```python
def even_odd(arr):
    even = 0
    odd = len(arr) - 1
    while even < odd:
        if arr[even] % 2 == 0:
            even += 1
        else:
            arr[even], arr[odd] = arr[odd], arr[even]
            odd -= 1

```


## Similar Probelm
