### **Implementing Two Stacks in a Single Array**

#### **Problem Statement:**
We need to implement two stacks in a single array such that both stacks operate efficiently. One stack will push and pop elements from the beginning of the array, and the other will push and pop elements from the end of the array. 
This approach will optimize space by utilizing the available memory in the array from both ends.

#### **Approach:**
- We initialize a single array to store both stacks.
- We maintain two variables: one (`top1`) for the top of the first stack (left side) and the other (`top2`) for the top of the second stack (right side).
- The idea is to allow both stacks to grow towards each other, so the first stack grows from the left to right (`top1` starts at 0), and the second stack grows from right to left (`top2` starts at the size of the array minus 1).
- The `push` operation for each stack will add elements at `top1` or `top2`, respectively.
- The `pop` operation will remove elements from the `top1` or `top2` and update their indices accordingly.

### **Code Implementation:**

```cpp
#include <iostream>
#include <stdexcept>
using namespace std;

class TwoStacks {
private:
    int *arr;           // Array to store elements of both stacks
    int size;           // Size of the array
    int top1, top2;     // Top indices for both stacks

public:
    // Constructor to initialize the array and the top indices
    TwoStacks(int s) {
        size = s;
        arr = new int[size];
        top1 = -1;     // Stack 1 is empty
        top2 = size;   // Stack 2 is empty
    }

    // Push an element onto Stack 1
    void push1(int value) {
        // Check for overflow (if top1 crosses top2)
        if (top1 + 1 == top2) {
            throw runtime_error("Stack Overflow: No space left for Stack 1");
        }
        arr[++top1] = value;  // Increment top1 and push value
    }

    // Push an element onto Stack 2
    void push2(int value) {
        // Check for overflow (if top2 crosses top1)
        if (top2 - 1 == top1) {
            throw runtime_error("Stack Overflow: No space left for Stack 2");
        }
        arr[--top2] = value;  // Decrement top2 and push value
    }

    // Pop an element from Stack 1
    int pop1() {
        // Check if Stack 1 is empty
        if (top1 == -1) {
            throw runtime_error("Stack Underflow: Stack 1 is empty");
        }
        return arr[top1--];  // Pop the top element from Stack 1
    }

    // Pop an element from Stack 2
    int pop2() {
        // Check if Stack 2 is empty
        if (top2 == size) {
            throw runtime_error("Stack Underflow: Stack 2 is empty");
        }
        return arr[top2++];  // Pop the top element from Stack 2
    }

    // Destructor to free the allocated memory
    ~TwoStacks() {
        delete[] arr;
    }
};
```

*Driver Code*
```c++
int main() {
    try {
        TwoStacks stacks(10);  // Create an array of size 10 to hold both stacks
        
        // Push elements onto Stack 1
        stacks.push1(10);
        stacks.push1(20);
        stacks.push1(30);

        // Push elements onto Stack 2
        stacks.push2(40);
        stacks.push2(50);
        stacks.push2(60);

        // Pop elements from Stack 1
        cout << "Popped from Stack 1: " << stacks.pop1() << endl;  // 30
        cout << "Popped from Stack 1: " << stacks.pop1() << endl;  // 20

        // Pop elements from Stack 2
        cout << "Popped from Stack 2: " << stacks.pop2() << endl;  // 60
        cout << "Popped from Stack 2: " << stacks.pop2() << endl;  // 50

    } catch (const runtime_error& e) {
        cout << e.what() << endl;  // Handle errors (overflow/underflow)
    }

    return 0;
}
```

### **Explanation:**
1. **Class Definition (`TwoStacks`)**:
   - **arr**: The array holding the elements for both stacks.
   - **size**: The total size of the array.
   - **top1**: Tracks the top of Stack 1 (from the left side).
   - **top2**: Tracks the top of Stack 2 (from the right side).
   - **Constructor** initializes `top1` to `-1` (empty stack 1) and `top2` to `size` (empty stack 2).
   
2. **Push Operations**:
   - **push1(value)**: Adds elements to Stack 1 by incrementing `top1`.
   - **push2(value)**: Adds elements to Stack 2 by decrementing `top2`.

3. **Pop Operations**:
   - **pop1()**: Removes and returns elements from Stack 1 by decrementing `top1`.
   - **pop2()**: Removes and returns elements from Stack 2 by incrementing `top2`.

4. **Overflow and Underflow Handling**:
   - Overflow occurs when `top1` reaches `top2` (no space left for new elements).
   - Underflow occurs when trying to pop from an empty stack (`top1 == -1` for Stack 1 or `top2 == size` for Stack 2).

5. **Destructor**: Frees the dynamically allocated memory for the array.

### **Example Output:**

```
Popped from Stack 1: 30
Popped from Stack 1: 20
Popped from Stack 2: 60
Popped from Stack 2: 50
```

### **Time and Space Complexity:**

- **Time Complexity**:
  - **push1(value)** and **push2(value)**: O(1) - Constant time for pushing an element onto either stack.
  - **pop1()** and **pop2()**: O(1) - Constant time for popping an element from either stack.

- **Space Complexity**: 
  - O(N) where `N` is the size of the array. We only use the array to store the elements, and no additional space is used except for the array itself.

This implementation efficiently manages two stacks in one array, using constant time for each push and pop operation.