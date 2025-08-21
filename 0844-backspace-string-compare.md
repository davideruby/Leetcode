## [844. Backspace String Compare](https://leetcode.com/problems/backspace-string-compare/)

${\textsf{\color{green}Easy}}$

Given two strings s and t, return true if they are equal when both are typed into empty text editors. '#' means a backspace character.

Note that after backspacing an empty text, the text will continue empty.

## Solution
```python
class Solution:
    def backspaceCompare(self, s: str, t: str) -> bool:
        return self.typed(s) == self.typed(t)

    def typed(self, string):
        BACKSPACE = "#"
        stack = []

        for char in string:
            if char == BACKSPACE:
                if len(stack) > 0:
                    stack.pop()
            else:
                stack.append(char)
        
        return "".join(stack)
```

## Notes
Use a stack to get the typed version of a string.
