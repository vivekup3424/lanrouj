---
id: Sort 0s 1s 2s
aliases: 
tags:
  - pointers
  - two-pointer
  - 2-pointer
---

# Sort Colors
- Dutch National Problem
- The problem is then to produce an array such that all "bottom" elements 
    come before (have an index less than the index of) all 
    "middle" elements, which come before all "top" elements. 

```c++
void sortColors(vector<int> &v){
    int i = 0, j = 0, k = v.size()-1;
    while (j<=k) {
        if (v[j]==0) {
            swap(v[i],v[j]);
            i++;
            j++;
        }else if(v[j]==1){
            j++;
        }else{
            swap(v[j],v[k]);
            k--;
        }
    }
}
```

