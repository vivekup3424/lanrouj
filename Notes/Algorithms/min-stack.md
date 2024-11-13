Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

You must implement a solution with `O(1)` time complexity for each function.

**Constraints:**

- $-2^{31} <= val <= 2^{31} - 1$
- Methods `pop`, `top` and `getMin` operations will always be called on **non-empty** stacks.
- At most `3 * 104` calls will be made to `push`, `pop`, `top`, and `getMin`.
```c++
class MinStack
{
    // Naive Approach
public:
    stack<pair<int, int>> stk;
    MinStack()
    {
        ;
    }
    void push(int val)
    {
        if (stk.size() == 0)
        {
            stk.push({val, val});
        }
        else
        {
            int mini = min(val, stk.top().second);
            stk.push({val, mini});
        }
    }
    void pop()
    {
        if (stk.size() > 0)
        {
            stk.pop();
        }
    }
    int top()
    {
        return stk.top().first;
    }
    int getMin()
    {
        return stk.top().second;
    }
};

```