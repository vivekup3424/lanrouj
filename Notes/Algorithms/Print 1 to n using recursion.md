```js
// Function to print numbers from i to n recursively
function print1toN(i, n) {
  if (i === n) {
    process.stdout.write(`${i} `); // Inline output
    return;
  }
  process.stdout.write(`${i} `); // Inline output
  print1toN(i + 1, n);
}
```

