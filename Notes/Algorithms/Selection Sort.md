Selection sort is a comparison based sorting algorithm. 
It works by first selecting a smallest element from an unsorted portion and replacing it with the first unsorted element.

```c++
void selectionSort(vector<int> &v){
    for(int i = 0; i < v.size(); i++){
        int minIdx = i;
        int minValue = v[i];
        for(int j = i; j < v.size(); j++){
            if(v[j] < minValue){
                minIdx = j;
                minValue = v[j];
            }
        }
        swap(v[i],v[minIdx]);
    }
}
```
> [!NOTE]
> Time Complexity = Θ(n<sup>2</sup>)
> Space Complexity = constant extra space
