### Problem Statement
Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

### Approach
1. Thing of the problem in terms of stack
2. Or store the pair of opening and closing brackets
```cpp
class Solution
{
public:
    bool isValid(string s)
    {
        stack<char> stk;
        for (const char &c : s)
        {
            if (c == '(' or c == '{' or c == '[')
            {
                stk.push(c);
            }
            else if (c == ']')
            {
                if (stk.empty() or stk.top() != '[')
                    return false;
                else
                    stk.pop();
            }
            else if (c == '}')
            {
                if (stk.empty() or stk.top() != '{')
                    return false;
                else
                    stk.pop();
            }
            else if (c == ')')
            {
                if (stk.empty() or stk.top() != '(')
                    return false;
                else
                    stk.pop();
            }
        }
        if (!stk.empty())
            return false;
        return true;
    }
};

```

