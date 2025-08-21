---
tags:
  - matrix
  - array
---
<img src="WhatsApp Image 2025-05-19 at 16.51.31_341b841b 1.jpg" width="400px">

## Question
Given an `m x n` integer matrix `matrix`, if an element is `0`, set its entire row and column to `0`'s.
You must do it [in place](https://en.wikipedia.org/wiki/In-place_algorithm).

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/08/17/mat1.jpg)

**Input:** `matrix = [[1,1,1],[1,0,1],[1,1,1]]`  
**Output:** `[[1,0,1],[0,0,0],[1,0,1]]`


**Example 2:**

![](https://assets.leetcode.com/uploads/2020/08/17/mat2.jpg)

**Input:** matrix = `[[0,1,2,0],[3,4,5,2],[1,3,1,5]]`
**Output:** `[[0,0,0,0],[0,4,5,0],[0,3,1,0]]`

**Constraints:**
$$
\begin{aligned}
m &= \texttt{matrix.length} \\
n &= \texttt{matrix[0].length} \\
1 &\leq m, n \leq 200 \\
-2^{31} &\leq \texttt{matrix}[i][j] \leq 2^{31}-1
\end{aligned}
$$

**Follow up:**

- A straightforward solution using `O(mn)` space is probably a bad idea.
- A simple improvement uses `O(m + n)` space, but still not the best solution.
- Could you devise a constant space solution?

Some things to ponder over-
1. Since the element in the matrix can be any integer, hence I would not be able to use any integer to mark if a particular row or column need to be zeroed out. And I should not convert the matrix into long long elements as that would be require creating a new matrix altogether.
2. The other approach I can think is finding out an integer that is not inside the matrix and using it as the special integer for us.
3. Now the matrix can contain only 200 x 200 = 40,000 unique elements, but I have a whole range of $-2^{31}$ to $2^{31}$ integers to choose from.
	1. *Attempts at getting unique integers*
		1. Finding the maximum or minimum integer not found in the matrix, this approach can create problem if INT_MAX or INT_MIN is in the matrix
		2. Finding the sum of integers, this approach may lead to integer overflow
		3. Finding the xor of integers, this also doesn't guarantee uniqueness.