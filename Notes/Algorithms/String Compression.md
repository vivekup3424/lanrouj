---
tags:
  - string
  - blind-75
---

Given an array of characters chars, compress it using the following algorithm:-
Begin with an empty string s. For each group of consecutive repeting characters in chars:
- If the group's length is 1, append the character to s.
- Otherwise, append the character followed by the group's length.
The compressed string s should not be returned seperately, but instead be stored in the input character array chars. (whatever that means)

After you are done modifying the input array, return the new length of the array.

```java
class Solution {
	public int compress(char[] chars) {
		StringBuilder temp = new StringBuilder();
		Integer i = 0;
		while (i < chars.length) {
			Integer current_length = 0;
			Character current_char = chars[i];
			while (i < chars.length && chars[i] == current_char) {
				current_length++;
				i++;
			}
			temp.append(current_char);
			if (current_length > 1) {
				String lengthString = current_length.toString();
				temp.append(lengthString);
			}
		}
		System.out.println(temp);
		for (int r = 0; r < temp.length(); r++) {
			chars[r] = temp.charAt(r);
		}
		return temp.length();
	}
}
```
Time Complexity = linear worst case time compexity
Space Complexity = constant extra space