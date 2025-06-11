Given an array which is sorted in non-decreasing fashion, I need to remove duplicate from it, such that left portion of the array contains the unique elements in the original order

```c++
void removeDuplicates(vector<int> &v){
	int i = 1, j = 1; //using two pointers method
	while(j < v.size()){
		if(v[j]!=v[j-1]){
			v[i] = v[j];
			i++;
		}
		j++;
	}
}
```
```c++
vector<int> removeDuplicates(vector<int> v){
    //since v is in a sorted form
    int j = 0;
    for(int i = 0; i < v.size(); i++){
        if(v[j]!=v[i]){
            j++;
            v[j] = v[i];
        }
    }
    return v;
}
```

>[!OUTPUT]
>![[Pasted image 20241104191914.png]]
>
![[Pasted image 20241104192018.png]]

> [!NOTE]
>   Time Complexity = O(n) //single pass
