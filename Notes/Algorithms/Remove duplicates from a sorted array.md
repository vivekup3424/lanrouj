
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
> [!NOTE]
>   Time Complexity = O(n) //single pass
