Given two strings `s` and `t`, return `true` _if_ `s` _is a **subsequence** of_ `t`_, or_ `false` _otherwise_.

A **subsequence** of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (i.e., `"ace"` is a subsequence of `"abcde"` while `"aec"` is not).

**Example 1:**

**Input:** s = "abc", t = "ahbgdc"
**Output:** true

**Example 2:**

**Input:** s = "axc", t = "ahbgdc"
**Output:** false

**Constraints:**

- `0 <= s.length <= 100`
- `0 <= t.length <= 104`
- `s` and `t` consist only of lowercase English letters.

My solution
```python
def isSubsequence(self, s: str, t: str) -> bool:
	i,j = 0,0 #i == s, j == t
	while i < len(s) and j < len(t):
		if s[i] == t[j]:
			i+=1
		j+=1
	return i == len(s)
```

### Follow up:-
Suppose there are lots of incoming `s`, say `s1, s2, ..., sk` where `k >= 10^9`, and you want to check one by one to see if `t` has its subsequence. In this scenario, how would you change your code?
