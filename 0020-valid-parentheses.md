## [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

<h2 style="color:#00b8a3">Easy</h2>
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

## Solution
```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        close_to_open = { ")": "(", "]": "[", "}": "{"}

        for char in s:
            is_closing_bracket = char in close_to_open
            if is_closing_bracket:
                open_bracket = close_to_open[char]
                if len(stack) == 0 or stack.pop() != open_bracket:
                    return False
            else:
                stack.append(char)

        return len(stack) == 0
```

## Notes
If the current character is a closing bracket, check that the character on top of che stack is the relative opening bracket.