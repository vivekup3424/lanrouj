### Problem Statement
Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

### Approach

- **Define** a map to match each closing bracket with its opening bracket:
    - `')' -> '('`, `'}' -> '{'`, and `']' -> '['`.
- **Initialize** an empty stack.
- **For** each character `ch` in the string:
    - **If** `ch` is a closing bracket (`)`, `}`, or `]`):
        - **If** the stack is empty, or the top of the stack is not the matching opening bracket for `ch`:
            - **Return** `false` (the string is unbalanced).
        - **Else**, pop the top element from the stack (it’s a match).
    - **Else** (it’s an opening bracket `(`, `{`, or `[`):
        - Push `ch` onto the stack.
    
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

### Other Questions similar to this
1. [[MinimumAddToMakeParenthesesValid]]
	1. In this question the only extra step is the calculate of the extra closing parentheses after each step, and the total extra openinig parentheses.
	2. And then output their sum
2. 