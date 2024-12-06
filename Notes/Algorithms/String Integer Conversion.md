### Implement an integer to string conversion function, and a string to integer conversison function.

For example, if the input to the first function is the integer 314, it should return the string "314" and
if the input to the second function is the string "314" it should return the integer 314.

## Integer to String Conversion
If the number has more than one digit, it is natural to perform the conversion digit-by-digit. The
key insight is that for any positive integer x, the least significant digit in the decimal representation
of x is x mod 10, and the remaining digits are x/10. This approach computes the digits in reverse
order, e.g., if we begin with 423, we get 3 and are left with 42 to convert. Then we get 2, and are left
with 4 to convert. Finally, we get 4 and there are no digits to convert.

