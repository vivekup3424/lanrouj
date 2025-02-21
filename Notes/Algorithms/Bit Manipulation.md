Bitwise operators operate on binary representations of integers. They perform bit-level operations and are typically faster than arithmetic operations.

---

### **1. Bitwise AND (`&`)**

- **Operation**: Compares each bit of two integers. Result is `1` if both bits are `1`, otherwise `0`.
- **Usage**: Used to mask or clear specific bits.
- **Example**:
    
    ```python
    a = 6  # Binary: 110
    b = 4  # Binary: 100
    result = a & b  # Binary: 100 → 4
    ```
    

---

### **2. Bitwise OR (`|`)**

- **Operation**: Compares each bit of two integers. Result is `1` if either bit is `1`.
- **Usage**: Used to set specific bits.
- **Example**:
    
    ```python
    a = 6  # Binary: 110
    b = 4  # Binary: 100
    result = a | b  # Binary: 110 → 6
    ```
    

---

### **3. Bitwise XOR (`^`)**

- **Operation**: Compares each bit of two integers. Result is `1` if bits are different, `0` if the same.
- **Usage**: Toggles specific bits.
- **Note**: Please see [[Importance of Bitwise XOR]]
- **Example**:
    
    ```python
    a = 6  # Binary: 110
    b = 4  # Binary: 100
    result = a ^ b  # Binary: 010 → 2
    ```
    

---

### **4. Bitwise NOT (`~`)**

- **Operation**: Inverts all bits (1 becomes 0, and 0 becomes 1).
- **Usage**: Flips all bits and changes the sign in Python due to 2's complement representation.
- **Example**:
    
    ```python
    a = 15  # Binary: 00001111
    result = ~a  # Binary: 11110000 → -16
    ```
    

---

### **5. Left Shift (`<<`)**

- **Operation**: Shifts all bits to the left by a specified number of positions. Fills with `0` on the right.
- **Usage**: Multiplies the number by `2^n` (where `n` is the shift count).
- **Example**:
    
    ```python
    a = 1  # Binary: 00000001
    result = a << 3  # Binary: 00001000 → 8
    ```
    

---

### **6. Right Shift (`>>`)**

- **Operation**: Shifts all bits to the right by a specified number of positions.
    - For positive numbers: Fills with `0` on the left.
    - For negative numbers: Fills with `1` on the left (sign bit preserved).
- **Usage**: Divides the number by `2^n` (integer division).
- **Example**:
    
    ```python
    a = 8  # Binary: 1000
    result = a >> 2  # Binary: 0010 → 2
    ```
    

---

### **Special Notes**

1. **Negative Numbers and 2's Complement**:
    
    - Python represents negative numbers in 2's complement format.
    - For example, `-6` in 8 bits:
        - Binary of `6`: `00000110`.
        - Invert bits: `11111001`.
        - Add `1`: `11111010`.
2. **Logical vs Arithmetic Shifts**:
    
    - Python does not have an **unsigned right shift** because integers have infinite precision.
    - Right shift (`>>`) always preserves the sign bit for negative numbers.

---

### **Common Use Cases**

- **Masking**: Extract specific bits using `&`.
    
    ```python
    num = 29  # Binary: 11101
    mask = 0b111  # Binary: 00111
    result = num & mask  # Binary: 00101 → 5
    ```
    
- **Bit Flags**: Use `|` to set flags and `&` to check flags.
    
- **Power of 2 Checks**:
    
    ```python
    num = 16
    is_power_of_2 = (num & (num - 1)) == 0  # True if power of 2
    ```
    
- **Swapping Variables**: Without a temporary variable:
    
    ```python
    a, b = 5, 3
    a = a ^ b
    b = a ^ b
    a = a ^ b
    ```
    

---

### **Summary Table**

|Operator|Symbol|Example|Binary Result|Decimal Result|
|---|---|---|---|---|
|AND|`&`|`6 & 4`|`00000100`|`4`|
|OR|`|`|`6|4`|
|XOR|`^`|`6 ^ 4`|`00000010`|`2`|
|NOT|`~`|`~15`|`11110000`|`-16`|
|Left Shift|`<<`|`1 << 3`|`00001000`|`8`|
|Right Shift|`>>`|`8 >> 2`|`00000010`|`2`|

---

### Practice

1. What is the result of `~6`?
2. Use bitwise operators to check if a number is odd or even.
3. Write a Python program to count the number of set bits in an integer.
## Problems
1. [[Shortest Subarray With OR at Least K II]]
2. [[count-set-bits]]

## [[Bit Set]]
Important data structure for bit manipulation
