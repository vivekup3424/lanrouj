## 📝 **Problem: Longest Nice Subarray**

### **Problem Statement**

Given an array of integers `nums`, find the length of the **longest subarray** where the **bitwise AND** of every pair of elements is **zero**.

**In other words**, in this subarray, no two numbers should have a **common bit set** to `1`.

### **Example**

#### **Input**

```python
nums = [1, 3, 8, 48, 10]
```

#### **Output**

```python
3
```

#### **Explanation**

The longest **"nice" subarray** is `[3, 8, 48]` because:

- `3 & 8 == 0`
- `3 & 48 == 0`
- `8 & 48 == 0`
- **Size of the subarray = `3`**

---

## 📌 **Constraints**

- `1 ≤ nums.length ≤ 10⁵`
- `1 ≤ nums[i] ≤ 10⁹`
- Each `nums[i]` is a **positive integer**.

---

## ✅ **Approach**

### **Using Sliding Window & Bit Frequency Count**

We use a **sliding window approach** to maintain a subarray where **no two numbers share common bits**.

### **Key Idea**

1. Use a **bit frequency hashmap** (`freqHashmap`) to track the count of **each bit position (0-63)** in the **current window**.
2. Expand the window (`j`) while ensuring all elements in the window have **unique bits**.
3. If adding a new number `nums[j]` causes a **bit conflict** (a bit appears twice):
    - Shrink the window (`i++`) **until** the conflict is removed.
4. **Track the maximum window size** found during this process.

---

## 🏃 **Dry Run**

### **Input**

```python
nums = [1, 3, 8, 48, 10]
```

### **Step-by-Step Execution**

|`j`|`nums[j]`|`bitmask` Before|Conflict?|Shrink `i`?|`i` (After)|`bitmask` After|`maxLen`|
|---|---|---|---|---|---|---|---|
|0|1|0|No|No|0|1|1|
|1|3|1|No|No|0|3|2|
|2|8|3|No|No|0|11|3|
|3|48|11|No|No|0|59|4|
|4|10|59|Yes|Yes|3|58|4|

### **Final Output**

```python
4
```

---

## ⏳ **Time Complexity Analysis**

- **Each element is added and removed once** → **O(N)**
- **Bit operations are O(1) since there are at most 64 bits** → **O(1)**
- **Total complexity**: **O(N)** ✅

---

### **Summary**

- Use a **sliding window** to maintain a "nice" subarray.
- Track the **bit frequencies** using a hashmap.
- **Expand** the window and **shrink** if a conflict arises.
- **Optimal solution runs in O(N) time.**

---

This should be a great addition to your **Obsidian notes**! Let me know if you want any refinements. 🚀