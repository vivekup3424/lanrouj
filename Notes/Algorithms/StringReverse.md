- [Using backward traversal – O(n) Time and O(n) Space](https://www.geeksforgeeks.org/string-reverse/#using-a-loop-on-time-and-on-space)
- [Using Two Pointers – O(n) Time and O(n) Space](https://www.geeksforgeeks.org/string-reverse/#reverse-string-using-two-pointers-on-time-and-on-space)
- [Using Recursion – O(n) Time and O(n) Space](https://www.geeksforgeeks.org/string-reverse/#reverse-string-using-recursion-on-time-and-on-space)
- [Using Stack – O(n) Time and O(n) Space](https://www.geeksforgeeks.org/string-reverse/#using-stack-on-time-and-on-space)
- [Using Inbuilt methods – O(n) Time and O(1) Space](https://www.geeksforgeeks.org/string-reverse/#reverse-string-using-inbuilt-method-on-time-and-o1-space)

```js
function reverseString(s) {
    let res = [];
  
    // Traverse `s` in backward direction
    // and add each character to the `res` array
    for (let i = s.length - 1; i >= 0; i--) {
        res.push(s[i]);
    }
  
    // Join the array to form the reversed string
    return res.join('');
}

// Test the function
const s = "abdcfe";
console.log(reverseString(s));  // Output: "efcdba"

```

