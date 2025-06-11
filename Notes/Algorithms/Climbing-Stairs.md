The _climbing stairs problem_ is a classic problem in dynamic programming. It involves finding the number of distinct ways to climb a staircase with nn steps, where you can take either 1 step or 2 steps at a time.

### Problem Statement

Given **n**, the number of stairs, determine how many distinct ways you can reach the top.

### Approach: Caching (Memoization)

Memoization is a technique where we store the results of expensive function calls and reuse them when the same inputs occur again. In this case, we can use an array (or a dictionary) to cache the results of subproblems.

### Recursive Solution with Caching

The recursive relation is:

f(n)=f(n−1)+f(n−2)f(n) = f(n-1) + f(n-2)

This means that the number of ways to climb nn stairs is the sum of:

1. The ways to climb n−1n-1 stairs (taking a single step), and
2. The ways to climb n−2n-2 stairs (taking two steps).

Here's how you can implement it in Python:

```python
def climb_stairs(n, memo=None):
    if memo is None:
        memo = {}
    
    # Base cases
    if n == 0:  # No steps left to climb
        return 1
    if n < 0:  # Invalid case
        return 0
    
    # Check if result is already cached
    if n in memo:
        return memo[n]
    
    # Recursive computation with caching
    memo[n] = climb_stairs(n-1, memo) + climb_stairs(n-2, memo)
    return memo[n]

# Example usage:
n = 5
print(f"Number of ways to climb {n} stairs: {climb_stairs(n)}")
```

### Explanation

1. **Base Cases**:
    - If n=0n = 0: There is one way to stay where you are (do nothing).
    - If n<0n < 0: There are no ways to climb negative steps.
2. **Memoization**:
    - The `memo` dictionary stores results of previously solved subproblems, preventing redundant calculations.
3. **Recursive Relation**:
    - The function calls itself for n−1n-1 and n−2n-2, summing the results and caching the outcome for nn.

### Time Complexity

- Each subproblem (nn) is computed only once, and there are O(n)O(n) subproblems.
- The time complexity is O(n)O(n).

### Space Complexity

- Space is used for the recursion stack (O(n)O(n)) and the memo dictionary (O(n)O(n)).
- Total space complexity is O(n)O(n).

### Iterative Version with Caching (Optional)

If you prefer avoiding recursion, you can use an iterative approach:

```python
def climb_stairs_iterative(n):
    if n == 0:
        return 1
    if n == 1:
        return 1
    
    dp = [0] * (n + 1)
    dp[0] = 1
    dp[1] = 1
    
    for i in range(2, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]
    
    return dp[n]

# Example usage:
n = 5
print(f"Number of ways to climb {n} stairs: {climb_stairs_iterative(n)}")
```

This uses an array `dp` to store intermediate results, reducing the space complexity of the recursion stack.