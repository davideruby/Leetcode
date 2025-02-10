## [3174. Clear Digits](https://leetcode.com/problems/clear-digits/)

${\textsf{\color{green}Easy}}$

You are given a string s.

Your task is to remove all digits by doing this operation repeatedly:

- Delete the first digit and the closest non-digit character to its left.

Return the resulting string after removing all digits.

## Solution
```python
class Solution:
    def clearDigits(self, s: str) -> str:
        stack = []
        digits = set(['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'])

        for char in s:
            if char in digits:
                stack.pop()
            else:
                stack.append(char)

        return ''.join(stack)
```

## Notes
Use a stack.
