---
tags:
  - recursion
---
## What is Recursion?
- **Definition**: A function that calls itself directly or indirectly to solve a problem.
- **Components**:
  - **Base Case**: The condition that terminates the recursion.
  - **Recursive Case**: The logic where the function calls itself.

---

## How Recursion Works
1. A recursive function is pushed onto the call stack every time it is called.
2. Once the base case is met, the stack unwinds, resolving each call step-by-step.

---

## Types of Recursion
1. **Direct Recursion**: A function calls itself directly.
   ```python
   def factorial(n):
       if n == 0:
           return 1  # Base case
       return n * factorial(n - 1)  # Recursive case
```

2. **Indirect Recursion**: A function calls another function that calls it back.
    
    ```python
    def functionA():
        functionB()
    def functionB():
        functionA()
    ```
    

---

## Advantages of Recursion

- Simplifies code for problems that have repetitive substructure (e.g., tree traversal).
- Natural solution for divide-and-conquer problems (e.g., [[Merge Sort]], [[Quick Sort]]).

---

## Disadvantages of Recursion

- **Stack Overflow**: Too many recursive calls may exceed the stack memory.
- **Overhead**: Recursive calls involve function call overheads compared to iterative solutions.

---

## Examples of Recursive Problems

### Factorial

```python
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n - 1)
```

### Fibonacci Sequence

```python
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)
```

### Tower of Hanoi

```python
def tower_of_hanoi(n, source, target, auxiliary):
    if n == 1:
        print(f"Move disk 1 from {source} to {target}")
        return
    tower_of_hanoi(n - 1, source, auxiliary, target)
    print(f"Move disk {n} from {source} to {target}")
    tower_of_hanoi(n - 1, auxiliary, target, source)
```

---

## Tail Recursion

- A special case where the recursive call is the last operation in the function.
- **Optimization**: Many compilers optimize tail-recursive functions to avoid stack overflow.

```python
def tail_recursive_factorial(n, accumulator=1):
    if n == 0:
        return accumulator
    return tail_recursive_factorial(n - 1, n * accumulator)
```

---

## Common Patterns in Recursion

1. **Divide and Conquer**:
    - Break the problem into smaller subproblems, solve recursively, and combine results.
    - Example: Merge Sort, Quick Sort.
2. **Tree Traversals**:
    
    - Preorder, Inorder, Postorder traversal in Binary Trees.
    
    ```python
    def inorder_traversal(root):
        if root is not None:
            inorder_traversal(root.left)
            print(root.val)
            inorder_traversal(root.right)
    ```
    
3. **Backtracking**:
    - Explore all possible solutions and backtrack on invalid paths.
    - Example: N-Queens Problem, Sudoku Solver.

---

## Steps to Solve a Recursive Problem

1. Identify the **base case**.
2. Define the **recursive case**.
3. Ensure the problem **converges** to the base case.
4. **Dry run** with simple examples to verify correctness.

---

## Recursion vs Iteration

|**Aspect**|**Recursion**|**Iteration**|
|---|---|---|
|Approach|Function calls itself|Loop structures|
|Memory Usage|Uses call stack|Uses loop counters|
|Readability|Cleaner for complex problems|Clear for simple problems|
|Efficiency|May lead to stack overflow|Typically faster and less memory-intensive|

---

## Practice Problems

1. Factorial Calculation
2. Fibonacci Sequence
3. [[Tower of Hanoi]]
4. N-Queens Problem
5. Permutations of a String
6. Subset Generation (Power Set)
7. Binary Search (Recursive Version)
8. Depth-First Search (DFS) for Graphs
9. [[Print 1 to n using recursion]]
---

## Debugging Tips

1. **Trace Recursive Calls**: Use print statements to track function inputs and outputs.
2. **Check Base Case**: Ensure it terminates correctly.
3. **Limit Recursive Depth**: Test for large inputs to avoid stack overflow.
4. **Memoization**: Use caching for overlapping subproblems (e.g., Fibonacci).

---

## Additional Notes

- Recursion is powerful but should be used judiciously.
- For problems with overlapping subproblems, consider **Dynamic Programming** for efficiency.

```python
# Fibonacci with Memoization
def fibonacci_dp(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fibonacci_dp(n - 1, memo) + fibonacci_dp(n - 2, memo)
    return memo[n]
```

```

You can copy this file directly into Obsidian, and it will be well-organized with headings and code blocks. Let me know if you need additional customization!
```