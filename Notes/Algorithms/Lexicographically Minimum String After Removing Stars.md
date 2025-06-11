You are given a string `s`. It may contain any number of `'*'` characters. Your task is to remove all `'*'` characters.

While there is a `'*'`, do the following operation:

- Delete the leftmost `'*'` and the **smallest** non-`'*'` character to its _left_. If there are several smallest characters, you can delete any of them.

Return the lexograpically smallest resulting string after removing all `'*'` characters.