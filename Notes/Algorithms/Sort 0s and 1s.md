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

