---
tags:
  - bit-manipulation
---

- **Why focus on XOR?**  
    XOR is crucial because of its unique properties:
    
    - `a ^ 0 = a` → Useful to keep values unchanged.
    - `a ^ a = 0` → Can cancel out duplicates.
    - `a ^ b ^ a = b` → Allows swapping values without a temporary variable.
- **Example of XOR for Swapping**:
```python

a = 5
b = 3
a = a ^ b  # a becomes 6 (binary 110)
b = a ^ b  # b becomes 5 (binary 101)
a = a ^ b  # a becomes 3 (binary 011)
print(a, b)  # Output: 3, 5
```

**Practical Applications**:
- Detecting odd occurrences in a list.
- Efficient parity checks in data transmission.
- Swapping values without extra memory.

