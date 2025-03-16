### Problem Statement
Given an **integer N** and an array of size **N-1** containing N-1 numbers between 1 to N. Find the number(_between 1 to N_), that is not present in the given array.

### Solution
My approach is simple
1. The sum of first n natural numbers  = (n * (n+1))/2;
2. Calculate the current sum
3. subtract total sum by current sum to get the desired number

### XOR Approach
for a0 ^ a1 ^ a2 .... an
and then basically you should get what I am trying to say
