# Sort Colors
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

