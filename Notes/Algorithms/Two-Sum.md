### Problem Statement
Given an array of integers `nums` and an integer `target`, return _indices of the two numbers such that they add up to `target`_.

```c++
vector<int> twoSumHashing(vector<int> v, int sum){
    unordered_map<int, int> indices;
    for(int i = 0; i < v.size(); i++){
        if(v[i]<=sum){
            int complement = sum - v[i];
            if(indices.find(complement)!=indices.end()){
                return {i,indices[complement]};
            }else{
                indices[v[i]] = i;
            }
        }
    }
    return {};
}

vector<int> twoSumTwoPointers(vector<int> v, int sum){
    sort(v.begin(),v.end());
    int l = 0, r = v.size()-1;
    while (l <= r) {
        int currentSum = v[l] + v[r];
        if(currentSum<sum){
            l++;
        }else if(currentSum>sum){
            r--;
        }else{
            return {l,r};
        }
    }
    return {};
}

```
