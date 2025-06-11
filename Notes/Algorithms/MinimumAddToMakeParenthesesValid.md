### Problem Statement
A parentheses string is valid if and only if:

- It is the empty string,
- It can be written as `AB` (`A` concatenated with `B`), where `A` and `B` are valid strings, or
- It can be written as `(A)`, where `A` is a valid string.

You are given a parentheses string `s`. In one move, you can insert a parenthesis at any position of the string.

- For example, if `s = "()))"`, you can insert an opening parenthesis to be `"(**(**)))"` or a closing parenthesis to be `"())**)**)"`.

Return _the minimum number of moves required to make_ `s` _valid_.


### My Approach
![[Pasted image 20241109235235.png]]
```cpp
class Solution {
public:
    int minAddToMakeValid(string s) {
        int opening = 0; //counts the number of opening brackets currently
        int closing = 0; //count the number of extra closing bracket, without the opening bracket paired with them
        for(char c: s){
            if(opening == 0){
                if(c==')'){
                    closing++;
                }
                else{
                    opening++;
                }
            }
            else{
                if(c=='(')opening++;
                else if(c==')')opening--;
            }
        }
        return opening+closing;
    }
};

```

