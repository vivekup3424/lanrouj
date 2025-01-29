---
tags:
  - awk
  - grep
  - pipeline
---

# AWK
Certainly! `awk` is a powerful text processing tool in Unix/Linux for handling and manipulating data. It's widely used for pattern scanning, processing, and reporting.
### **Getting Started with `awk`**

`awk` operates by reading input line by line and splitting each line into fields. It can then perform actions on specific fields or lines based on patterns you specify.

### **Basic Syntax**

The general syntax of an `awk` command is:

```bash
awk 'pattern {action}' file
```

- **`pattern`**: The condition to match (e.g., a string, a regular expression, or a numeric comparison). If no pattern is provided, `awk` will apply the action to every line.
- **`action`**: The action to perform when the pattern is matched (e.g., printing data, performing arithmetic operations, etc.). If no action is specified, the default is to print the matching line.

### **1. Printing Columns**

By default, `awk` splits each input line into fields separated by spaces or tabs. These fields are referred to as `$1`, `$2`, ..., `$NF` (where `NF` is the number of fields in the current line).

#### Example 1: Print the first column

```bash
awk '{print $1}' filename
```

- This prints the first column of each line in the file.

#### Example 2: Print the second and third columns

```bash
awk '{print $2, $3}' filename
```

#### Example 3: Print all columns

```bash
awk '{print $0}' filename
```

- `$0` refers to the entire line (i.e., all columns).

### **2. Pattern Matching**

You can specify a pattern to match lines before performing actions.

#### Example 4: Print lines that match a pattern

```bash
awk '/pattern/ {print $0}' filename
```

- This prints lines containing "pattern".

#### Example 5: Print lines where the second column is greater than 100

```bash
awk '$2 > 100 {print $1, $2}' filename
```

- This prints the first and second columns only if the second column is greater than 100.

### **3. Field Separators**

By default, `awk` uses spaces or tabs as field separators. You can change this using the `-F` flag or the `FS` variable inside the program.

#### Example 6: Set a custom field separator

```bash
awk -F ',' '{print $1, $2}' filename
```

- This sets the field separator to a comma (`,`) and prints the first and second columns.

You can also use regular expressions for field separators:

```bash
awk 'BEGIN {FS=":"} {print $1, $2}' filename
```

- This sets the field separator to a colon (`:`) and prints the first and second columns.

### **4. BEGIN and END Blocks**

You can use `BEGIN` and `END` blocks for actions that should occur before processing starts or after processing finishes.

#### Example 7: Using BEGIN

```bash
awk 'BEGIN {print "Start Processing"} {print $1}' filename
```

- The `BEGIN` block runs before processing any data, and then the action prints the first column of the file.

#### Example 8: Using END

```bash
awk 'END {print "End of Processing"}' filename
```

- The `END` block runs after all lines are processed.

### **5. Arithmetic Operations**

`awk` can perform arithmetic on fields.

#### Example 9: Add two columns

```bash
awk '{sum = $1 + $2; print sum}' filename
```

- This adds the first and second columns and prints the result.

#### Example 10: Average of a column

```bash
awk '{sum += $1} END {print sum/NR}' filename
```

- `sum += $1`: Adds the values in the first column.
- `NR`: The number of records (lines) processed.
- The `END` block prints the average of the first column.

### **6. Conditionals**

You can use conditionals inside `awk` to control which lines to process.

#### Example 11: If-else statement

```bash
awk '{if ($1 > 50) print "High", $1; else print "Low", $1}' filename
```

- This checks if the first column is greater than 50 and prints "High" or "Low" accordingly.

### **7. Using Variables in `awk`**

You can define and use variables in `awk`.

#### Example 12: Defining and using variables

```bash
awk '{threshold = 50; if ($1 > threshold) print $1}' filename
```

- The `threshold` variable is set to 50, and `awk` checks if the first column is greater than this threshold.

### **8. Processing Multiple Files**

`awk` can handle multiple files at once.

#### Example 13: Process multiple files

```bash
awk '{print $1}' file1 file2
```

- This prints the first column of both `file1` and `file2`.

### **9. Print Line Numbers**

You can print the line number using the `NR` variable.

#### Example 14: Print line numbers with content

```bash
awk '{print NR, $0}' filename
```

- This prints the line number followed by the entire line.

### **10. User-defined Functions**

`awk` supports defining and using functions.

#### Example 15: Define a function to calculate square

```bash
awk 'function square(x) { return x * x } {print square($1)}' filename
```

- This defines a function `square` to return the square of a number, and then prints the square of the first column for each line.

---

### **Useful `awk` Examples**

#### Example 16: Print lines with more than 3 columns

```bash
awk 'NF > 3' filename
```

- `NF` represents the number of fields in the current line. This command prints lines with more than 3 fields.

#### Example 17: Sum values in a column

```bash
awk '{sum += $1} END {print "Total:", sum}' filename
```

#### Example 18: Print unique values from a column

```bash
awk '{print $1}' filename | sort | uniq
```

- This extracts the first column, sorts the values, and prints only unique entries.

---

### **Additional Tips:**

- **Escape characters**: You may need to escape special characters like `{`, `}`, and `$` in `awk` if used within strings.
- **Quoting**: Single quotes (`'`) are typically used for `awk` programs in the shell to avoid issues with shell interpretation of characters.

---
