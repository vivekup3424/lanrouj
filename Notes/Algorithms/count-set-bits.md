---
id: count-set-bits
aliases: []
tags:
  - bit-manipulation
  - algorithms
  - set-bits
---

# Count Set Bits
Write a program to count the number of set bits in an integer.

```python
def count_bits(x):
    num_bits = 0
    while x:
        num_bits += x & 1
        x >>= 1
    return num_bits
```

**Time Complexity:** O(log n)
**Space Complexity:** O(1)

In the above algorithm we are doing a brute-force of sorts, where we are going to all the 
m = log(n) bits, and checking if they are set ot not
We can do one improvement by only going to the bits of number that are set originally and then unsetting them, that we can going to p bits, where
$p <= m$ 

```python
 def count_bits(x):
    num_bits = 0
    while x:
        x &= x - 1
        num_bits += 1
    return num_bits
```
