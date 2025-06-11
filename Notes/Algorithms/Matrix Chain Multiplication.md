![[Pasted image 20241216234738.png]]
![[Pasted image 20241216234822.png]]
```python
def matrix_chain_order(p):
    n = len(p) - 1
    m = [[0] * (n + 1) for _ in range(n + 1)]

    # l is chain length
    for l in range(2, n + 1):
        for i in range(1, n - l + 2):
            j = i + l - 1
            m[i][j] = float('inf')
            for k in range(i, j):
                cost = m[i][k] + m[k+1][j] + p[i-1] * p[k] * p[j]
                m[i][j] = min(m[i][j], cost)

    return m[1][n]

```
