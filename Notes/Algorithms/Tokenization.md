# Tokenization
So there are variety of questions where the first step is
1. If we have a sentence, we want to get all the words from the sentence.
```c++
vector<string> getWords(string &sentence){
	string temp = "";
	vector<string> ans;
	for(auto c : sentence){
		if(c==' '){
			if(temp!=""){
				ans.push_back(temp);
				temp="";
			}
		}else{
			temp.push_back(c);
		}
	}
	return ans;
}
```

2. in a arithmetric expression we want to get all the numbers and operators from the expression given as string eg. ((14/2)-(743\*824)+5)\*10
```cpp
vector<string> getLiterals(string &expression){
    vector<string> ans;
    string temp = "";
    set<char> operators = {'+','/','-','*','(',')'};
    for(auto c : expression){
        if(operators.count(c)){
            if(temp!=""){
                ans.push_back(temp);
            }
            ans.push_back(string(1,c));
            temp = "";
        }else{
            temp.push_back(c);
        }
    }
    if(temp!=""){
        ans.push_back(temp);
    }
    return ans;
}
```