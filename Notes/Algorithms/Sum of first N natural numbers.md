---
tags:
  - recursion
---
```js
const calculateSum = (n) => {
  if (n == 0) {
    return 0;
  } else {
    return n + calculateSum(n - 1);
  }
};

```